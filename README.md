# Multi-Modal Document Intelligence (RAG-Based QA System)

This project implements a Retrieval-Augmented Generation (RAG) system designed to handle complex financial documents containing text, tables, and images. It features a multi-modal ingestion pipeline and a QA chatbot interface capable of providing source-backed answers.

## Features

* **Multi-Modal Ingestion:** Extracts text, parses tables, and performs OCR on charts/images using Tesseract.
* **Local Privacy:** Runs entirely offline using open-source models (No API keys required).
* **Vector Search:** Utilizes FAISS for efficient semantic retrieval.
* **Source Attribution:** Every answer includes precise citations (Page #, Source Type, and Relevance Score).
* **Automated Pipeline:** Single-script execution for data processing and embedding generation.

## Technical Stack

* **LLM:** `google/flan-t5-base` (via HuggingFace)
* **Embeddings:** `sentence-transformers/all-MiniLM-L6-v2`
* **Vector Store:** FAISS (CPU)
* **OCR Engine:** Tesseract
* **PDF Processing:** PyMuPDF (Fitz)
* **UI:** Streamlit

## Project Structure

```text
assignment/
├── data/
│   ├── raw/                # Place PDF here
│   ├── processed/          # JSON chunks
│   ├── vector_store/       # FAISS index
│   └── images/             # Extracted chart images
├── app.py                  # Streamlit Dashboard
├── config.py               # Configuration paths & models
├── create_embeddings.py    # Vectorization script
├── document_processor.py   # PDF parsing & OCR logic
├── llm_qa.py               # LLM generation logic
├── process_document.py     # Ingestion entry point
├── run_pipeline.py         # Automation script
├── vector_store.py         # FAISS wrapper
└── requirements.txt        # Python dependencies
```
## Setup & Installation
### 1. System Prerequisites (Tesseract OCR)
You must install Tesseract OCR on your machine for image processing to work.

Windows: Download Installer and add to PATH.

Mac: brew install tesseract

Linux: sudo apt-get install tesseract-ocr

### 2. Python Environment
Create a virtual environment and install dependencies:

```Bash

pip install -r requirements.txt
```
### 3. Add Data
Place your target document (e.g., qatar_test_doc.pdf) inside the data/raw/ folder. Note: The code defaults to looking for qatar_test_doc.pdf per config.py.

##  How to Run
### Step 1: Run the Ingestion Pipeline
This script handles directory creation, document processing (OCR), and vector embedding generation automatically.

```bash

python run_pipeline.py
```
Wait for the "PIPELINE COMPLETE" message.

### Step 2: Launch the Demo App
Start the chatbot interface:

```bash

streamlit run app.py
```
## Evaluation & Benchmarks
**Ingestion Speed**: ~0.5s per chunk (CPU).

**Retrieval**: Top-5 semantic search using Cosine Similarity.

**Generation**: Context window limited to 512 tokens (Flan-T5 base constraint).
