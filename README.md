# AccountsClassifier
📘 Accounts Receivable Matching Automation (n8n)

This project is an Accounts Receivable (AR) automation workflow built using n8n, designed to:

✔ Fetch invoices & receipts from Google Drive
✔ Normalize CSV data
✔ Match invoices ↔ receipts
✔ Write matched entries to Google Sheets
✔ Detect unmatched invoices/receipts
✔ Send email alerts for mismatches

This automation helps accountants reconcile payments automatically without manually checking hundreds of entries.

🧠 Project Overview

The workflow automatically processes two CSV files:

invoices.csv → list of invoices raised

receipts.csv → list of payments received

Using n8n, it:

Downloads files from Google Drive

Parses & normalizes invoice + receipt data

Matches entries using merge logic

Pushes matched data to a Google Sheet

Finds unmatched invoices (invoice without payment)

Finds unmatched receipts (payment without invoice)

Sends email alerts for exceptions

Stores unmatched data in separate Google Sheets

This replicates a real-world AR reconciliation system.

⚙️ Features
🔹 Data Normalization

Converts invoice and receipt numbers to a consistent format (uppercase, trimmed)

Fixes date formats (DD-MM-YYYY → YYYY-MM-DD)

Converts amounts to numeric values

Handles spelling mistakes in CSV headers

🔹 Matching Logic

Uses Merge → Combine (Matching Items) for matched entries

Uses Left Join to find unmatched invoices

Uses Right Join to find unmatched receipts

Filters using IF nodes

🔹 Google Sheets Output

Three sheets are updated:

Matched_AR_Entries

Unmatched_Invoices

Unmatched_Receipts

🔹 Email Alerts

Sends an email to the accountant when:

An invoice is missing a receipt

A receipt has no matching invoice

🧩 Workflow Architecture
1. Data Input

Google Drive → Download Invoices

Google Drive → Download Receipts

2. Parsing & Cleaning

Extract from File (CSV → JSON)

Normalize Invoices (Code/Set Node)

Normalize Receipts (Code/Set Node)

3. Matching

Merge (Combine → Matching Items) → Matched Output

Merge (Left Join) → Unmatched Invoices

Merge (Right Join) → Unmatched Receipts

4. Filtering

IF (ReceiptInvoiceNumber empty?) → Unmatched Invoices

IF (InvoiceNumber empty?) → Unmatched Receipts

5. Output

Google Sheet → Matched Entries

Google Sheet → Unmatched Invoices

Google Sheet → Unmatched Receipts

Email Notification Nodes (Gmail / SMTP)

📄 Google Sheet Column Structure
Matched_AR_Entries
InvoiceNumber
InvoiceDate
CustomerName
InvoiceAmount
ReceiptID
ReceiptInvoiceNumber
ReceivedDate
AmountReceived

Unmatched_Invoices
InvoiceNumber
InvoiceDate
CustomerName
InvoiceAmount
Status
Note

Unmatched_Receipts
ReceiptID
ReceiptInvoiceNumber
ReceivedDate
AmountReceived
Status
Note

📂 Repository Structure
├── invoices.csv
├── receipts.csv
├── ar-matching-workflow.json
├── README.md
└── assets/
     ├── workflow-diagram.png
     ├── merge-node-screenshot.png
     ├── normalization-screenshot.png
     └── example-results.png

🚀 How to Use This Project

Import ar-matching-workflow.json into n8n

Update Google Drive IDs for your files

Update Google Sheets IDs

Configure Gmail/SMTP credentials

Execute the workflow

Check Sheets for matched/unmatched entries

🛠️ Tech Stack

n8n (Self-Hosted)

Google Drive API

Google Sheets API

Gmail / SMTP

JavaScript (for normalization)

📬 Contact

For questions or improvements, feel free to raise an issue or contribute.
