# Marksheet Management System (ML + OCR + LLM)

An OCR-based backend system to extract structured marksheet data from images and PDFs using **Tesseract OCR** and rule-based/LLM-based text processing for structured JSON output.

## Architecture

```
Client → FastAPI → OCR (Tesseract) → Text → LLM (Gemini/Ollama) → JSON Output
```


## Tech Stack

* **Backend**: FastAPI
* **OCR**: Tesseract (`pytesseract`)
* **Image Processing**: PIL, pdf2image
* **LLM Integration**:

  * Google Gemini (`google.genai`)
  * Ollama
* **Storage**: AWS S3 / MinIO (`boto3`)
* **Config**: YAML + Environment Variables


## 📦 Installation

### 1. Clone the repository

```bash
git clone https://github.com/Industrial-Projects-2025-2026/ml-marksheet-processing.git
cd ml-marksheet-processing
```

### 2. Create virtual environment

```bash
python -m venv venv
source venv/bin/activate   # Mac/Linux
venv\Scripts\activate      # Windows
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```


## Configuration

### `.env` file

```env
UVICORN_HOST=0.0.0.0
UVICORN_PORT=8000
S3_ENDPOINT_URL=http://s3:9000
S3_ACCESS_KEY=admin
S3_SECRET_KEY=admin123
S3_REGION=us-east-1
GEMINI_API_KEY=gemini_api_key
```

---

## ▶️ Run the Application

```bash
python -W ignore api.py
```

Server runs at:

```
http://localhost:8000
```

## 📡 API Endpoint

### 1. Process File from S3

**POST** `/process`

**Request:**

```json
{
  "bucket": "your-bucket",
  "key": "path/to/file.pdf"
}
```

---

## 🧠 How It Works

1. File is uploaded (image/PDF)
2. PDF → converted to images (`pdf2image`)
3. Image → preprocessed (grayscale, scaling, contrast)
4. OCR → text extraction (`pytesseract`)
5. Board detection → selects correct prompt
6. LLM → converts text into structured JSON
7. JSON response returned


## ⚡ Key Features Explained

### 🔍 OCR Processing

* Uses Tesseract with optimized config:

  ```
  --oem 3 --psm 6
  ```
* Image enhancement: grayscale + autocontrast

### 🧠 LLM Integration

Supports:

* Google Gemini API
* Ollama local models
* Automatic retry mechanism with exponential backoff

### 📄 Board Detection

* Keyword-based detection from OCR text
* Maps to predefined prompts


## Running the Application with Docker

```bash
docker compose -p mms up
```