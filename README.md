# Portfolio RAG Scripts

A Retrieval-Augmented Generation (RAG) pipeline that extracts text from PDF documents, generates embeddings using Google's Gemini models, stores them in a ChromaDB vector database, and enables semantic search with LLM-powered question answering.

## Overview

This project implements a complete RAG workflow:

1. **PDF Text Extraction** — Reads and extracts text content from PDF files using `pypdf`
2. **Text Chunking** — Splits extracted text into overlapping chunks for efficient retrieval
3. **Embedding Generation** — Converts text chunks into vector embeddings using Google's `gemini-embedding-2` model
4. **Vector Storage** — Stores embeddings in a persistent ChromaDB collection (`rag_db/`)
5. **Semantic Retrieval** — Queries the vector store to find the most relevant chunks for a user query
6. **Answer Generation** — Feeds retrieved context to Gemini (`gemini-2.5-flash`) to produce grounded answers

The workflow is encapsulated in a Jupyter Notebook (`rag_scripts.ipynb`) for interactive exploration and demonstration.

## Architecture

```
PDF Document
    │
    ▼
Text Extraction (PyPDF)
    │
    ▼
Chunking (configurable size & overlap)
    │
    ▼
Embedding (gemini-embedding-2)
    │
    ▼
ChromaDB (persistent vector store)
    │
    ▼
Semantic Query → Retrieved Context → Gemini Generation → Answer
```

## Prerequisites

- Python 3.12 or higher
- A Google AI (Gemini) API key

## Setup

### 1. Clone the repository

```bash
git clone https://github.com/karthi-100/portfolio-rag-scripts.git
cd portfolio-rag-scripts
```

### 2. Install dependencies

Using **pip**:

```bash
pip install -r requirements.txt
```

Or using **uv** (recommended for faster dependency resolution):

```bash
uv sync
```

### 3. Configure environment variables

Create a `.env` file in the project root with your Google API key:

```
GOOGLE_API_KEY=your_google_api_key_here
```

Get your API key from [Google AI Studio](https://aistudio.google.com/apikey).

### 4. Run the notebook

Launch Jupyter Notebook or JupyterLab:

```bash
jupyter notebook rag_scripts.ipynb
```

Or if you have VS Code, open the project and run the notebook cells directly.

## Project Structure

```
├── rag_scripts.ipynb     # Main Jupyter notebook with the RAG pipeline
├── requirements.txt       # Python dependencies
├── pyproject.toml         # Project metadata and build configuration
├── .env                   # Environment variables (GOOGLE_API_KEY) — not tracked in git
├── .gitignore             # Git ignore rules
├── .python-version        # Python version pinning
├── uv.lock                # Lock file for uv dependency manager
├── karthi_profile_summary.pdf  # Sample PDF used for demonstration
├── rag_db/                # Persistent ChromaDB storage directory
└── README.md              # This file
```

## Dependencies

| Package          | Version   | Purpose                              |
|------------------|-----------|--------------------------------------|
| `google-genai`   | ≥2.0.1    | Gemini API for embeddings and generation |
| `chromadb`       | ≥1.5.9    | Vector database for embedding storage |
| `pypdf`          | ≥6.11.0   | PDF text extraction                   |
| `python-dotenv`  | ≥1.2.2    | Environment variable loading          |

## Usage Example

The notebook (`rag_scripts.ipynb`) walks through each step:

1. **Load API key** from `.env` and initialize the Gemini client
2. **Extract text** from a PDF file (e.g., `karthi_profile_summary.pdf`)
3. **Chunk the text** into overlapping segments (default: 500 chars with 50 char overlap)
4. **Generate embeddings** for each chunk using `gemini-embedding-2`
5. **Store embeddings** in ChromaDB under the collection `knowledge_base`
6. **Query** the vector store with a question (e.g., "tell me about karthi's skills")
7. **Generate an answer** using `gemini-2.5-flash` with the retrieved context

## License

This project is for demonstration purposes. See the repository for details.