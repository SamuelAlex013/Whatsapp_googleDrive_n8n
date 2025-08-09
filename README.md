# WhatsApp to Google Drive Bot with n8n

A powerful WhatsApp bot that manages Google Drive files through simple text commands. Built with n8n workflow automation, featuring AI-powered document summarization and comprehensive audit logging.

## 🚀 Features

- **📱 WhatsApp Integration**: Control Google Drive through WhatsApp messages via Twilio
- **📁 File Management**: List, delete, move files and folders with simple commands
- **🤖 AI Summarization**: Get concise summaries of PDF, DOCX, and TXT files using Google Gemini
- **🐳 Docker Deployment**: Easy setup with Docker Compose

## 🗂️ Project Structure

```
whatsapp_drive_bot/
├── workflows/
│   └── Drive-whatsapp.json          # Alternative Drive→WhatsApp workflow
├── n8n_data/                        # Persistent n8n data and executions
├── .env                             # Environment configuration
├── docker-compose.yml               # Docker services 
└── README.md                        # This documentation
```

## ⚙️ Setup Instructions

### 1. Prerequisites
- Docker and Docker Compose installed
- Twilio account with WhatsApp Sandbox
- Google Drive API credentials
- Google Gemini API key (for AI summarization)
- ngrok for local tunneling (development)

### 2. Twilio WhatsApp Setup
1. **Create Twilio Account**: https://console.twilio.com/
2. **Enable WhatsApp Sandbox**: Console → Messaging → Try it out → Send a WhatsApp message
3. **Get Credentials**: Account SID and Auth Token from Console
4. **Configure Webhook**: Point to your ngrok webhook URL (see step 5)

### 3. Google Drive API Setup
1. **Google Cloud Console**: https://console.cloud.google.com/
2. **Enable Drive API**: APIs & Services → Library → Google Drive API → Enable
3. **Create OAuth2 Credentials**: Credentials → Create → OAuth 2.0 Client ID
4. **Configure Consent Screen**: Add necessary scopes for Drive access
5. **Add Redirect URI**: `http://localhost:5678/rest/oauth2-credential/callback`

### 4. Google Gemini API Setup
1. **Google AI Studio**: https://aistudio.google.com/app/apikey
2. **Create API Key**: Free tier available with generous limits
3. **Copy the key** for environment configuration

### 5. Environment Configuration
Create `.env` file in project root:
```env
# n8n Configuration
N8N_BASIC_AUTH_USER=admin
N8N_BASIC_AUTH_PASSWORD=securepass123
N8N_WEBHOOK_TUNNEL_URL=https://your-ngrok-url.ngrok-free.app
N8N_HOST=localhost
TIMEZONE=Asia/Kolkata


# Twilio Configuration
TWILIO_ACCOUNT_SID=your_account_sid
TWILIO_AUTH_TOKEN=your_auth_token

# Google APIs
GOOGLE_CLIENT_ID=your_client_id.apps.googleusercontent.com
GOOGLE_CLIENT_SECRET=your_client_secret
GEMINI_API_KEY=your_gemini_api_key

```

### 6. Deploy with Docker
```bash
# Clone the repository
git clone <repository-url>
cd whatsapp_drive_bot

# Start services
docker-compose up -d

# Access n8n interface
open http://localhost:5678
```

### 7. Import Workflow
1. Open n8n at `http://localhost:5678`
2. Login with credentials from `.env`
3. Import `workflows/Whatsapp-drive.json`
4. Configure credentials:
   - Google Drive OAuth2
   - Google Gemini API
   - Twilio Account
5. Activate the workflow

### 8. Setup ngrok Tunnel (Development)
```bash
# Install ngrok: https://ngrok.com/download
ngrok http 5678

# Copy the HTTPS URL to .env as N8N_WEBHOOK_TUNNEL_URL
# Update Twilio webhook URL to: https://your-url.ngrok-free.app/webhook/whatsapp
```

## 📱 Command Syntax

### File Listing
```
LIST /ProjectX              # List files in ProjectX folder
LIST /                      # List files in root Drive
```

### File Deletion
```
DELETE /ProjectX/report.pdf
# Bot responds with confirmation prompt
CONFIRM DELETE              # Required confirmation
```

### File Moving
```
MOVE /ProjectX/report.pdf /Archive
# Moves report.pdf from ProjectX to Archive folder
```

### AI Document Summarization
```
SUMMARY /ProjectX/report.pdf     # Summarize specific file
SUMMARY /ProjectX                # Summarize all supported files in folder
```

## 🔧 Supported File Types

- **📄 PDF**: Text extraction and AI summarization
- **📝 DOCX**: Microsoft Word documents
- **📃 TXT**: Plain text files


## 🤖 AI Integration

The bot uses **Google Gemini** for document summarization:
- Supports multiple file formats (PDF, DOCX, TXT)
- Intelligent text extraction and processing
- Concise, actionable summaries
- Handles large documents efficiently


### Common Issues

1. **"Insufficient quota" errors**
   - ✅ Using Gemini instead of OpenAI (higher free limits)
   - Check API billing settings in Google AI Studio

2. **WhatsApp webhook not receiving**
   - Verify ngrok tunnel is active: `ngrok http 5678`
   - Check Twilio webhook configuration points to correct URL
   - Ensure n8n workflow is activated

3. **Google Drive access denied**
   - Refresh OAuth2 tokens in n8n credentials
   - Verify API permissions and scopes
   - Check redirect URI configuration

4. **Docker issues**
   - Ensure ports 5678 are available
   - Check Docker logs: `docker-compose logs -f`
   - Verify .env file is properly configured




## 🏆 Acknowledgments

- **n8n**: Powerful workflow automation platform
- **Twilio**: Reliable WhatsApp API integration
- **Google**: Drive API and Gemini AI services
- **Docker**: Containerization and deployment

---