# 🏥 Automated EMR Clinical Summary Engine (MedGemma)

## Overview
This project is an Enterprise-Grade API designed for IMC Hospital. It takes raw, unstructured OCR text from patient medical lab reports (PDFs) and uses a **Biological Intelligence Engine** to accurately extract lab values, completely ignoring formatting errors, timestamps, and layout inconsistencies.

The extracted verified data is then fed into Google's **MedGemma-4B-IT** AI model to generate actionable, zero-hallucination clinical summaries in valid HTML for direct email dispatch.

## Core Architecture
1. **OCR Data Ingestion:** Receives raw text via n8n webhook.
2. **Biological Constraint Scanner:** Cleans noise (dates, MRNs, time) and uses medical logic to extract valid values (e.g., strictly filtering Uric Acid between 1.5 - 15.0).
3. **MedGemma AI Processor:** Processes the verified tabular data alongside unstructured Ultrasound/Clinical notes.
4. **HTML Dispatch:** Returns a fully formatted HTML overview ready for Supabase storage and email.

## Tech Stack
* **AI Model:** `google/medgemma-4b-it`
* **Framework:** FastAPI / Uvicorn (Python)
* **Hardware:** RTX A4000 (Vast.ai Cloud GPU)
* **Automation:** n8n Pipeline

## How to Run
1. Install dependencies: `pip install -r requirements.txt`
2. Authenticate HuggingFace: `huggingface-cli login`
3. Run Server: `python api_medgemma.py`
