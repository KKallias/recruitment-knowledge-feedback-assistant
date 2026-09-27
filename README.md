# Recruitment Knowledge & Feedback Assistant

**AI Automation portfolio project | n8n · OpenAI · Pinecone · RAG**

A hands-on prototype for retrieving answers from a controlled recruitment-policy knowledge base. I am building it as part of my transition into **AI Automation Engineering**, using a recruitment problem I understand from my previous Talent Acquisition experience.

> **Current status:** Working RAG foundation. The repository distinguishes completed functionality from planned improvements so that the project remains transparent and testable.

## What I built

The current n8n workflow has two connected parts.

**Document ingestion**

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

**Question answering**

```text
Chat Message
      ↓
AI Agent
   ↙       ↘
OpenAI     Pinecone Vector Store
Chat Model  + OpenAI Embeddings
      ↓
Response
```

A policy document is loaded, split into chunks, converted into embeddings and stored in Pinecone. A user can then ask a question through the n8n chat trigger. The AI Agent uses the Pinecone vector-store tool to retrieve relevant context before producing a response.

## Why this project

Recruitment teams work with process guides, scorecard guidance, candidate-communication rules, escalation procedures and role-intake documentation. Information can be spread across multiple documents and can change over time.

This project explores a practical question:

> How can an AI workflow retrieve relevant recruitment-policy information while keeping the answer grounded in a defined knowledge source?

The assistant is designed for **process and policy questions**. It does **not** score, rank or recommend candidates.

## Current implementation

| Area | Current state |
| --- | --- |
| Workflow orchestration | n8n |
| Document loading | Implemented |
| Recursive text splitting | Implemented |
| Embeddings | OpenAI Embeddings |
| Vector storage | Pinecone |
| Semantic retrieval | Implemented through Pinecone Vector Store |
| LLM | OpenAI Chat Model |
| Agent workflow | Implemented in n8n |
| Source citations | Planned |
| Abstention when evidence is insufficient | Planned |
| Retrieval evaluation | Planned |
| PostgreSQL / pgvector | Planned extension |
| Feedback reminder workflow | Planned |

This table is intentional: I want the repository to show what works today without presenting roadmap items as completed engineering work.

## Workflow screenshot

The current n8n workflow contains the ingestion path on the left and the retrieval/agent path on the right.

> **Screenshot pending repository upload.** The workflow image will be stored at `docs/workflow.png`.

## What I am learning

Building the prototype is helping me connect concepts I have been studying with an actual workflow: document ingestion, recursive chunking, embeddings, vector retrieval, LLM context, n8n node connections and AI-agent tool use.

The next stage is less about adding more nodes and more about **testing whether retrieval and answers are reliable**.

## Development roadmap

### Stage 1 — RAG foundation
- [x] Document upload
- [x] Document loader
- [x] Recursive text splitting
- [x] OpenAI embeddings
- [x] Pinecone vector storage
- [x] Chat trigger
- [x] AI Agent
- [x] Pinecone retrieval tool

### Stage 2 — Grounding and traceability
- [ ] Add source metadata
- [ ] Return source citations
- [ ] Add an explicit “not found” path when evidence is insufficient
- [ ] Handle document versions

### Stage 3 — Evaluation
- [ ] Create a small labelled question set
- [ ] Check whether supporting chunks appear in Top 3 / Top 5 retrieval
- [ ] Check answer faithfulness and citation correctness
- [ ] Compare an alternative chunking configuration
- [ ] Test an instruction embedded inside a source document

### Stage 4 — Recruitment coordination
- [ ] Add a separate deterministic branch for overdue interview feedback
- [ ] Use explicit date/status rules rather than an LLM for reminder decisions
- [ ] Prevent duplicate reminders

## Target architecture

The portfolio plan for the completed version is:

```text
Ingest & Parse
      ↓
Chunk + Metadata
      ↓
Create Embeddings
      ↓
Vector Store
      ↓
Retrieve
      ↓
Rerank
      ↓
Assemble Context
      ↓
Generate + Citations
      ↓
Log
      ↓
Evaluate
```

The plan also explores PostgreSQL/pgvector later. **The current prototype uses Pinecone.** I am keeping that distinction explicit rather than claiming technology that is not yet implemented.

## Evaluation plan

A future labelled set of approximately 25 fictional recruitment-policy questions will be used to check:

- whether the supporting chunk is retrieved in the Top 3 and Top 5 results
- whether the answer stays faithful to retrieved evidence
- whether citations point to the correct source
- whether the assistant abstains when the knowledge base does not contain the answer
- whether source-document instructions are treated as content rather than workflow instructions

See [evaluation/README.md](evaluation/README.md) for the planned evaluation approach.

## Planned deterministic feedback branch

The second part of the portfolio project will deliberately separate workflow logic from generative AI:

```text
Interview Date + Status
        ↓
Explicit IF / AND Rules
        ↓
Overdue?
        ↓
Draft Reminder
        ↓
Reminder Flag
        ↓
Duplicate Prevention
```

This is a design choice: document questions belong in retrieval; date/status decisions can be handled with explicit rules.

## Repository structure

```text
.
├── README.md
├── docs/
│   └── architecture.md
├── evaluation/
│   └── README.md
├── workflows/
│   └── README.md
└── .gitignore
```

The exported n8n workflow and screenshot will be added when available. Workflow exports will be checked before publishing so credentials, keys and personal data are not committed.

## Skills demonstrated by the current build

**n8n · Retrieval-Augmented Generation (RAG) · OpenAI · Pinecone · embeddings · vector retrieval · document ingestion · recursive text splitting · AI Agent workflow**

The roadmap includes technologies and evaluation work I am still developing. They are intentionally not listed here as completed skills.

## Portfolio context

This is **Project 1** in my AI Automation Engineering portfolio. The portfolio combines my current technical learning with problems connected to my previous experience in recruitment, operations and stakeholder-facing work.

My goal is to show the progression clearly: **learn → build → test → document → improve**.

## Author

**Konstantinos Kallias**  
Transitioning into AI Automation Engineering

[GitHub profile](https://github.com/KKallias) · [LinkedIn](https://www.linkedin.com/in/konstantinoskallias/)
