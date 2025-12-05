# 📬 Contact Form Workflow (n8n)

This repository contains my n8n workflow for a website contact form.  
The workflow receives submitted form data, validates the fields through a Code node, and sends a formatted message to Telegram.

---

## 🚀 Features

- Receives form submissions through a **POST Webhook**
- Validates required fields:
  - name  
  - email  
  - message  
- Builds a clean and readable notification string
- Sends the final message to Telegram

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
