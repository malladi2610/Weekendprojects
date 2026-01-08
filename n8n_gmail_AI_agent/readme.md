# Email Parser → Bright Data → AI Fit Scoring → Notion Tracker (n8n)

This n8n workflow turns job-alert emails (LinkedIn / Glassdoor / Indeed) into **structured job entries** in a Notion database.

**Setup & Configuration:** See [SETUP.md](./SETUP.md) for complete installation instructions and credential configuration.

## What it does

1) fetches unread emails from a Gmail label for a chosen date,
2) extracts job links/IDs from the email HTML,
3) enriches job details via Bright Data dataset snapshots,
4) normalizes the job schema across platforms,
5) uses an AI agent to score job fit against multiple CV profiles,
6) writes KEEP/MAYBE jobs into Notion,
7) marks processed emails as read.

## High-level architecture

**Trigger (manual date)** → **Gmail search** → **Split in batches** → **Platform switch**  
→ **Parse + clean URLs** → **Bright Data dataset trigger** → **Poll progress** → **Fetch snapshot**  
→ **Normalize + standardize** → **AI fit scoring** → **IF (KEEP/MAYBE)** → **Notion create page**

Platforms supported:
- LinkedIn (jobs-noreply / jobalerts / jobs-listings)
- Glassdoor (noreply@glassdoor.com)
- Indeed (alert@indeed.com)

---

## How to run

### Option A — open the mini UI (GET)
1. Call the **GET** webhook endpoint (`Webhook` node).
2. You’ll receive a small HTML page with a date picker.
3. Submitting the form sends a **POST** to the **POST webhook** (`Webhook1` node).

### Option B — call the POST webhook directly
Send `runDate=YYYY-MM-DD` (form body) to the **POST webhook** (`Webhook1` node).

---

## Workflow details (node-by-node, by logical blocks)

### 1) Web UI and date → Gmail query
**Nodes:**
- `Webhook` (GET)
- `Respond to Webhook` (returns HTML form)
- `Webhook1` (POST)
- `Code in JavaScript` (builds Gmail search window)

**What happens**
- GET webhook serves a simple HTML form.
- POST webhook receives the selected date (`runDate`).
- `Code in JavaScript` converts the day into:
  - `after:<unix>` and `before:<unix>` timestamps
  - stored as `gmailQuery`

**Why**
- You can replay the pipeline for any date deterministically.
- Avoids parsing “all time” emails.

---

### 2) Fetch unread job-alert emails from Gmail label
**Nodes:**
- `Emails from Followup label` (Gmail: getAll)
- `Loop over` (Split in batches)

**What happens**
- Gmail reads unread emails inside a specific label (`Label_8163...`) filtered by `gmailQuery`.
- `Loop over` processes emails **one by one**.

**Why**
- Split-in-batches prevents memory spikes and makes processing more stable.

---

### 3) Route by platform (LinkedIn / Glassdoor / Indeed)
**Nodes:**
- `Linkedin, glassdoor,indeed segregator` (Switch)

**Logic**
Checks sender address:
- LinkedIn: `jobs-noreply@linkedin.com`, `jobalerts-noreply@linkedin.com`, `jobs-listings@linkedin.com`
- Glassdoor: `noreply@glassdoor.com`
- Indeed: `alert@indeed.com`

Output lanes:
- LinkedIn → `Linkedin_parser`
- Glassdoor → `Glassdoor_parser`
- Indeed → `Indeed_parser`

---

### 4) Platform-specific email parsing (extract URLs/IDs)
#### LinkedIn parsing
**Node:** `Linkedin_parser` (Code)
- Reads the email HTML.
- Splits into paragraphs and extracts:
  - `jobTitle`, `company`, `location`
  - LinkedIn job URLs from `.../comm/jobs/view/<id>`
  - creates `uniqueKey = linkedin:<jobId>` (or fallback)

**Important guard**
- Skips the “Jobs similar to …” paragraph to avoid null/null/null outputs.

#### Glassdoor parsing
**Node:** `Glassdoor_parser` (Code)
- Extracts `partner/jobListing.htm?...jobListingId=<id>` links.
- Creates `uniqueKey = glassdoor:<jobListingId>`.

#### Indeed parsing
**Node:** `Indeed_parser` (Code)
- Extracts Indeed click/tracking links.
- Tries to infer `jobTitle` and `company` from text around the link.
- Extracts `xkcb` as a stable job identifier (stored as `jobId`).
- Creates `uniqueKey = indeed:<jobId>` (or fallback to URL).

---

### 5) Normalize URLs for Bright Data input
Bright Data works best with stable canonical URLs. Each platform has two cleanup steps:
1) normalize single items (build `brightdataUrl`)
2) package into `{ input: [{ url }, ...] }` for the dataset trigger

#### LinkedIn
**Nodes:** `Linkedin_cleaning_block` → `Linkedin_cleaning_block_2`
- Converts to canonical: `https://www.linkedin.com/jobs/view/<jobId>/`
- Creates `json.input = [{ url: brightdataUrl }]`

#### Glassdoor
**Nodes:** `Glassdoor_cleaning_block` → `Glassdoor_cleaning_block_1`
- Converts partner links into canonical `glassdoor.com/job-listing/... ?jl=<id>`
- Packages into `input` array.

#### Indeed
**Nodes:** `Indeed_cleaning_block` → `Indeed_cleaning_block_1`
- Converts click links into `.../viewjob?jk=<xkcb>` when possible.
- Packages into `input` array.

---

### 6) Trigger Bright Data dataset run + poll until ready
Each platform has:
- trigger dataset: `POST /datasets/v3/trigger`
- check progress: `GET /datasets/v3/progress/<snapshot_id>`
- wait (30s)
- IF status == `ready`
- fetch snapshot JSON: `GET /datasets/v3/snapshot/<snapshot_id>?format=json`

#### LinkedIn polling loop
**Nodes:**  
`Brightdata_linkedin_request` → `BD_Status_check` → `Wait` → `If`  
- If **ready** → `Linkedin_snapshot_collector`
- Else → loop back to `BD_Status_check`

#### Glassdoor polling loop
**Nodes:**  
`brightdata_glassdoor_request` → `BD_status_check` → `Wait3` → `If1`  
- If **ready** → `Glassdoor_snapshot_collector`
- Else → loop back to `BD_status_check`

#### Indeed polling loop
**Nodes:**  
`Brightdata_indeed_request` → `BD_status_check1` → `Wait2` → `If2`  
- If **ready** → `Indeed_snapshot_collector`
- Else → loop back to `BD_status_check1`

---

### 7) Normalize Bright Data output into a common schema
Goal: produce the same fields regardless of source.

#### LinkedIn
**Node:** `Normalise_linkedin` (Code)
Outputs:
- `platform`, `jobId`, `jobTitle`, `company`, `location`, `jobUrl`, `applyUrl`
- `description` (HTML stripped and decoded)
- `postedAt`, `scrapedAt`
- `raw` payload retained

#### Glassdoor
**Node:** `Normalise_glassdoor` (Code)
Outputs similar structure; `description` from `job_overview`.

#### Indeed
**Node:** `Normalise_indeed`
> Note: this node is currently empty in the JSON. If you want Indeed fully supported end-to-end, you’ll need to implement the same normalized output fields as LinkedIn/Glassdoor (platform/jobId/jobTitle/company/location/jobUrl/applyUrl/description/postedAt/scrapedAt/raw).

---

### 8) Standardize + generate stable identifiers (uniqueKey)
**Nodes:**
- `Standard_structure_generator` (Set)
- `Strcuture_cleaning_up_block2` (Code)

**What happens**
- Copies the normalized fields into a consistent structure.
- Cleans and clamps fields:
  - platform lowercased
  - trims jobId/company/jobTitle
  - preserves nulls for `jobUrl` (doesn’t stringify null)
  - clamps `description` to 6000 chars and adds `…[TRUNCATED]` if needed
- Ensures `uniqueKey` exists:
  - prefers upstream uniqueKey if present
  - else builds from `platform + jobId`, or `platform + jobUrl`, else a company+title fallback

**Why**
- This `uniqueKey` is the best anchor for:
  - de-duplication
  - stable Notion IDs/search keys later

---

### 9) CV profiles + AI Agent fit scoring
**Nodes:**
- `Set-CV` (Set)
- `AI Agent` (LangChain Agent)
- `OpenAI Chat Model`
- `Output_parser` (Code)

**What happens**
- `Set-CV` injects multiple CV profiles (embedded / robotics / AI / edge AI) as JSON strings.
- AI Agent receives:
  - the job record
  - the CV profiles
  - strict output schema requirements

AI Agent output fields:
- `matchedProfileId` (one of cv_embedded/cv_robotics/cv_ai/cv_edge_ai/none)
- `fitScore` (0–100)
- `decision` (KEEP/MAYBE/SKIP via thresholds)
- evidence lists + reason strings + notion tags

`Output_parser` ensures the agent output is parsed as a JSON object.

---

### 10) Gate: only KEEP/MAYBE goes to Notion
**Nodes:**
- `If4` (decision == KEEP OR MAYBE)
- `Fill_structure_block` (Set)
- `Create a database page` (Notion)

**What happens**
- IF decision is KEEP/MAYBE:
  - Map job fields → Notion properties:
    - Company Name (title)
    - Category (based on matchedProfileId)
    - Link (jobUrl)
    - Platform
    - Job Title
    - Decision
    - Reasons (flattened)
    - Fit Score
    - Date Posted
    - Reminder date = Date Posted + 3 days (fallback to today)
- Then create a Notion DB page in:
  - databaseId: `28ecea8e-cff1-8017-8644-cacaeec0f62d` (“Job Applications Tracker”)

If decision is SKIP:
- It routes back to `Loop over` to continue the batch.

---

### 11) Mark processed email as read
**Node:**
- `Mark a message as read` (Gmail)

**How it is connected**
- After Notion create, workflow returns to `Loop over`, and the **second output** of `Loop over` triggers:
  - mark the email as read
  - platform switch parsing

This means:
- Once an email leads to a Notion create (KEEP/MAYBE), it will later be marked as read.
- For SKIP items, the flow is designed to keep moving; you may want to ensure emails that contain only SKIP jobs are also marked read (depends on your intended behavior).

---

## Configuration / credentials

### Required credentials
- Gmail OAuth2
- Notion API token
- OpenAI API key (through n8n credential)
- Bright Data API token

<!-- ### Security note (important)
Your Bright Data token is present directly in the workflow JSON as a Bearer token inside HTTP Request nodes.
For GitHub repos, replace this with an environment variable or n8n credential reference.

Suggested approach:
- store token in n8n credentials or environment variable (e.g. `BRIGHTDATA_TOKEN`)
- set HTTP header: `Authorization: Bearer {{$env.BRIGHTDATA_TOKEN}}`

---

## Known limitations / TODO
- `Normalise_indeed` is empty → Indeed jobs will not produce the standardized schema for AI scoring + Notion creation until implemented.
- No explicit Notion de-duplication step exists in this JSON. If you want hard de-dup, add:
  - Notion search by `Link` or `uniqueKey` before creating a page
  - Only create if not found

---

## Extension ideas
- Add a Notion “Search” node before “Create a database page” keyed by `uniqueKey` or `Link`.
- Add retry/backoff logic if Bright Data rate limits.
- Store snapshot_id and job IDs for auditing. -->
