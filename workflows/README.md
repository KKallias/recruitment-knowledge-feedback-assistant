# Workflow Files

The current prototype is implemented in n8n.

The exported workflow JSON is **not yet committed**. Before publishing an export, it will be reviewed to ensure that API keys, credentials, private URLs, identifiers and personal data are not included.

## Current workflow

The implemented nodes shown in the current prototype include:

- policy upload
- Default Data Loader
- Recursive Character Text Splitter
- OpenAI Embeddings
- Pinecone Vector Store
- chat trigger
- AI Agent
- OpenAI Chat Model
- Pinecone Vector Store as an agent tool

When the sanitized export is available, it will be stored in this directory as:

`recruitment-policy-assistant.json`
