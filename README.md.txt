# Autonomous Insurance Claims Processing Agent

This project is a lightweight Python agent that processes FNOL (First Notice of Loss)
documents, extracts important claim fields, detects missing data, and routes claims
based on predefined business rules.

## Features
- Extracts policy and incident details
- Identifies missing mandatory fields
- Routes claims automatically
- Outputs structured JSON

## Technologies
- Python
- pdfplumber
- regex

## How to Run

1. Install Python
2. Install dependencies
   pip install -r requirements.txt
3. Run application
   python app.py

## Output Format

{
  "extractedFields": {},
  "missingFields": [],
  "recommendedRoute": "",
  "reasoning": ""
}

