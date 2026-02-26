# Financial RAG System — Apple & Tesla 10-K

A RAG pipeline that answers financial and legal questions 
from Apple's 2024 and Tesla's 2023 annual SEC filings.

## Approach
- PDF parsing with PyMuPDF
- Hybrid search (BM25 + Vector) with ChromaDB
- Cohere reranker for better retrieval
- Llama 3.3 70B via Groq as the open-source LLM

## Files
- `notebook.ipynb` — main runnable notebook
- `design_report.md` — design decisions explained
- `requirements.txt` — all dependencies

## How to Run
1. Open the notebook in Google Colab
2. Add your API keys (OpenAI, Groq, Cohere)
3. Run all cells top to bottom

## Tech Stack
- LLM: Llama 3.3 70B (Groq)
- Embeddings: OpenAI text-embedding-3-small
- Vector DB: ChromaDB
- Reranker: Cohere rerank-english-v3.0
- Search: Hybrid BM25 + Vector
