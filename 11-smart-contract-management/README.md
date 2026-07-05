\# Smart Contract Management System



\## 📋 Description



An intelligent contract management and legal automation system that automatically processes incoming contracts via email, extracts key clauses using AI, assesses risk levels, and routes contracts to the appropriate teams (Legal, Finance, or Sales) based on risk assessment.



\## 🔧 Nodes Used



\- \*\*Email Trigger (IMAP)\*\* - Monitors inbox for new contract emails

\- \*\*Google Drive\*\* - Stores contract documents

\- \*\*OpenAI GPT-4\*\* - Analyzes contracts and extracts key information

\- \*\*Code Node\*\* - Processes AI responses and calculates risk scores

\- \*\*Switch Node\*\* - Routes contracts based on risk level

\- \*\*Slack\*\* - Alerts legal team for high-risk contracts

\- \*\*Email Send\*\* - Notifies finance and sales teams

\- \*\*Google Sheets\*\* - Logs all processed contracts



\## 🔄 Workflow Diagram



!\[Workflow Diagram](screenshots/workflow-diagram.png)



\## ⚙️ How It Works



1\. \*\*Email Monitoring\*\*: System continuously monitors a designated email inbox for new contract emails

2\. \*\*Document Storage\*\*: Automatically saves contract attachments to Google Drive

3\. \*\*AI Analysis\*\*: Uses GPT-4 to analyze contract text and extract:

&#x20;  - Parties involved

&#x20;  - Effective and expiration dates

&#x20;  - Payment terms and financial obligations

&#x20;  - Termination and penalty clauses

&#x20;  - Risk factors and compliance issues

4\. \*\*Risk Assessment\*\*: Calculates an overall risk score (0-100) and categorizes as:

&#x20;  - \*\*High Risk\*\* (70-100): Routes to Legal Team via Slack

&#x20;  - \*\*Medium Risk\*\* (40-69): Routes to Finance Team via Email

&#x20;  - \*\*Low Risk\*\* (0-39): Routes to Sales Team via Email

5\. \*\*Logging\*\*: All processed contracts are logged in Google Sheets with full details

6\. \*\*Notification\*\*: Appropriate teams receive detailed notifications with contract summaries and risk assessments



\## 🚀 How to Use



\### Prerequisites



\- n8n instance (self-hosted or cloud)

\- Email account with IMAP access

\- Google Drive account

\- Google Sheets account

\- OpenAI API key

\- Slack workspace (optional)



\### Setup Steps



1\. \*\*Import Workflow\*\*

&#x20;  - Open n8n

&#x20;  - Click "Import from File"

&#x20;  - Select `workflow.json`



2\. \*\*Configure Email Trigger\*\*

&#x20;  - Set your email credentials (IMAP server, username, password)

&#x20;  - Update subject filter if needed (default: "New Contract")



3\. \*\*Configure Google Drive\*\*

&#x20;  - Connect your Google Drive account

&#x20;  - Update `YOUR\_GOOGLE\_DRIVE\_ID` with your Drive ID

&#x20;  - Update `YOUR\_CONTRACTS\_FOLDER\_ID` with target folder ID



4\. \*\*Configure OpenAI\*\*

&#x20;  - Add your OpenAI API credentials

&#x20;  - Model is set to GPT-4 (can be changed)



5\. \*\*Configure Google Sheets\*\*

&#x20;  - Connect your Google Sheets account

&#x20;  - Update `YOUR\_GOOGLE\_SHEET\_ID` with your sheet ID

&#x20;  - Create a sheet named "ContractsLog" with columns:

&#x20;    - contract\_id

&#x20;    - file\_name

&#x20;    - received\_at

&#x20;    - parties

&#x20;    - effective\_date

&#x20;    - expiration\_date

&#x20;    - risk\_score

&#x20;    - risk\_level

&#x20;    - recommended\_action

&#x20;    - route\_to

&#x20;    - drive\_url

&#x20;    - processed\_at



6\. \*\*Configure Slack (Optional)\*\*

&#x20;  - Connect your Slack account

&#x20;  - Update channel name (default: #legal-alerts)



7\. \*\*Configure Email Notifications\*\*

&#x20;  - Update email addresses in the email nodes:

&#x20;    - finance@yourcompany.com

&#x20;    - sales@yourcompany.com

&#x20;  - Update sender email (default: contracts@yourcompany.com)



8\. \*\*Activate Workflow\*\*

&#x20;  - Toggle the workflow to "Active"

&#x20;  - Test by sending a contract email to your monitored inbox



\## 🔐 Credentials Required



\- \*\*IMAP Email\*\*: Email server credentials

\- \*\*Google Drive OAuth2\*\*: Google Drive API access

\- \*\*Google Sheets OAuth2\*\*: Google Sheets API access

\- \*\*OpenAI API\*\*: OpenAI API key

\- \*\*SMTP Email\*\*: Email sending credentials

\- \*\*Slack API\*\*: Slack bot token (optional)



\## 📊 Risk Scoring Logic



The system uses the following risk assessment criteria:



\- \*\*High Risk (70-100)\*\*:

&#x20; - Unusual payment terms

&#x20; - Excessive penalties

&#x20; - Compliance concerns

&#x20; - Unclear termination clauses

&#x20; - Multiple risk factors identified



\- \*\*Medium Risk (40-69)\*\*:

&#x20; - Non-standard payment terms

&#x20; - Moderate financial obligations

&#x20; - Some compliance considerations

&#x20; - Standard but complex clauses



\- \*\*Low Risk (0-39)\*\*:

&#x20; - Standard payment terms

&#x20; - Clear obligations

&#x20; - No compliance issues

&#x20; - Standard contract language



\## 💡 Use Cases



\- \*\*Legal Departments\*\*: Automate initial contract review and risk assessment

\- \*\*Procurement Teams\*\*: Streamline vendor contract processing

\- \*\*Sales Operations\*\*: Quick assessment of customer contracts

\- \*\*Compliance Teams\*\*: Flag contracts with potential compliance issues

\- \*\*Executive Management\*\*: Get instant visibility into contract risk exposure



\## 🔧 Customization Ideas



\- Add integration with DocuSign for digital signatures

\- Implement automatic contract renewal reminders

\- Add multi-language support for international contracts

\- Create a dashboard for contract analytics

\- Integrate with CRM systems (Salesforce, HubSpot)

\- Add automated clause comparison with standard templates



\## 📝 Notes



\- The AI analysis quality depends on the contract text clarity

\- For very long contracts, consider splitting into sections

\- Risk scoring thresholds can be adjusted in the Code Node

\- Email templates can be customized for your organization

\- Consider adding error handling for failed AI analyses



\## 🐛 Troubleshooting



\*\*Issue\*\*: Email trigger not working

\- \*\*Solution\*\*: Verify IMAP credentials and ensure "Less secure app access" is enabled



\*\*Issue\*\*: AI analysis returning errors

\- \*\*Solution\*\*: Check OpenAI API key and ensure contract text is readable



\*\*Issue\*\*: Google Drive upload failing

\- \*\*Solution\*\*: Verify folder permissions and Drive API access



\*\*Issue\*\*: Risk score seems incorrect

\- \*\*Solution\*\*: Adjust the scoring logic in the Code Node



\## 📄 License



This workflow is provided as-is for educational and commercial use.



\## 🤝 Contributing



Feel free to fork, modify, and improve this workflow for your specific needs.



\---



\*\*Created for\*\*: n8n-workflows-practice  

\*\*Exercise\*\*: 11 - Smart Contract Management  

\*\*Author\*\*: Koroosh  

\*\*Date\*\*: 2026

