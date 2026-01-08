# Email Parser Workflow Template

## 📋 About This Template

This is a **sanitized version** of the `Email_parser.json` n8n workflow with all sensitive credentials replaced by placeholders.

**✅ This template contains:**
- Complete workflow structure with all nodes
- All workflow logic and code
- Configuration settings
- Node connections and flow

**🔒 Sensitive data removed:**
- ❌ OpenAI credential IDs
- ❌ Gmail OAuth2 credential IDs
- ❌ Notion API credential IDs
- ❌ Bright Data Bearer tokens
- ❌ Notion database IDs
- ❌ Workflow instance IDs

## 🔄 Placeholders Used

The following placeholders replace real credentials:

| Placeholder | What to Replace | Occurrences |
|-------------|----------------|-------------|
| `YOUR_OPENAI_CREDENTIAL_ID` | Your n8n OpenAI credential ID | 1 |
| `YOUR_GMAIL_CREDENTIAL_ID` | Your n8n Gmail OAuth2 credential ID | 2 |
| `YOUR_NOTION_CREDENTIAL_ID` | Your n8n Notion API credential ID | 1 |
| `YOUR_BRIGHTDATA_API_TOKEN` | Your Bright Data Bearer token | 9 |
| `YOUR_NOTION_DATABASE_ID` | Your Notion database ID | 1 |
| `WORKFLOW_ID_WILL_BE_GENERATED` | n8n will auto-generate this on import | 1 |

## 📥 How to Use This Template

### Step 1: Set Up Credentials in n8n

Before importing, create these credentials in your n8n instance:

1. **OpenAI API** (`openAiApi`)
   - Add your OpenAI API key
   - Note the credential ID from n8n

2. **Gmail OAuth2** (`gmailOAuth2`)
   - Set up Gmail OAuth2
   - Note the credential ID from n8n

3. **Notion API** (`notionApi`)
   - Add your Notion Integration token
   - Note the credential ID from n8n

### Step 2: Get Your Bright Data Token

1. Log in to Bright Data dashboard
2. Go to API settings
3. Copy your Bearer token

### Step 3: Prepare the Template

1. Make a copy of `Email_parser.template.json`
2. Replace all placeholders:

   ```bash
   # Example using sed (macOS/Linux)
   sed -i '' 's/YOUR_OPENAI_CREDENTIAL_ID/abc123xyz/g' Email_parser.template.json
   sed -i '' 's/YOUR_GMAIL_CREDENTIAL_ID/def456uvw/g' Email_parser.template.json
   sed -i '' 's/YOUR_NOTION_CREDENTIAL_ID/ghi789rst/g' Email_parser.template.json
   sed -i '' 's/YOUR_BRIGHTDATA_API_TOKEN/your_actual_token_here/g' Email_parser.template.json
   sed -i '' 's/YOUR_NOTION_DATABASE_ID/your_database_id/g' Email_parser.template.json
   ```

   Or manually find and replace in your text editor.

### Step 4: Optional Configurations

You may also want to update:

- **Gmail Label ID** (line ~416): Currently `Label_8163444995902261724`
- **Bright Data Dataset IDs**: 
  - LinkedIn: `gd_lpfll7v5hcqtkxl6l`
  - Glassdoor: `gd_lpfbbndm1xnopbrcr0`
  - Indeed: `gd_l4dx9j9sscpvs7no2`
- **Webhook IDs**: n8n will regenerate these on import

### Step 5: Import to n8n

1. Go to your n8n instance
2. Click "Import from File" or "Import from URL"
3. Select your prepared JSON file
4. Verify all nodes are connected correctly
5. Test the workflow with a sample date

## 🔍 Verification Checklist

Before activating the workflow, verify:

- [ ] All credential IDs are replaced with your actual n8n credential IDs
- [ ] Bright Data Bearer token is updated in all 9 HTTP Request nodes
- [ ] Notion database ID points to your database
- [ ] Gmail label ID is correct
- [ ] Test run completes successfully
- [ ] Jobs appear in your Notion database

## 🚨 Security Warning

**⚠️ NEVER commit your configured workflow file to version control!**

- ✅ Use this template for sharing
- ✅ Keep your actual `Email_parser.json` (with real credentials) local only
- ✅ Add `Email_parser.json` to `.gitignore`
- ❌ Don't share your configured file with credentials

## 📚 Additional Resources

- [Complete Setup Guide](../SETUP.md)
- [Security Summary](../SECURITY_SUMMARY.md)
- [Project README](../readme.md)

## 🔧 Structure Overview

This workflow contains **35 nodes** organized in these main sections:

1. **Email Fetching** (Webhooks + Gmail nodes)
2. **Platform Detection** (Switch node for LinkedIn/Glassdoor/Indeed)
3. **Email Parsing** (JavaScript code nodes per platform)
4. **URL Cleaning** (Normalization for Bright Data)
5. **Bright Data Scraping** (HTTP Request + Wait + Status Check)
6. **Data Normalization** (Standardize across platforms)
7. **AI Scoring** (OpenAI Agent with CV matching)
8. **Decision Filter** (KEEP/MAYBE/SKIP)
9. **Notion Integration** (Create database pages)
10. **Batch Processing** (Loop and mark emails as read)

## 💡 Tips

- **Start simple**: Test with just LinkedIn first
- **Monitor usage**: Check your Bright Data credits
- **Adjust prompts**: Modify the AI Agent prompt for your needs
- **Batch size**: Adjust the "Split in Batches" node if needed
- **Wait times**: Increase if Bright Data needs more time to scrape

---

**Last Updated:** January 8, 2026  
**Template Version:** 1.0  
**Compatible with:** n8n v1.0+
