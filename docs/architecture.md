# Architecture Notes

## Current prototype

The implemented workflow uses n8n for orchestration, OpenAI for the chat model and embeddings, and Pinecone for vector storage and retrieval.

### Ingestion path

```text
Upload Policy
→ Default Data Loader
→ Recursive Character Text Splitter
→ OpenAI Embeddings
→ Pinecone Vector Store
```

### Retrieval path

```text
Chat Trigger
→ AI Agent
→ Pinecone Vector Store tool
→ OpenAI Chat Model
→ Response
```

## Why RAG

The project is based on a fictional recruitment-policy library where answers may depend on information contained in policy and process documents. Retrieval allows relevant document context to be supplied to the model instead of relying only on general model knowledge.

## Current boundary

The screenshot demonstrates the initial ingestion and retrieval foundation. It does not demonstrate source citations, reranking, evaluation, document versioning, PostgreSQL/pgvector, or the deterministic feedback-reminder branch. Those remain roadmap items.

## Planned direction

The intended full project adds chunk metadata, source/version handling, citations, an insufficient-evidence path, retrieval evaluation and a separate rule-based workflow for overdue feedback.

This document will be updated as those components are actually implemented.
