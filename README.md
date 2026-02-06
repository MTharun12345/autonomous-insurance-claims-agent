# Autonomous Insurance Claims Processing Agent

Lightweight Python agent for extracting FNOL fields and routing insurance claims.

## 📌 Features
- Extracts key fields from FNOL text files
- Identifies missing mandatory information
- Applies rule-based claim routing
- Outputs structured JSON

## 🛠 Technologies Used
- Python
- Regex

## ▶ How to Run

1. Install Python  
2. Install dependencies  
   pip install -r requirements.txt  

3. Run the application  
   python app.py  

## 📄 Sample Input
FNOL text file: sample_fnol.txt

## 📤 Sample Output
JSON object containing:
- extractedFields  
- missingFields  
- recommendedRoute  
- reasoning  

