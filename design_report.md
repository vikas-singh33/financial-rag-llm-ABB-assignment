# Design Report

## Overview
Built a RAG system to answer questions from Apple 2024 and 
Tesla 2023 10-K SEC filings using an open-source LLM.

## PDF Parsing
Used PyMuPDF (fitz) to extract text page by page. Chose it 
over unstructured because it has zero dependency conflicts 
and reliably captures page numbers for citations.

## Chunking Strategy
Used RecursiveCharacterTextSplitter with chunk_size=1000 and 
overlap=200. The overlap ensures context is not lost at chunk 
boundaries. Each chunk carries source and page metadata.

## Retrieval Pipeline
Used hybrid search combining BM25 (keyword) and vector search 
(semantic) with weights 0.7/0.3. BM25 handles exact financial 
figures like "$391,035 million" while vector search handles 
meaning-based queries. Combined they outperform either alone.

## Reranker
Used Cohere rerank-english-v3.0 to re-score top 15 hybrid 
results and return top 5. This adds a second layer of 
relevance filtering before the LLM sees any context.

## LLM Choice
Used Groq API with Llama 3.3 70B. Chosen because it is fully 
open-source, free, fast, and the LangChain integration is 
nearly identical to OpenAI making it easy to swap in.

## Out-of-Scope Handling
The prompt explicitly instructs the LLM to return a standard 
refusal message for questions outside the provided documents. 
Tested on Q11 (stock forecast), Q12 (2025 CFO), Q13 (HQ color) 
— all correctly refused.
