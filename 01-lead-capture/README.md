\# 🎯 Exercise 1: Lead Capture System



\## 📌 Description

This workflow receives customer information via Webhook, stores it in Google Sheets, and sends notifications to Telegram.



\## 🔧 Nodes Used

\- Webhook (Trigger)

\- Google Sheets

\- Telegram

\- Respond to Webhook



\## 📸 Workflow Diagram



!\[Workflow Diagram](screenshots/workflow-diagram.png)



\##  How to Use

1\. Import `workflow.json` file in n8n

2\. Configure Google Sheets and Telegram credentials

3\. Activate the workflow

4\. Test with POST request to the Webhook URL



\## 📋 Example Request

```bash

curl -X POST https://your-n8n.com/webhook/lead-capture \\

&#x20; -H "Content-Type: application/json" \\

&#x20; -d '{

&#x20;   "name": "John Doe",

&#x20;   "email": "john@example.com",

&#x20;   "phone": "1234567890",

&#x20;   "message": "Hello, I need help!"

&#x20; }'

