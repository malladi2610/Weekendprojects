# Setup Guide for n8n Gmail AI Agent

## Overview
This workflow automates job application tracking by parsing emails from LinkedIn, Glassdoor, and Indeed, matching them against your CV profiles using AI, and adding qualified jobs to Notion.

## Prerequisites

- n8n instance (self-hosted or cloud)
- Gmail account
- OpenAI API account
- Notion account with a Job Applications database
- Bright Data account (for web scraping)

## Required Credentials

You'll need to set up the following credentials in n8n:

### 1. OpenAI API
- Type: `openAiApi`
- Required: API Key from OpenAI

### 2. Gmail OAuth2
- Type: `gmailOAuth2`
- Required: Gmail OAuth2 credentials
- Scopes needed:
  - Read emails
  - Modify emails (mark as read)
  - Access specific labels

### 3. Notion API
- Type: `notionApi`
- Required: Notion Integration Token
- Database required with these properties:
  - Company Name (title)
  - Category (select)
  - Link (url)
  - Platform (select)
  - Job Title (rich_text)
  - Decision (select)
  - Reasons (rich_text)
  - Fit Score (number)
  - Reminder data (date)
  - Date Posted (date)

### 4. Bright Data API Token
- Get your Bearer token from Bright Data dashboard
- This is used in HTTP request headers

## Installation Steps

### Step 1: Set up Gmail Filter

Create a Gmail filter/label:
1. Go to Gmail Settings → Filters and Blocked Addresses
2. Create a new filter for job emails from:
   - `jobs-noreply@linkedin.com`
   - `jobalerts-noreply@linkedin.com`
   - `jobs-listings@linkedin.com`
   - `noreply@glassdoor.com`
   - `alert@indeed.com`
3. Label these emails (note the Label ID for configuration)

### Step 2: Prepare Your CV Profiles

The workflow uses 4 CV profiles stored as JSON in the workflow:
- `cv_embedded` - Embedded Systems profile
- `cv_robotics` - Robotics profile
- `cv_ai` - AI Software Engineering profile
- `cv_edge_ai` - Edge AI profile

Update these in the `Set-CV` node with your own profile details.

### Step 3: Configure n8n Credentials

1. In your n8n instance, go to Credentials
2. Add credentials for:
   - OpenAI API
   - Gmail OAuth2
   - Notion API
3. Note down the credential IDs (they look like: `fhRdPB2DP1IUBxx0`)

### Step 4: Import Workflow

The workflow is provided as a template file with placeholders for security.

**Using the Template:**

1. Copy `n8n_pipeline/Email_parser.template.json` to a new file
2. Replace all placeholders with your actual credentials:
   - `YOUR_OPENAI_CREDENTIAL_ID` → Your OpenAI credential ID from n8n
   - `YOUR_GMAIL_CREDENTIAL_ID` → Your Gmail credential ID from n8n  
   - `YOUR_NOTION_CREDENTIAL_ID` → Your Notion credential ID from n8n
   - `YOUR_BRIGHTDATA_API_TOKEN` → Your Bright Data Bearer token (9 occurrences)
   - `YOUR_NOTION_DATABASE_ID` → Your Notion database ID

   **Quick replace using command line:**
   ```bash
   cd n8n_pipeline
   cp Email_parser.template.json my_workflow.json
   
   # Replace with your actual values
   sed -i '' 's/YOUR_OPENAI_CREDENTIAL_ID/abc123/g' my_workflow.json
   sed -i '' 's/YOUR_GMAIL_CREDENTIAL_ID/xyz789/g' my_workflow.json
   sed -i '' 's/YOUR_NOTION_CREDENTIAL_ID/def456/g' my_workflow.json
   sed -i '' 's/YOUR_BRIGHTDATA_API_TOKEN/your_token_here/g' my_workflow.json
   sed -i '' 's/YOUR_NOTION_DATABASE_ID/28ecea8e.../g' my_workflow.json
   ```

3. Import `my_workflow.json` into your n8n instance
4. **Delete** `my_workflow.json` after import (don't commit it!)

**Optional configurations:**
- Gmail Label ID (if different from default)
- Bright Data dataset IDs for LinkedIn/Glassdoor/Indeed
- Update CV profiles in the `Set-CV` node

### Step 5: Configure Bright Data

The template includes placeholder dataset IDs. Update if needed:
- LinkedIn dataset: `gd_lpfll7v5hcqtkxl6l`
- Glassdoor dataset: `gd_lpfbbndm1xnopbrcr0`
- Indeed dataset: `gd_l4dx9j9sscpvs7no2`

Bearer token should already be replaced in Step 4.

### Step 6: Test the Workflow

1. Use the webhook endpoint to trigger the workflow manually
2. Check that emails are being processed
3. Verify jobs are being added to Notion

## Security Best Practices

### What's Protected

✅ The actual workflow JSON file is gitignored  
✅ All API tokens and bearer tokens are kept out of version control  
✅ Credential IDs are not committed  

### Important Notes

⚠️ **Never commit:**
- `n8n_pipeline/Email_parser.json` (actual workflow with credentials)
- Any files containing API keys or tokens
- `.env` files with secrets

✅ **Safe to commit:**
- `Email_parser.template.json` (this template)
- Documentation files
- CV profile structures (if you want to share your format)

### If You've Already Pushed Credentials

If you've accidentally pushed credentials to GitHub:

1. **Immediately rotate all exposed credentials:**
   - Regenerate OpenAI API key
   - Regenerate Bright Data Bearer token
   - Regenerate Notion Integration token
   - Revoke and recreate Gmail OAuth credentials

2. **Remove from Git history:**
   ```bash
   git filter-branch --force --index-filter \
     "git rm --cached --ignore-unmatch n8n_pipeline/Email_parser.json" \
     --prune-empty --tag-name-filter cat -- --all
   
   git push origin --force --all
   ```

3. **Verify removal:**
   - Check your GitHub repository
   - Verify the file is in `.gitignore`

## Workflow Architecture

```
Email Trigger (Webhook)
    ↓
Gmail Fetch & Parse
    ↓
Platform Segregation (LinkedIn/Glassdoor/Indeed)
    ↓
URL Cleaning & Normalization
    ↓
Bright Data Scraping
    ↓
Job Data Normalization
    ↓
AI Matching (Against CV Profiles)
    ↓
Decision Filter (KEEP/MAYBE/SKIP)
    ↓
Notion Database Update
```

## Troubleshooting

### Common Issues

1. **Workflow fails at credential validation**
   - Verify all credential IDs are correct
   - Check that credentials have proper scopes/permissions

2. **Bright Data requests timeout**
   - Increase wait time in Wait nodes
   - Check Bright Data API limits

3. **AI Agent returns incorrect format**
   - Verify OpenAI model availability
   - Check prompt structure in AI Agent node

4. **Jobs not appearing in Notion**
   - Verify Notion database ID
   - Check database property names match exactly
   - Ensure Notion integration has access to the database

## Contributing

When contributing to this project:
- Never include actual credentials
- Always use placeholders in templates
- Document any new credential requirements
- Update this SETUP.md with configuration changes

## Support

For issues related to:
- **n8n**: Check [n8n documentation](https://docs.n8n.io/)
- **Bright Data**: Check [Bright Data docs](https://docs.brightdata.com/)
- **OpenAI API**: Check [OpenAI documentation](https://platform.openai.com/docs)
