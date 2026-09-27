# Recruitment Knowledge & Feedback Assistant

> **Status:** Prototype in development  
> **Portfolio:** Project 1 of my AI Automation Engineering portfolio

A hands-on AI automation project exploring how Retrieval-Augmented Generation (RAG) can help recruiters and interviewers retrieve answers from a controlled recruitment policy knowledge base while keeping deterministic workflow decisions separate from AI-generated answers.

This project connects my previous Talent Acquisition experience with my transition into **AI Automation Engineering**.

## Project Goal

Recruitment teams work across interview-process guides, scorecard guidance, communication rules, escalation procedures and role-intake documentation.

The goal is to build an assistant that can:

- ingest recruitment policy documents into a searchable knowledge base
- retrieve relevant policy context for a user's question
- generate grounded answers from retrieved evidence
- eventually return source citations and abstain when evidence is insufficient
- separately track overdue interview feedback using explicit workflow rules

The assistant is **not designed to score, rank or recommend candidates**.

## Current Prototype

The current implementation is built in **n8n** using **OpenAI** and **Pinecone**.

### Knowledge ingestion

```text
Upload Policy
    ↓
Default Data Loader
    ↓
Recursive Character Text Splitter
    ↓
OpenAI Embeddings
    ↓
Pinecone Vector Store
```

A policy document is loaded, split into smaller chunks, converted into embeddings and stored in Pinecone for semantic retrieval.

### Question answering

```text
Chat Message
    ↓
AI Agent
   ↙   ↘
OpenAI   Pinecone Vector Store
Chat     Retrieval Tool
Model
    ↓
Grounded Response
```

A user asks a question through the n8n chat trigger. The AI Agent can query the Pinecone vector store for relevant policy information and use the retrieved context when generating its response.

## Workflow Screenshot

The current n8n workflow screenshot is stored in `docs/workflow.png`.

## Current Technology

- n8n
- OpenAI Chat Model
- OpenAI Embeddings
- Pinecone Vector Store
- Retrieval-Augmented Generation (RAG)
- Recursive text splitting
- Semantic/vector retrieval
- AI Agent workflow

## What This Project Is Teaching Me

This project is helping me move from studying individual AI concepts to understanding how they connect inside an application.

Current learning areas include workflow orchestration, document ingestion, chunking and context construction, embeddings, vector databases, semantic retrieval, LLM grounding, prompt and context design, AI agents and tool use, retrieval quality, evaluation, reliability, failure handling and human oversight.

## Target Architecture

The current workflow is the first RAG foundation. The complete portfolio project is intended to progress toward:

```text
Ingest & Parse
      ↓
Chunk + Metadata
      ↓
Create Embeddings
      ↓
Vector Storage
      ↓
Retrieve Relevant Chunks
      ↓
Rerank
      ↓
Assemble Context
      ↓
Generate with Citations
      ↓
Log Result
      ↓
Evaluate Quality
      ↓
Refresh / Version Documents
```

## Planned Improvements

### Metadata and document versioning

Each chunk should eventually carry metadata such as `document_id`, `title`, `version`, `section`, `page` and `effective_date`.

Re-ingesting an updated policy should replace or deactivate the previous version so outdated information is not silently treated as current.

### Grounded answers and citations

The assistant will be instructed to answer from retrieved evidence and provide source identifiers. If the evidence is insufficient, the desired behaviour is to state that the answer was not found rather than inventing one.

### Retrieval evaluation

A labelled evaluation set of approximately 25 questions is planned. The project will measure whether supporting evidence appears in the retrieved Top 3 and Top 5 chunks.

Answer-level tests will examine citation correctness, faithfulness to retrieved text and correct abstention when evidence is missing.

### Chunking experiments

The current workflow uses a Recursive Character Text Splitter. A later experiment will compare chunk-size and overlap settings and record their effect on retrieval quality.

### Prompt-injection testing

A test document will contain an instruction inside its content. The expected behaviour is for the system to treat it as source content rather than allowing it to override system instructions.

## Deterministic Feedback Workflow

The completed project will include a separate workflow for overdue interview feedback. This part is intentionally rule-based rather than delegated to the LLM.

```text
Interview Date + Feedback Status
              ↓
          Database
              ↓
         IF / AND Rules
              ↓
     Overdue Feedback?
              ↓
       Draft Reminder
              ↓
       Reminder Flag
              ↓
 Prevent Duplicate Reminder
```

This separates **knowledge retrieval** from **workflow decisions**. RAG handles questions whose answers depend on changing policy documents. Explicit date and status rules handle reminder decisions.

## Planned Technical Extensions

- PostgreSQL
- pgvector
- SQL queries
- source metadata
- reranking
- citations
- query/result logging
- Python evaluation scripts
- retrieval tests
- document versioning
- duplicate-prevention logic

The current prototype uses **Pinecone** while I build and understand the core RAG workflow. PostgreSQL/pgvector is a planned later implementation, not a currently completed feature.

## Evaluation Philosophy

A working chatbot is not enough to demonstrate a reliable RAG system.

The finished project should provide evidence for questions such as:

1. Did retrieval find the correct source?
2. Is the generated answer supported by that source?
3. Does the citation identify the correct evidence?
4. Does the assistant abstain when evidence is unavailable?
5. What happens when a policy is updated?
6. Can instructions hidden inside source documents alter system behaviour?
7. Can deterministic reminder logic avoid duplicate actions?

## Why Recruitment?

My previous professional background includes **Talent Acquisition, recruitment operations and stakeholder-facing work**.

That experience gives me practical context around interview coordination, stakeholder questions, recruitment processes and feedback delays.

As I transition into **AI Automation Engineering**, I want my portfolio projects to connect technical learning with real operational problems I understand.

The purpose of this project is not to automate recruitment judgement. It explores how AI automation can make internal knowledge easier to retrieve while preserving evidence and keeping human decision-making separate from the system.

## Skills Demonstrated

**Current prototype:** n8n · RAG · LLM integration · OpenAI · Pinecone · embeddings · vector search · document ingestion · recursive text splitting · AI agents

**Developing through the full project:** APIs · nested JSON · PostgreSQL · SQL · pgvector · metadata filtering · reranking · citations · Python evaluation · prompt testing · retrieval evaluation · deterministic routing · human-in-the-loop design

## Repository Roadmap

- [x] Build basic document ingestion workflow
- [x] Add recursive text splitting
- [x] Generate OpenAI embeddings
- [x] Store embeddings in Pinecone
- [x] Connect chat-triggered AI Agent
- [x] Add vector-store retrieval tool
- [ ] Add fictional recruitment policy dataset
- [ ] Add source metadata
- [ ] Add citations
- [ ] Add abstention behaviour
- [ ] Compare chunking configurations
- [ ] Build labelled retrieval evaluation set
- [ ] Add retrieval and answer evaluation
- [ ] Add prompt-injection test
- [ ] Add document versioning
- [ ] Add PostgreSQL logging
- [ ] Evaluate / migrate retrieval layer with pgvector
- [ ] Build deterministic feedback reminder workflow
- [ ] Add duplicate-reminder prevention
- [ ] Add Python evaluation script
- [ ] Publish measured results and limitations

## Planned Repository Structure

```text
recruitment-knowledge-feedback-assistant/
├── README.md
├── workflows/
│   └── recruitment-policy-assistant.json
├── docs/
│   └── workflow.png
├── sample-data/
│   └── fictional-policies/
├── evaluation/
│   ├── questions.json
│   └── README.md
└── scripts/
    └── evaluate_retrieval.py
```

Only fictional or sanitized data will be committed. Credentials, API keys and personal data will never be included in exported workflows.

## Portfolio Context

This is the first project in a four-project portfolio designed to turn my learning in AI automation into practical, explainable evidence.

The broader learning path includes n8n, APIs, nested JSON, structured prompting, RAG ingestion and retrieval, evaluation, Python, SQL/PostgreSQL and MCP concepts.

My objective is to demonstrate progression from understanding fundamentals to building, testing, documenting and improving complete AI workflows.

## Author

**Konstantinos Kallias**

Career transition into AI Automation Engineering

GitHub: https://github.com/KKallias  
LinkedIn: https://www.linkedin.com/in/konstantinoskallias/
