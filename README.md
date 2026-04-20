# 🤖 DOCUMIND — RAG-Powered AI Agent
A **Retrieval-Augmented Generation (RAG)** chatbot that lets you chat with your documents. Upload a PDF, DOCX, TXT file, or paste a URL and ask questions — the agent retrieves the most relevant chunks from your document and generates accurate, context-grounded answers using a local **LLaMA 3.2** model via Ollama.
---
## ✨ Features
- 📄 **Multi-format document ingestion** — PDF, DOCX, TXT, and web URLs
- 🔍 **Semantic search** — FAISS vector store with HuggingFace embeddings (`all-MiniLM-L6-v2`)
- 🦙 **Local LLM inference** — powered by [Ollama](https://ollama.com/) running LLaMA 3.2 (no API key required)
- 💬 **Persistent chat history** — conversation context kept within a session
- 🛡️ **Safe responses** — the model is instructed to answer only from the provided document context and politely decline off-topic or flagged queries
- 🖥️ **Interactive Streamlit UI** — clean chat interface with a sidebar for model selection and document upload
---
## 🗂️ Project Structure
```
RAG-Powered-AI-Agent/
├── app.py          # Streamlit web application (main entry point)
├── helper.py       # Core logic: document parsing, vector store, LLM response
├── main.py         # Standalone CLI script for document processing
└── main.ipynb      # Jupyter notebook for exploratory development & prototyping
```
---
## 🔧 How It Works
```
User uploads document / URL
        │
        ▼
Text Extraction (PDF → PyMuPDF, DOCX → python-docx, TXT, URL → BeautifulSoup)
        │
        ▼
Embedding Generation (HuggingFace all-MiniLM-L6-v2)
        │
        ▼
FAISS Vector Store (similarity search, k=15)
        │
        ▼
Context Assembly → LLaMA 3.2 via Ollama
        │
        ▼
Grounded Answer displayed in Streamlit chat
```
---
## 🚀 Getting Started
### Prerequisites
| Requirement | Version |
|---|---|
| Python | 3.9+ |
| [Ollama](https://ollama.com/) | latest |
| LLaMA 3.2 model | pulled via Ollama |
### 1. Clone the repository
```bash
git clone https://github.com/MuhammadAdilRizwan/RAG-Powered-AI-Agent.git
cd RAG-Powered-AI-Agent
```
### 2. Install Python dependencies
```bash
pip install streamlit langchain langchain-community faiss-cpu \
            sentence-transformers pymupdf python-docx \
            beautifulsoup4 requests ollama
```
### 3. Pull the LLaMA 3.2 model
```bash
ollama pull llama3.2
```
### 4. Run the app
```bash
streamlit run app.py
```
Open your browser at `http://localhost:8501`.
---
## 🖼️ Usage
1. **Select a model** in the sidebar (currently LLaMA 3.2).
2. **Upload a document** (PDF / DOCX / TXT) **or paste a URL**.
3. The document is parsed and indexed automatically.
4. **Ask questions** in the chat box — the agent retrieves the most relevant sections and answers from the document.
> 💡 You can upload multiple documents in the same session; the vector stores are merged automatically.
---
## 📦 Key Dependencies
| Library | Purpose |
|---|---|
| `streamlit` | Web UI |
| `langchain` / `langchain-community` | Vector store abstraction |
| `faiss-cpu` | Fast similarity search |
| `sentence-transformers` | HuggingFace embeddings (`all-MiniLM-L6-v2`) |
| `pymupdf` (`fitz`) | PDF text extraction |
| `python-docx` | DOCX text extraction |
| `beautifulsoup4` | Web page text extraction |
| `ollama` | Local LLM inference (LLaMA 3.2) |
---
## 📋 Notes
- The LLM is instructed to **only answer questions that can be answered from the uploaded document**. Questions outside the document context receive a polite apology instead of a hallucinated answer.
- Ollama must be running locally (`ollama serve`) before starting the app.
- For GPU acceleration install `faiss-gpu` instead of `faiss-cpu`.
---
## 📄 License
This project is open source. Feel free to use, modify, and distribute it.
