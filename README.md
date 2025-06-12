# OpenAI-Automated-Email-Workflow

# 🏠 AI-Powered Property Management System (n8n)

This project is a smart, automated property management assistant built with **n8n**, using OpenAI API to classify and triage tenant emails, integrate with Google services, and send alerts to the manager for timely action. It’s ideal for landlords and small property managers looking to automate routine communication. I designed it to help my work as a property manager for a housing agency back in highschool. 

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

---

## 📂 Files to Include in Repository

```text
/README.md               ← You’re reading it now
/workflow.json           ← Exported n8n workflow
/example_emails.md       ← Example email inputs used during testing
/assets/                 ← Screenshots or Telegram/email examples (optional)
.env.example             ← Environment variable template for API keys, emails

