# WhatsApp to Google Drive Workflow Templates

This directory contains n8n workflow templates for the WhatsApp to Google Drive bot.

## Files

- `Whatsapp-drive-template.json` - Main workflow template (clean version without credentials)
- `workflow-setup-guide.md` - Step-by-step setup instructions

## Important Security Note

⚠️ **Never commit workflows with real credentials!**

Before sharing workflows:
1. Export from n8n 
2. Replace all real credentials with placeholders:
   - `YOUR_TWILIO_ACCOUNT_SID`
   - `YOUR_GOOGLE_CLIENT_ID`
   - `YOUR_GEMINI_API_KEY`
3. Remove instance IDs and personal data

## Usage

1. Import the template into your n8n instance
2. Configure your actual credentials in n8n
3. Update webhook URLs and endpoints
4. Test with your WhatsApp sandbox
5. Activate the workflow

## Credentials Required

- Twilio Account (WhatsApp Sandbox)
- Google Drive API (OAuth2)
- Google Gemini API
- n8n basic auth

See the main README.md for detailed setup instructions.
