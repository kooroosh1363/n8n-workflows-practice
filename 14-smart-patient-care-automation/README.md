\# Smart Patient Care Automation



\## 📋 Description



A comprehensive healthcare automation system designed for clinics and medical centers. It manages the entire patient journey from appointment booking and AI-powered medical triage to automated time-delayed reminders and post-visit follow-ups, ensuring high patient engagement and reducing no-show rates.



\## 🔧 Nodes Used



\- \*\*Webhook\*\* - Receives appointment requests and follow-up responses

\- \*\*OpenAI GPT-4\*\* - AI medical triage and post-visit symptom analysis

\- \*\*Google Calendar\*\* - Checks availability and creates appointment events

\- \*\*Google Sheets\*\* - Stores appointment records and follow-up logs

\- \*\*Telegram\*\* - Sends confirmation, reminders, and follow-up questionnaires

\- \*\*Wait Node\*\* - Implements time-delayed actions (24h, 2h, 48h delays)

\- \*\*IF Node\*\* - Conditional routing for doctor alerts

\- \*\*Code Node\*\* - Calculates appointment times and processes data



\##  Workflow Diagram



!\[Workflow Diagram](screenshots/workflow-diagram.png)



\## ⚙️ How It Works



\### Phase 1: Appointment Booking \& Triage

1\. \*\*Request Received\*\*: Patient sends an appointment request via Webhook or Telegram.

2\. \*\*AI Triage\*\*: GPT-4 analyzes symptoms to determine urgency level (Emergency, Urgent, Normal) and priority score.

3\. \*\*Scheduling\*\*: System calculates the best appointment time based on urgency and checks Google Calendar.

4\. \*\*Confirmation\*\*: Appointment is saved to the database, added to the clinic's calendar, and a confirmation message is sent to the patient.



\### Phase 2: Automated Reminders

1\. \*\*24-Hour Reminder\*\*: Sent one day before the appointment to reduce no-shows.

2\. \*\*2-Hour Reminder\*\*: Sent two hours before the appointment with location and contact details.



\### Phase 3: Post-Visit Follow-up

1\. \*\*Questionnaire\*\*: 48 hours after the visit, an automated health check questionnaire is sent to the patient.

2\. \*\*Response Analysis\*\*: Patient's response is analyzed by AI to assess symptom improvement and risk level.

3\. \*\*Smart Routing\*\*: 

&#x20;  - If high risk/adverse effects are detected, an immediate alert is sent to the doctor.

&#x20;  - Otherwise, a standard recovery confirmation is sent to the patient.

4\. \*\*Logging\*\*: All follow-up data is securely logged in Google Sheets.



\## 🚀 How to Use



\### Prerequisites



\- n8n instance (self-hosted or cloud)

\- OpenAI API key

\- Google Calendar account

\- Google Sheets account

\- Telegram Bot Token and Chat IDs



\### Setup Steps



1\. \*\*Import Workflow\*\*

&#x20;  - Open n8n and import `workflow.json`.



2\. \*\*Configure Webhooks\*\*

&#x20;  - Copy the production URLs for `Appointment Request Webhook` and `Follow-up Response Webhook`.

&#x20;  - Use these URLs in your frontend form or Telegram bot.



3\. \*\*Configure AI (OpenAI)\*\*

&#x20;  - Connect your OpenAI API credentials to both AI nodes.



4\. \*\*Configure Google Calendar\*\*

&#x20;  - Connect your Google Calendar OAuth2 account.

&#x20;  - Update `YOUR\_GOOGLE\_CALENDAR\_ID` in the "Check Calendar Availability" and "Create Calendar Event" nodes.



5\. \*\*Configure Google Sheets\*\*

&#x20;  - Connect your Google Sheets OAuth2 account.

&#x20;  - Update `YOUR\_GOOGLE\_SHEET\_ID`.

&#x20;  - Create two sheets:

&#x20;    - \*\*"Appointments"\*\*: appointment\_id, patient\_name, patient\_email, patient\_phone, age, symptoms, specialty, urgency\_level, priority\_score, appointment\_time, estimated\_duration, status, created\_at.

&#x20;    - \*\*"FollowUpLog"\*\*: appointment\_id, patient\_name, follow\_up\_response, symptom\_improvement, risk\_level, doctor\_alert\_needed, needs\_follow\_up\_visit, processed\_at.



6\. \*\*Configure Telegram\*\*

&#x20;  - Connect your Telegram Bot API.

&#x20;  - Update `YOUR\_TELEGRAM\_CHAT\_ID` for patient messages.

&#x20;  - Update `YOUR\_DOCTOR\_TELEGRAM\_CHAT\_ID` for medical alerts.



7\. \*\*Activate Workflow\*\*

&#x20;  - Toggle the workflow to "Active" to enable the Webhooks and Wait nodes.



\## 🔐 Credentials Required



\- \*\*OpenAI API\*\*: OpenAI API key

\- \*\*Google Calendar OAuth2\*\*: Google Calendar API access

\- \*\*Google Sheets OAuth2\*\*: Google Sheets API access

\- \*\*Telegram Bot API\*\*: Telegram Bot Token



\## 💡 Use Cases



\- \*\*Private Clinics\*\*: Automate booking and reduce administrative workload.

\- \*\*Hospitals\*\*: Manage high volumes of patient inquiries and follow-ups.

\- \*\*Telemedicine Platforms\*\*: Streamline virtual consultation workflows.

\- \*\*Dental \& Aesthetic Centers\*\*: Reduce appointment cancellations and no-shows.



\## 🔧 Customization Ideas



\- \*\*SMS Integration\*\*: Replace or add Telegram with SMS gateways (Twilio, Kavenegar) for broader reach.

\- \*\*WhatsApp Integration\*\*: Use the WhatsApp Business API for patient communication.

\- \*\*Payment Gateway\*\*: Add a node to collect consultation fees before confirming the appointment.

\- \*\*EHR/EMR Integration\*\*: Connect to electronic health record systems instead of Google Sheets.

\- \*\*Multi-language Support\*\*: Add a language detection node to respond in the patient's preferred language.



\## 📝 Notes



\- \*\*Wait Nodes\*\*: Ensure your n8n instance is configured to handle long-running executions (Wait nodes) properly. If using n8n cloud, it handles this automatically. For self-hosted, ensure the `EXECUTIONS\_MODE` supports waiting.

\- \*\*Privacy\*\*: Ensure compliance with local healthcare data regulations (e.g., HIPAA, GDPR) when storing patient data in Google Sheets.

\- \*\*AI Accuracy\*\*: The AI triage is for administrative prioritization and does not replace professional medical diagnosis.



\## 🐛 Troubleshooting



\*\*Issue\*\*: Wait nodes not resuming

\- \*\*Solution\*\*: Ensure n8n is running in a mode that supports webhooks for wait node resumption (e.g., `production` mode with a proper webhook URL).



\*\*Issue\*\*: Google Calendar events not creating

\- \*\*Solution\*\*: Check if the Calendar ID is correct and the OAuth token has write permissions.



\*\*Issue\*\*: Telegram bot not sending messages

\- \*\*Solution\*\*: Verify the Bot Token and ensure the bot is not blocked by the user. Check Chat IDs.



\## 📄 License



This workflow is provided as-is for educational and commercial use.



\## 🤝 Contributing



Feel free to fork, modify, and improve this workflow for your specific healthcare needs.



\---



\*\*Created for\*\*: n8n-workflows-practice  

\*\*Exercise\*\*: 14 - Smart Patient Care Automation  

\*\*Author\*\*: Koroosh  

\*\*Date\*\*: 2026

