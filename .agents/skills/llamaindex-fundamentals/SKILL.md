---
name: llamaindex-fundamentals
description: "INVOKE THIS SKILL when writing ANY LlamaIndex Python framework code. Covers the core abstractions and call chain: `Document`, `Node`, readers, `Settings`, indexes, retrievers, query engines, chat engines, tools, and storage."
---

<overview>
Think about LlamaIndex as a layered pipeline:

`load data -> transform into nodes -> index/store -> retrieve -> synthesize -> expose as query/chat/tool/agent`

The framework is most effective when you keep these responsibilities separate instead of jumping directly from raw files to an agent.
</overview>

<core-abstractions>

| Abstraction | Purpose |
|-------------|---------|
| `Document` | Raw source content plus metadata |
| `Node` | Chunked or transformed unit used for retrieval and synthesis |
| Reader | Load data from files, web pages, APIs, SaaS, or cloud |
| `Settings` | Global defaults for LLM, embeddings, parser, callbacks |
| Index | Organize nodes for retrieval or summarization |
| Retriever | Return candidate nodes for a query |
| Query Engine | Question-answering interface over an index or retriever |
| Chat Engine | Multi-turn conversational interface |
| Tool | Make query engines, functions, or APIs usable by agents |
| `StorageContext` | Bundle vector, doc, and index stores for persistence |

</core-abstractions>

---

## Core Design Rules

1. Configure shared defaults in `Settings`, then override locally only where necessary.
2. Keep ingestion logic separate from querying logic.
3. Treat `QueryEngine` as the standard read interface for RAG-style QA.
4. Treat `ChatEngine` as a conversational wrapper, not a replacement for retrieval design.
5. Wrap query engines as tools when an agent should use retrieval selectively.

---

## Minimal Skeleton

<ex-basic-index>
<python>

Build the canonical load-index-query flow.
```python
from llama_index.core import Settings, SimpleDirectoryReader, VectorStoreIndex
from llama_index.llms.openai import OpenAI
from llama_index.embeddings.openai import OpenAIEmbedding

Settings.llm = OpenAI(model="gpt-4.1")
Settings.embed_model = OpenAIEmbedding(model="text-embedding-3-small")

documents = SimpleDirectoryReader("data").load_data()
index = VectorStoreIndex.from_documents(documents)

query_engine = index.as_query_engine()
response = query_engine.query("What is in these files?")
print(response)
```

</python>
</ex-basic-index>

---

## Query Surfaces

<query-surface-selection>

| Need | Use |
|------|-----|
| One-shot QA over indexed data | `index.as_query_engine()` |
| Conversational QA with memory/history | `index.as_chat_engine()` |
| Retrieval as part of a larger agent | `QueryEngineTool` or custom tool wrapper |
| Full custom retrieval pipeline | Explicit retriever + response synthesizer |

</query-surface-selection>

---

## Persistence Pattern

<ex-persist-index>
<python>

Persist a local index and reload it later.
```python
from llama_index.core import StorageContext, load_index_from_storage

index.storage_context.persist(persist_dir="./storage")

storage_context = StorageContext.from_defaults(persist_dir="./storage")
restored_index = load_index_from_storage(storage_context)
```

</python>
</ex-persist-index>

Use explicit stores when you need a real vector DB, graph store, document store, or remote persistence.

---

## Migration Guidance

- Prefer `Settings` over `ServiceContext`.
- Prefer current workflow and agent APIs over very old `AgentRunner` era examples.
- Treat the official docs as source of truth when older notebooks conflict with current imports.

---

## Routing

- Use `llamaindex-rag` when the main problem is ingestion, retrieval, routing, or response synthesis.
- Use `llamaindex-agents` when the main problem is tool-calling agents or multi-agent design.
- Use `llamaindex-workflows` when you need event-driven orchestration, loops, or concurrency.
- Use `llamaindex-structured-graph` for structured extraction, typed outputs, or graph retrieval.

Read [references/architecture.md](references/architecture.md) for a fuller call-chain walkthrough and common design boundaries.
