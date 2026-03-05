# Flux RAG Assistant

**Role:** Lead Engineer  
**Tech Stack:** Python, LangChain, FastAPI, Vector Databases, Next.js

## Overview

The **Flux RAG (Retrieval-Augmented Generation) Assistant** was engineered to solve enterprise knowledge retrieval bottlenecks. By embedding massive amounts of internal documentation into a vector database, this system allows employees to query internal policies and technical guides using natural language, drastically reducing onboarding and research time.

---

## 1. The Challenge

Traditional enterprise search relies on keyword matching, which fails when users don't know the exact terminology. Documentation is often siloed across Confluence, Google Drive, and local markdown files.

We needed a system that could "understand" semantic intent across varied file types and synthesize accurate, hallucination-free answers citing its exact source.

## 2. Technical Implementation

### Document Ingestion Pipeline

We built a robust extraction pipeline that cron-syncs with internal drives, parses PDFs, raw text, and Markdown, chunks them contextually using an intelligent token splitter, and embeds them using OpenAI's embedding models.

### Vector Search & Retrieval

Using an open-source vector database, we structured the querying layer. When a user asks a question:

1. The question is embedded.
2. We perform a k-nearest neighbors (k-NN) search to pull the top 5 most relevant document chunks.
3. These chunks are injected into the context window of a Large Language Model (LLM).

### The API Layer

The backend is a high-performance **FastAPI** application, utilizing asynchronous concurrent requests to handle multiple user queries simultaneously.

```python
# Pseudo-code architecture of the Retrieval endpoint
@app.post("/api/v1/query")
async def process_query(req: QueryRequest):
    # Retrieve relevant context
    context = await vector_db.similarity_search(req.question, k=5)

    # Generate response via LLM
    response = await llm_chain.predict(
        question=req.question,
        context=context
    )
    return {"answer": response, "sources": context}
```

## 3. Results & Impact

- Reduced average internal query time from 15 minutes to 3 seconds.
- Achieved a hallucination rate of less than 2% via strict prompt engineering guardrails.
- Fully deployed on scalable containerized infrastructure via Docker and Kubernetes.
