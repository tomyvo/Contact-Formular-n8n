# 📬 Contact Form Workflow (n8n)

This repository contains my n8n workflow for a website contact form.  
The workflow receives submitted form data, validates the fields through a Code node, and sends a formatted message to Telegram:
<p align="center"> <img src="https://img.shields.io/badge/n8n-Workflow-orange?style=for-the-badge" /> <img src="https://img.shields.io/badge/Automation-Active-brightgreen?style=for-the-badge" /> <img src="https://img.shields.io/badge/Telegram-Notifications-26A5E4?style=for-the-badge" /> </p>

---

## 🚀 Features

✨ Webhook-based contact form handler
✨ JavaScript validation for name, email, message
✨ Readable message formatting
✨ Instant Telegram notification
✨ Simple to deploy on any n8n instance
✨ 100% safe — no credentials stored in repo

---

## 📥 Importing the Workflow

To use this workflow in your own n8n instance:

1. Open n8n  
2. Click **Import from File**  
3. Select the file:



---

## 📁 Workflow Structure

### 1. **Webhook Node**
- Method: `POST`
- Expects the following fields in the request body:
  - `name`
  - `email`
  - `message`
  - `subject` (optional)

### 2. **Code Node (JavaScript)**  
Validates the incoming data and builds a formatted message:

```js
const input = $json.body;

const requiredFields = ["name", "email", "message"];

for (const field of requiredFields) {
    if (!input[field] || input[field].trim() === "") {
        throw new Error(`Field ${field} is missing!`);
    }
}

const notification =
`New contact form message:

Name: ${input.name}
Email: ${input.email}
Subject: ${input.subject || "(no subject)"}

Message:
${input.message}`;

return [{
    json: {
        notification,
        ...input
    }
}];
