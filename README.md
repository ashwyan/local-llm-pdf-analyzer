# 📄 On-Device PDF Analyzer with Local LLM

Analyze any PDF documents using a **fully local LLM** — no internet connection, no API keys, no data leaving your machine. Built with [Ollama](https://ollama.com) and [LangChain](https://www.langchain.com/).

---

## ✨ What It Does

Drop PDFs into a folder, run the notebook, and get a structured analysis of each document including:

- **Summary** of the main argument
- **Key Takeaways** in bullet form
- **Important Keywords** with definitions
- **Resources Mentioned** in the text
- **Most Memorable Quote**
- **Study Questions** to test understanding
- **ELI5 Explanation** — core idea in plain language
- **Potential Exam Topics**
- A **scrolling MP4 video** of the full analysis output (optional)
- A saved **Markdown report** (`analysis_report.md`)

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| [Ollama](https://ollama.com) | Runs LLMs locally on your machine |
| [LangChain](https://langchain.com) | Chains prompt → model → output |
| [pypdf](https://pypdf.readthedocs.io) | Extracts text from PDF files |
| [Matplotlib](https://matplotlib.org) | Renders the scrolling MP4 video |
| [ffmpeg](https://ffmpeg.org) | Video encoding (required for MP4) |

---

## ⚡ Quickstart

### 1. Install Ollama

Download from [https://ollama.com](https://ollama.com) and install for your OS. Then pull a model:

```bash
ollama pull llama3
```

Ollama must be running in the background before you use the notebook:

```bash
ollama serve
```

### 2. Install Python Dependencies

```bash
pip install langchain-community langchain-ollama pypdf matplotlib
```

### 3. (Optional) Install ffmpeg for Video Export

| OS | Command |
|---|---|
| macOS | `brew install ffmpeg` |
| Ubuntu/Debian | `sudo apt install ffmpeg` |
| Windows | Download from [ffmpeg.org](https://ffmpeg.org/download.html) |

### 4. Add Your PDFs

Create a `pdfs/` folder in the same directory as the notebook and drop your PDF files in:

```
your-project/
├── On_device_LLM.ipynb
├── pdfs/
│   ├── lecture_notes.pdf
│   ├── research_paper.pdf
│   └── ...
└── README.md
```

### 5. Run the Notebook

Open the notebook in JupyterLab or VS Code and run cells top to bottom.

---

## ⚙️ Configuration

All settings are in **Cell 2**:

```python
PDF_FOLDER  = "pdfs"         # Folder with your PDF files
MODEL_NAME  = "llama3:8b"    # Any model you've pulled via Ollama
MAX_CHARS   = 12000          # Max characters sent to the LLM per doc
OUTPUT_VIDEO = "analysis_output.mp4"
```

### Supported Models

Any model available on Ollama works. Recommendations:

| Model | Size | Good For |
|---|---|---|
| `llama3:8b` | ~4.7 GB | Balanced speed + quality (default) |
| `mistral` | ~4.1 GB | Fast, great for summarization |
| `gemma:7b` | ~5 GB | Strong academic text analysis |
| `phi3` | ~2.3 GB | Lightweight, good for older hardware |

---

## 📁 Output Files

| File | Description |
|---|---|
| `analysis_report.md` | Full structured analysis in Markdown |
| `analysis_output.mp4` | Scrolling video of the analysis (optional) |

---

## 🔍 How It Works

```
pdfs/ folder
     │
     ▼
pypdf extracts text from each PDF
     │
     ▼
Text is truncated to MAX_CHARS if needed
     │
     ▼
LangChain prompt template fills in the document text
     │
     ▼
Ollama runs the LLM locally on your machine
     │
     ▼
StrOutputParser returns clean text
     │
     ├── Saved to analysis_report.md
     └── Rendered to scrolling MP4 (optional)
```

---

## ⚠️ Known Limitations

- **Scanned/image PDFs** — pypdf can only extract text from text-based PDFs. If your PDF is a scanned image, you'll need an OCR step first (e.g., `pytesseract`).
- **Very long documents** — text is truncated at `MAX_CHARS` to prevent context overflow. For large documents, consider splitting them.
- **Speed** — local inference is slower than cloud APIs. Expect 30–90 seconds per document depending on your hardware and model size.

---

## 🚀 Ideas for Future Improvement

- [ ] Add OCR support for scanned PDFs
- [ ] Implement RAG (Retrieval-Augmented Generation) with vector embeddings for long documents
- [ ] Interactive Q&A mode where you can ask follow-up questions
- [ ] Web UI with Gradio or Streamlit
- [ ] Support for `.docx` and `.txt` files

---

## 👤 Author

Built by a UC Berkeley Statistics student as a hands-on project in local LLM deployment and document analysis.
