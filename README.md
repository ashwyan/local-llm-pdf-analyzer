# 🏭 On-Device PDF Analyzer & Q&A Engine

**Industrial-grade, fully local RAG pipeline for document analysis and question answering.**

No cloud APIs. No data leaves your machine. Privacy by design.

## Architecture

```
PDFs ──▶ Loader ──▶ Chunker ──▶ Embeddings ──▶ FAISS Vector Store
                                                       │
                                    ┌──────────────────┘
                                    ▼
                    User Query ──▶ Retriever ──▶ LLM ──▶ Answer + Sources
```

## Features

| Feature | Description |
|---------|-------------|
| **RAG Q&A** | Ask natural-language questions, get answers with source attribution |
| **Multi-Doc Analysis** | Batch analysis producing structured Markdown reports |
| **Semantic Search** | FAISS vector store with MMR diversity-aware retrieval |
| **Source Tracing** | Every answer cites specific document chunks |
| **Caching** | Vector store persists to disk — skip re-embedding on reload |
| **Structured Logging** | Timestamped logs to file + console |
| **Export** | Markdown reports, JSON payloads, scrolling MP4 video |
| **Configurable** | Swap models, chunking params, retrieval strategy via dataclass |

## Quick Start

### Prerequisites
- Python 3.10+
- [Ollama](https://ollama.com) installed and running

### Setup

```bash
# 1. Pull required models
ollama pull llama3:8b
ollama pull nomic-embed-text

# 2. Install Python dependencies
pip install -r requirements.txt

# 3. Add your PDFs
mkdir -p pdfs
cp your-documents/*.pdf pdfs/

# 4. Launch the notebook
jupyter notebook On_Device_LLM_Industrial.ipynb
```

### Run

Execute cells 1–10 in order. Then:
- **Cell 11**: Interactive Q&A (type questions live)
- **Cell 12**: Batch Q&A (edit predefined questions)
- **Cell 13**: Export reports (Markdown + JSON)
- **Cell 14**: Generate MP4 video summary

## Configuration

All settings live in `PipelineConfig` (Cell 3):

```python
config = PipelineConfig(
    llm_model="llama3:8b",         # Any Ollama model
    embedding_model="nomic-embed-text",
    chunk_size=1000,                # Chars per chunk
    chunk_overlap=200,              # Context overlap
    retrieval_k=5,                  # Top-k chunks for Q&A
    search_type="mmr",              # "similarity" or "mmr"
    temperature=0.1,                # Analysis temperature
    qa_temperature=0.2,             # Q&A temperature
)
```

## Project Structure

```
├── On_Device_LLM_Industrial.ipynb   # Main notebook
├── requirements.txt                  # Python dependencies
├── pdfs/                            # Input PDF documents
├── vectorstore/                     # Cached FAISS index
├── outputs/                         # Generated reports
│   ├── analysis_report.md
│   ├── analysis_results.json
│   └── analysis_output.mp4
└── logs/                            # Timestamped pipeline logs
```

## Model Recommendations

| Model | Speed | Quality | VRAM | Best For |
|-------|-------|---------|------|----------|
| `llama3:8b` | ★★★★ | ★★★★ | 6 GB | General use (recommended) |
| `mistral` | ★★★★★ | ★★★ | 4 GB | Fast analysis |
| `gemma:7b` | ★★★★ | ★★★★ | 5 GB | Balanced |
| `phi3` | ★★★★★ | ★★★ | 3 GB | Low-resource machines |
| `llama3:70b` | ★★ | ★★★★★ | 40 GB | Maximum quality |

## Tech Stack

- **LLM Runtime**: Ollama (local inference)
- **Orchestration**: LangChain
- **Embeddings**: nomic-embed-text via Ollama
- **Vector Store**: FAISS (Facebook AI Similarity Search)
- **PDF Parsing**: pypdf
- **Visualization**: matplotlib + ffmpeg

