# local-llm-pdf-analyzer
A local AI tool using Ollama (Llama 3) to analyze PDF documents and generate a scrolling MP4 video report of the findings.

# Local LLM PDF Analyzer & Video Generator

**Author:** Ash Htet

## Project Overview
This tool allows you to upload PDF documents and receive a comprehensive analysis using a **local LLM** (Llama 3 via Ollama). Unlike standard text analyzers, this project takes the output and renders it into a **scrolling MP4 video file**, making it easy to consume the report visually.

## Features
- **Privacy-First:** Runs entirely locally using Ollama; no data leaves your device.
- **PDF Parsing:** Extracts text from multiple PDF files automatically.
- **Structured Analysis:** Generates summaries, key takeaways, and specific explanations (e.g., Monte Carlo simulations).
- **Video Output:** Converts the text analysis into a scrolling `.mp4` video format.

## Prerequisites
To run this notebook, you need two external tools installed on your machine:

1. **Ollama:** Download from [ollama.com](https://ollama.com/) and pull the Llama 3 model:
   ```bash
   ollama run llama3:8b
2. FFmpeg: Required for saving the MP4 video.
   `Mac: brew install ffmpeg`
   `Windows: Download from ffmpeg.org and add to PATH.`

## Installation
Clone the repository and install the Python dependencies:
   ```bash
   pip install langchain-community langchain-ollama pypdf matplotlib
