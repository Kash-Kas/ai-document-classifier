# ai-document-classifier
AI-powered document classification workflow using n8n and OpenAI
AI Document Classifier
An AI-powered document classification workflow built with n8n and OpenAI GPT-4o-mini.
This tool automatically analyzes text content and classifies documents into categories such as Invoice, Resume, Contract, Report, and Email — returning structured results in JSON format.
---
What It Does
Send any document text to the webhook endpoint, and the workflow will return:
Category — Document type (Invoice, Resume, Contract, Report, Email, Other)
Confidence — Classification confidence level (high / medium / low)
Summary — One-sentence description of the document
Key Entities — Up to 3 important names, dates, or amounts extracted from the text
---
Workflow Architecture
```
Webhook (POST)
    ↓
Extract Text (Code Node)
    ↓
Classify with OpenAI GPT-4o-mini
    ↓
Format Result (Code Node)
    ↓
JSON Response
```
---
Example
Input:
```json
{
  "filename": "invoice_april.txt",
  "text": "INVOICE #001 From: Acme Corp To: XYZ Inc Amount Due: $1500 Due Date: June 1 2026"
}
```
Output:
```json
{
  "filename": "invoice_april.txt",
  "char_count": 80,
  "category": "Invoice",
  "confidence": "high",
  "summary": "This document is an invoice from Acme Corp to XYZ Inc for $1500 due on June 1, 2026.",
  "key_entities": ["Acme Corp", "XYZ Inc", "$1500"],
  "processed_at": "2026-05-08T20:24:43.770Z"
}
```
---
Supported Document Categories
Category	Description
Invoice	Billing and payment documents
Contract	Legal agreements
Resume	Job application documents
Report	Business or analytical reports
Email	Email message content
Other	Uncategorized documents
---
Tech Stack
Tool	Purpose
n8n	Workflow automation platform
OpenAI GPT-4o-mini	AI classification and summarization
JavaScript (Code Node)	Data extraction and formatting
Webhook	HTTP endpoint for receiving documents
---
How to Use
1. Import the Workflow
Download `workflow.json` and import it into your n8n instance:
> n8n → New Workflow → Import from file
2. Configure Credentials
Add your OpenAI API key in the "Message a model" node
3. Send a Request
PowerShell:
```powershell
Invoke-RestMethod -Uri "YOUR_WEBHOOK_URL" -Method POST -ContentType "application/json" -Body '{
  "filename": "document.txt",
  "text": "Your document text here"
}'
```
curl:
```bash
curl -X POST YOUR_WEBHOOK_URL \
  -H "Content-Type: application/json" \
  -d '{"filename": "document.txt", "text": "Your document text here"}'
```
---
Project Background
This workflow is part of my automation portfolio, demonstrating practical AI + workflow automation skills.
It is designed to be extended with:
Web UI for browser-based input (in progress)
PDF/Word file upload support (planned)
Integration with Python PDF extraction tool
---
Related Projects
pdf-automation — Python tool for PDF keyword search, highlight, and file processing
job-market-analysis — LinkedIn job market analysis using Python, SQL, and Claude API
---
Author
Kaori Kashiwagi — Automation & AI Automation enthusiast  
Building toward: AI Automation Architect  
Focus areas: Business systems, ERP, workflow automation, AI integration
