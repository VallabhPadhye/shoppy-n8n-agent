# 🤖 Shoppy n8n Agent

An intelligent shopping automation agent built with n8n, powered by Google Gemini 3.5 Turbo, and integrated with Telegram, Google Sheets, and email automation. Shoppy assists users in product discovery, quotations, and information sharing while automatically logging all interactions for analytics and marketing insights.

---

## ✨ Features

### 🧠 AI-Powered Conversations
- Leverages **Google Gemini 3.5 Turbo** for smart, contextual shopping conversations
- Understands user preferences, interests, and intent
- Provides personalized product recommendations

### 💬 Telegram Bot Integration
- Seamless integration with Telegram via BotFather
- Responds to `/start`, `/help`, and shopping queries
- Handles conversation flows including product inquiries, interest tracking, and personal info collection

### 📊 Automated Google Sheets Logging
Logs every user interaction for marketing and behavioral analysis:

| Field | Description |
|-------|-------------|
| **Username** | Telegram username or display name |
| **Product** | Product discussed or requested |
| **Additional Comment** | User's extra notes or custom requests |
| **Conversation Type** | Categorized as Product, Interest, or Personal Info |
| **Timestamp** | When the conversation occurred |
| **Bot Response** | Agent's reply to the user |

### ✉️ Email Automation
- Sends detailed quotation emails and product information
- SMTP-based integration (supports ProtonMail, Gmail, etc.)
- Professional email templates for quotations and confirmations

### 🐳 Dockerized Deployment
- Fully containerized setup for easy deployment
- Isolated environment with Docker Compose

### 🌐 Secure Webhooks
- Uses ngrok tunnels for secure HTTPS connections
- Safely connects Telegram webhooks to local n8n workflows

---

## 🏗️ Architecture

```
User (Telegram)
    ↓
Telegram Bot (BotFather)
    ↓
n8n Workflows
 ├── Gemini 1.5 Turbo (AI Conversations)
 ├── Google Sheets (Log conversations)
 ├── Email Node (Send quotations)
 └── Webhook via ngrok (Secure HTTPS tunnel)
```

---

## 🚀 Quick Start

### Prerequisites

- Docker and Docker Compose
- Telegram Bot Token (from BotFather)
- Google Cloud API Key (for Gemini)
- ngrok account (for webhook tunneling)
- Google Sheets API credentials
- Gmail API credentials

### 1. Clone the Repository

```bash
git clone https://github.com/vallabhpadhye/shoppy-n8n-agent.git
cd shoppy-n8n-agent
```

### 2. Configure Environment Variables

Create a `.env` file in the project root:

```env
# n8n Configuration
N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=admin
N8N_BASIC_AUTH_PASSWORD=yourpassword

# Telegram Bot
TELEGRAM_BOT_TOKEN=your_botfather_token

# ngrok
NGROK_AUTH_TOKEN=your_ngrok_token

# Google Sheets
GOOGLE_SHEET_ID=your_google_sheet_id

# Google AI
GEMINI_API_KEY=your_google_ai_api_key
```

### 3. Start with Docker

```bash
docker-compose up -d
```

### 4. Configure ngrok Tunnel

```bash
ngrok http 5678
```

Copy the `https` URL provided by ngrok and set it as your Telegram webhook URL in n8n.

### 5. Import Workflows

1. Open n8n at `http://localhost:5678`
2. Log in with your credentials
3. Import `workflows/shoppy_agent.json`
4. Connect nodes for Google Sheets, Email, and Gemini
5. Activate your workflow

---

## 📊 Google Sheets Structure

Your Google Sheet should have the following columns:

| Timestamp | Username | Product | Additional Comment | Conversation Type | Bot Response |
|-----------|----------|---------|-------------------|------------------|--------------|
| 2025-10-04 13:20 | @user123 | iPhone 16 | Asking for color variants | Product | Shared product details |
| 2025-10-04 13:25 | @rajat | Samsung TV | Interested in exchange offer | Interest | Sent quotation email |

> **Tip:** Use this data to identify user preferences, evaluate product interest, and fine-tune marketing strategies.

---

## 📧 Email Automation Flow

1. Bot detects quotation or product detail request
2. Collects necessary product info and user email
3. Composes professional quotation email
4. Sends via configured gmail account.
5. Logs interaction in Google Sheets

---

## 📁 Project Structure

```
shoppy-n8n-agent/
├── workflows/
│   └── shoppy_agent.json
├── docker-compose.yml
├── .env.example
├── README.md
└── logs/
    └── user_conversations.log
```

---

## 🔐 Security

- **Authentication:** Protected with n8n basic authentication
- **Credentials:** All sensitive data managed via environment variables
- **Data Protection:** Google Sheet logs are sanitized and secured
- **Encryption:** ngrok provides end-to-end encryption for webhook calls

---

## 🛠️ Configuration

### Telegram Bot Setup

1. Open Telegram and search for [@BotFather](https://t.me/botfather)
2. Send `/newbot` and follow the instructions
3. Copy the bot token and add it to your `.env` file

### Google Sheets API

1. Create a new Google Sheet
2. Enable Google Sheets API in Google Cloud Console
3. Create service account credentials
4. Share your sheet with the service account email
5. Copy the sheet ID from the URL

### ngrok Setup

1. Sign up at [ngrok.com](https://ngrok.com)
2. Get your auth token from the dashboard
3. Add it to your `.env` file

---

## 🔮 Future Enhancements

- [ ] Auto-categorization of conversation types using AI
- [ ] Product recommendation system based on user history
- [ ] PDF quotation generation with dynamic templates
- [ ] Admin dashboard for conversation insights
- [ ] Multi-language support
- [ ] Payment gateway integration
- [ ] Order tracking system

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- [n8n](https://n8n.io/) - Workflow automation platform
- [Google Gemini](https://deepmind.google/technologies/gemini/) - AI model
- [Telegram](https://telegram.org/) - Messaging platform
- [ngrok](https://ngrok.com/) - Secure tunneling service

---

**Built with ❤️ n8n, gemini & ngroq.**
