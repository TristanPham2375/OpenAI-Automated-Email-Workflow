# OpenAI-Automated-Email-Workflow

# 🏠 AI-Powered Property Management System (n8n)

This project is a smart, automated property management assistant built with **n8n**, using OpenAI API to classify and triage tenant emails, integrate with Google services and uses Google Cloud Platform, and send alerts to the manager for timely action. It’s ideal for landlords and small property managers looking to automate routine communication. I designed it to help my work as a property manager for a housing agency back in highschool.

![Screenshot 2025-06-12 190614](https://github.com/user-attachments/assets/312656b3-499d-49ec-bb9f-fb65e8cb0fc8)

## ⚙️ Features

### 📥 Email Triage (via Gmail)
- Listens to incoming tenant emails using Gmail Trigger.
- Parses sender info, subject, thread ID, and email body.

### 🧠 AI-Powered Classification
- Uses OpenAI or structured output parser to categorize emails into:
  - `Urgent`: Maintenance emergencies (e.g., leaks, lockouts).
  - `House Request`: People asking to view/rent a unit.
  - `Book House Cleaner`: Tenants requesting cleaning.
  - `Other Housing`: Miscellaneous property-related topics.
  - `Irrelevant`: Spam or unrelated emails.
- Extracts structured data (summary, sender, unit, contact info, time).

### 🔀 Switch Routing System
- Directs the email to different automated actions:
  - **Urgent** → Sends alert via Telegram.
  - **House Request** → Logs to Google Sheets, alerts manager, and tracks responses.
  - **Cleaning Request**:
    - Checks if sender is an existing tenant.
    - If yes: Sends confirmation email, waits for reply, then schedules and follows up.
    - If no: Sends rejection message.
  - **Other Housing** → Sends Telegram notification (no Sheets tracking).

### 📊 Google Sheets Integration
- Logs viewing requests with timestamp and follow-up status.
- Sends daily summary via Telegram if there are unaddressed viewing requests.

### 📲 Telegram Alerts
- Alerts property manager instantly for:
  - Urgent maintenance issues.
  - New viewing or cleaning requests.
  - Daily reminders to follow up on pending viewing requests.

# 🏠 Property Manager AI

Automate property management with n8n, OpenAI, Google services, and Telegram. Get real-time alerts, intelligent message parsing, and seamless integration with your workflow.

---

## 📦 Installation & Deployment

### Clone Repository

```bash
git clone https://github.com/your-username/property-manager-ai.git
cd property-manager-ai
```

## Import Workflow into n8n

1. Go to your **n8n** instance.
2. Import `workflow.json` via the UI.

## Set Up Credentials

Configure the following services in your n8n credentials panel:

- 📧 **Gmail**
- 🤖 **Telegram Bot**
- 📊 **Google Sheets**
- 📆 **Google Calendar**
- 🧠 **OpenAI** *(or structured output parser)*

## Update Environment Variables (`.env`)

Set the following variables in your `.env` file:

```env
TELEGRAM_CHAT_ID=your_chat_id
TELEGRAM_BOT_TOKEN=your_bot_token
GOOGLE_SHEET_ID=your_sheet_id
OPENAI_API_KEY=your_openai_api_key  # optional if using OpenAI
```

## 🐳 Host with Docker

This project can be easily hosted using Docker.
Here’s a basic example using Docker Compose:

### 🐳 Example `docker-compose.yml`

```yaml
version: "3"

services:
  n8n:
    image: n8nio/n8n
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=yourpassword
      - TELEGRAM_BOT_TOKEN=${TELEGRAM_BOT_TOKEN}
      - TELEGRAM_CHAT_ID=${TELEGRAM_CHAT_ID}
      - GOOGLE_SHEET_ID=${GOOGLE_SHEET_ID}
      - OPENAI_API_KEY=${OPENAI_API_KEY}
    volumes:
      - ./n8n-data:/home/node/.n8n
```
Start it with:
```bash
docker-compose up -d
```
Then visit http://localhost:5678 to access n8n.

## 🧪 Example Use Case

**Incoming Email:**

> "Hi, I live in Unit 504. There's a leak under the bathroom sink flooding the floor. Please help!"

### 🔄 What Happens:

- 🧠 AI classifies the message as **Urgent**
- 📝 Summary and key details are extracted
- 🚨 A **Telegram alert** is instantly sent to the property manager

---

## 🧠 Ideas for Expansion

- 📲 Add **SMS alerts** using Twilio
- 🏢 Support **multiple properties** or managers
- 💾 Replace Google Sheets with a database (e.g., **Airtable** or **PostgreSQL**)
- 🔁 Sync tenant list dynamically

---

## 📸 Screenshots

Include screenshots of:

- ✅ **n8n Workflow**
- ✅ **Telegram Alerts**
- ✅ **Sample Google Sheets View**

---

## 🤝 Contributions

Pull requests and issues are welcome.  
Let’s automate housing together! 🛠️

---

## 📄 License

**MIT License** — Use freely, but please give credit where due.

---

## ✨ Built With

- [n8n](https://n8n.io)
- [OpenAI](https://openai.com)
- [Google Cloud Platform](https://cloud.google.com)
- [Telegram Bot API](https://core.telegram.org/bots/api)


