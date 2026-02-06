import pdfplumber
import re
import json

def extract_text(pdf_path):
    text = ""
    with pdfplumber.open(pdf_path) as pdf:
        for page in pdf.pages:
            text += page.extract_text() + "\n"
    return text

def get_field(pattern, text):
    match = re.search(pattern, text, re.IGNORECASE)
    return match.group(1).strip() if match else None

def process_claim(file):
    text = extract_text(file)

    extracted = {
        "policyNumber": get_field(r"POLICY NUMBER\s*(.*)", text),
        "claimant": get_field(r"NAME OF INSURED\s*(.*)", text),
        "dateOfLoss": get_field(r"DATE OF LOSS\s*(.*)", text),
        "description": get_field(r"DESCRIPTION OF ACCIDENT\s*(.*)", text),
        "estimatedDamage": get_field(r"ESTIMATE AMOUNT\s*(.*)", text),
        "claimType": "auto"
    }

    missing = [k for k,v in extracted.items() if v is None]

    route = ""
    reason = ""

    if missing:
        route = "Manual Review"
        reason = "Missing mandatory fields"

    elif extracted["estimatedDamage"] and int(re.sub("[^0-9]", "", extracted["estimatedDamage"])) < 25000:
        route = "Fast-track"
        reason = "Low estimated damage"

    elif "fraud" in text.lower():
        route = "Investigation Flag"
        reason = "Fraud keyword found"

    else:
        route = "Standard Queue"
        reason = "Normal claim"

    output = {
        "extractedFields": extracted,
        "missingFields": missing,
        "recommendedRoute": route,
        "reasoning": reason
    }

    print(json.dumps(output, indent=4))

process_claim("sample_fnol.pdf")
