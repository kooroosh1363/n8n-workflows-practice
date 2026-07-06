\# Invoice Processing Automation System



\## 📋 Description



An intelligent invoice processing and financial automation system that automatically receives invoices via email, extracts key information using OCR and AI, matches invoices with purchase orders, routes for approval based on matching accuracy, and sends automated payment reminders based on due dates.



\## 🔧 Nodes Used



\- \*\*Email Trigger (IMAP)\*\* - Monitors inbox for new invoice emails

\- \*\*Google Drive\*\* - Stores invoice documents

\- \*\*OpenAI GPT-4 Vision\*\* - OCR and invoice data extraction

\- \*\*Google Sheets\*\* - Purchase Orders database, Invoice logging

\- \*\*Code Node\*\* - Data matching, validation, and payment date checking

\- \*\*Switch Node\*\* - Routes invoices based on approval requirements

\- \*\*Email Send\*\* - Approval requests and payment reminders

\- \*\*Slack\*\* - Auto-approval notifications

\- \*\*Schedule Trigger\*\* - Daily payment due date checking



\## 🔄 Workflow Diagram



!\[Workflow Diagram](screenshots/workflow-diagram.png)



\## ⚙️ How It Works



\### Main Invoice Processing Flow:

1\. \*\*Email Monitoring\*\*: System continuously monitors inbox for invoice emails

2\. \*\*Document Storage\*\*: Automatically saves invoice attachments to Google Drive

3\. \*\*OCR \& AI Extraction\*\*: Uses GPT-4 Vision to extract:

&#x20;  - Invoice number, dates, vendor information

&#x20;  - Line items, quantities, unit prices

&#x20;  - Subtotal, tax, total amount

&#x20;  - Payment terms and PO number

&#x20;  - Confidence score for extraction accuracy

4\. \*\*Purchase Order Matching\*\*: Compares invoice with POs in Google Sheets:

&#x20;  - Matches by PO number (if available)

&#x20;  - Validates vendor name and total amount

&#x20;  - Calculates match score (0-100%)

5\. \*\*Status Determination\*\*:

&#x20;  - \*\*Auto-Approved\*\*: Match score 100% + OCR confidence ≥90%

&#x20;  - \*\*Pending Manual Review\*\*: Match score 70-99%

&#x20;  - \*\*Pending Review\*\*: Match score <70% or no PO match

6\. \*\*Approval Routing\*\*:

&#x20;  - Auto-approved invoices → Slack notification

&#x20;  - Invoices requiring approval → Email to finance manager

7\. \*\*Logging\*\*: All invoices logged in Google Sheets with full details



\### Daily Payment Reminder Flow:

1\. \*\*Scheduled Check\*\*: Runs daily at 9:00 AM

2\. \*\*Due Date Analysis\*\*: Checks all approved invoices

3\. \*\*Categorization\*\*:

&#x20;  - \*\*Overdue Payments\*\*: Due date < today

&#x20;  - \*\*Upcoming Payments\*\*: Due date within next 3 days

4\. \*\*Email Reminder\*\*: Sends consolidated reminder to finance team



\## 🚀 How to Use



\### Prerequisites



\- n8n instance (self-hosted or cloud)

\- Email account with IMAP access

\- Google Drive account

\- Google Sheets account

\- OpenAI API key (with Vision access)

\- Slack workspace (optional)



\### Setup Steps



1\. \*\*Import Workflow\*\*

&#x20;  - Open n8n

&#x20;  - Click "Import from File"

&#x20;  - Select `workflow.json`



2\. \*\*Configure Email Trigger\*\*

&#x20;  - Set your email credentials (IMAP server, username, password)

&#x20;  - Update subject filter if needed (default: "Invoice")



3\. \*\*Configure Google Drive\*\*

&#x20;  - Connect your Google Drive account

&#x20;  - Update `YOUR\_GOOGLE\_DRIVE\_ID` with your Drive ID

&#x20;  - Update `YOUR\_INVOICES\_FOLDER\_ID` with target folder ID



4\. \*\*Configure OpenAI\*\*

&#x20;  - Add your OpenAI API credentials

&#x20;  - Model is set to GPT-4 Vision Preview



5\. \*\*Configure Google Sheets\*\*

&#x20;  - Connect your Google Sheets account

&#x20;  - Update `YOUR\_GOOGLE\_SHEET\_ID` with your sheet ID

&#x20;  - Create two sheets:



&#x20;  \*\*Sheet 1: "PurchaseOrders"\*\* with columns:

&#x20;  - po\_number

&#x20;  - vendor\_name

&#x20;  - total\_amount

&#x20;  - order\_date

&#x20;  - status



&#x20;  \*\*Sheet 2: "InvoiceLog"\*\* with columns:

&#x20;  - invoice\_id

&#x20;  - invoice\_number

&#x20;  - invoice\_date

&#x20;  - due\_date

&#x20;  - vendor\_name

&#x20;  - total\_amount

&#x20;  - currency

&#x20;  - matched\_po

&#x20;  - match\_score

&#x20;  - confidence\_score

&#x20;  - status

&#x20;  - requires\_approval

&#x20;  - drive\_url

&#x20;  - received\_at

&#x20;  - processed\_at



6\. \*\*Configure Slack (Optional)\*\*

&#x20;  - Connect your Slack account

&#x20;  - Update channel name (default: #finance-notifications)



7\. \*\*Configure Email Notifications\*\*

&#x20;  - Update email addresses:

&#x20;    - finance@yourcompany.com (sender)

&#x20;    - finance-manager@yourcompany.com (approval requests)

&#x20;    - finance-team@yourcompany.com (payment reminders)



8\. \*\*Activate Workflow\*\*

&#x20;  - Toggle the workflow to "Active"

&#x20;  - Test by sending an invoice email to your monitored inbox



\## 🔐 Credentials Required



\- \*\*IMAP Email\*\*: Email server credentials

\- \*\*Google Drive OAuth2\*\*: Google Drive API access

\- \*\*Google Sheets OAuth2\*\*: Google Sheets API access

\- \*\*OpenAI API\*\*: OpenAI API key with Vision access

\- \*\*SMTP Email\*\*: Email sending credentials

\- \*\*Slack API\*\*: Slack bot token (optional)



\## 📊 Matching \& Approval Logic



\### Match Score Calculation:

\- \*\*100%\*\*: PO number matches + Amount matches (±$1) + Vendor matches

\- \*\*70%\*\*: Either amount OR vendor matches

\- \*\*50%\*\*: PO found but neither amount nor vendor matches

\- \*\*0%\*\*: No PO match found



\### Approval Requirements:

\- \*\*Auto-Approved\*\*: Match score = 100% AND OCR confidence ≥ 90%

\- \*\*Manual Review Required\*\*: All other cases



\### Status Flow:

1\. `pending\_review` → Initial status after OCR

2\. `auto\_approved` → Automatically approved (no manual intervention)

3\. `pending\_manual\_review` → Requires finance manager approval

4\. `approved` → Manually approved by finance manager

5\. `rejected` → Rejected by finance manager

6\. `paid` → Payment completed



\## 💡 Use Cases



\- \*\*Accounts Payable\*\*: Automate invoice receipt and processing

\- \*\*Procurement\*\*: Match invoices with purchase orders automatically

\- \*\*Finance Teams\*\*: Streamline approval workflows

\- \*\*Small Businesses\*\*: Reduce manual data entry and errors

\- \*\*Enterprise\*\*: Handle high volumes of invoices efficiently



\## 🔧 Customization Ideas



\- Add multi-level approval based on invoice amount thresholds

\- Integrate with accounting software (QuickBooks, Xero, SAP)

\- Add vendor performance tracking

\- Implement duplicate invoice detection

\- Add currency conversion for international invoices

\- Create dashboard for invoice analytics and cash flow forecasting

\- Add automatic payment scheduling

\- Integrate with bank APIs for direct payment processing



\## 📝 Notes



\- OCR quality depends on invoice image clarity and format

\- Standard invoice formats yield better extraction results

\- Match score thresholds can be adjusted in the Code Node

\- Consider adding error handling for failed OCR extractions

\- For high volumes, implement queue management

\- Test with various invoice formats to ensure robustness



\## 🐛 Troubleshooting



\*\*Issue\*\*: OCR extraction failing or inaccurate

\- \*\*Solution\*\*: Ensure invoice images are clear and readable; check OpenAI Vision API limits



\*\*Issue\*\*: No purchase order match found

\- \*\*Solution\*\*: Verify PO data in Google Sheets; check PO number format consistency



\*\*Issue\*\*: Approval email not sent

\- \*\*Solution\*\*: Check SMTP credentials; verify email addresses



\*\*Issue\*\*: Payment reminders not working

\- \*\*Solution\*\*: Verify due\_date format (YYYY-MM-DD); check Schedule Trigger settings



\*\*Issue\*\*: Auto-approval not triggering

\- \*\*Solution\*\*: Check match score calculation logic; verify OCR confidence threshold



\## 📄 License



This workflow is provided as-is for educational and commercial use.



\## 🤝 Contributing



Feel free to fork, modify, and improve this workflow for your specific needs.



\---



\*\*Created for\*\*: n8n-workflows-practice  

\*\*Exercise\*\*: 12 - Invoice Processing Automation  

\*\*Author\*\*: Koroosh  

\*\*Date\*\*: 2026

