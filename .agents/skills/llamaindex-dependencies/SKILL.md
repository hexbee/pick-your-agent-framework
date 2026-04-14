---
name: llamaindex-dependencies
description: "INVOKE THIS SKILL when setting up a new LlamaIndex Python project, choosing packages, installing integrations, or deciding how to pin LlamaIndex versions. Covers the `llama-index` umbrella package, `llama-index-core`, provider integrations, readers, vector stores, and workflow package layout."
---

<overview>
LlamaIndex ships as a namespaced package ecosystem.

Use these rules:

- Install `llama-index` for the fastest starter setup.
- Install `llama-index-core` plus only the integrations you need for production or constrained environments.
- Add provider-specific packages for LLMs, embeddings, readers, vector stores, and cloud services.
- Prefer current docs over old blog posts when package names or imports disagree.
</overview>

<install-selection>

| Need | Install |
|------|---------|
| Quick start with default OpenAI stack | `pip install llama-index` |
| Minimal custom stack | `pip install llama-index-core ...integration packages...` |
| Local models | `llama-index-llms-ollama`, `llama-index-embeddings-huggingface`, or equivalent |
| File readers | `llama-index-readers-file` and other reader packages |
| OpenAI APIs | `llama-index-llms-openai`, `llama-index-embeddings-openai` |
| Workflows only | `llama-index-core` or standalone `llama-index-workflows` |

</install-selection>

---

## Package Strategy

Follow this pattern when bootstrapping a project:

1. Start with `llama-index` if you are prototyping and want a working baseline quickly.
2. Drop down to `llama-index-core` plus targeted integrations once you know the exact LLM, embedding model, readers, and vector store.
3. Keep integration packages explicit in app dependencies so deployment stays reproducible.

The umbrella package currently includes a starter bundle, not every integration. Treat third-party vector DBs, cloud providers, and many readers as opt-in packages.

---

## Common Install Recipes

<ex-openai-starter>
<python>

Use the starter bundle when you want the shortest path to a local prototype.
```bash
pip install llama-index
```

</python>
</ex-openai-starter>

<ex-selective-install>
<python>

Install only the core runtime plus the exact providers you plan to use.
```bash
pip install \
  llama-index-core \
  llama-index-readers-file \
  llama-index-llms-ollama \
  llama-index-embeddings-huggingface
```

</python>
</ex-selective-install>

<ex-workflow-import>
<python>

Workflows can be imported from `llama_index.core.workflow` when you use `llama-index-core`.
```python
from llama_index.core.workflow import Workflow, Event, StartEvent, StopEvent, step
```

</python>
</ex-workflow-import>

---

## Import and Versioning Rules

- Prefer `llama_index.core` imports for framework primitives.
- Treat docs mentioning `ServiceContext` as older guidance; prefer `Settings`.
- Keep `llama-index-core` and first-party integration packages reasonably aligned instead of mixing very old and very new releases.
- Re-check official docs when package names, examples, or import paths look inconsistent; LlamaIndex evolves quickly.

---

## Dependency Checklist

Before writing code, answer these:

| Question | Typical Answer |
|----------|----------------|
| Which LLM provider? | OpenAI, Ollama, Anthropic-compatible integration, etc. |
| Which embedding model? | OpenAI, HuggingFace, local embedding server, etc. |
| Which data readers? | File reader, web reader, LlamaParse, SaaS connector |
| Which store? | Simple local store, vector DB, graph store, doc store |
| Are workflows needed? | If yes, ensure async-friendly runtime and workflow imports |
| Is cloud parsing or managed sync needed? | If yes, see `llamaindex-cloud-mcp` |

---

## Routing

- Use `llamaindex-fundamentals` after dependencies are chosen and you need core architecture guidance.
- Use `llamaindex-rag` for loading, ingestion, indexing, retrieval, and synthesis.
- Use `llamaindex-agents` for `FunctionAgent`, tools, state, and multi-agent patterns.
- Use `llamaindex-workflows` for `Workflow`, events, loops, concurrency, and custom orchestration.
- Use `llamaindex-cloud-mcp` for LlamaParse, LlamaCloud, and MCP integrations.

Read [references/install-matrix.md](references/install-matrix.md) for concrete package bundles and upgrade rules.
