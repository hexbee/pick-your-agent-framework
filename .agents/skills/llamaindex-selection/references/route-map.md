# LlamaIndex Route Map

Use this file when one request spans multiple LlamaIndex layers.

## Fast Routes

| Request shape | Route |
|---------------|-------|
| "Set up LlamaIndex" | `llamaindex-dependencies` -> `llamaindex-fundamentals` |
| "Build RAG over docs" | `llamaindex-rag` |
| "Build an agent over docs" | `llamaindex-rag` -> `llamaindex-agents` |
| "Build a multi-step agent system" | `llamaindex-agents` -> `llamaindex-workflows` |
| "Need typed extraction from PDFs" | `llamaindex-cloud-mcp` -> `llamaindex-structured-graph` |
| "Need GraphRAG" | `llamaindex-structured-graph` -> `llamaindex-rag` |
| "Need tracing or evals" | primary build skill -> `llamaindex-observability` |

## Dominant Concern Rule

Pick the skill for the hardest current problem, not the final app label.

Examples:

- A "chatbot" task is usually `llamaindex-rag` first, not automatically `llamaindex-agents`.
- A "workflow" task that is only sequential retrieval is often still `llamaindex-rag`.
- A "graph" task that only needs typed JSON is often `llamaindex-structured-graph` without full graph indexing.

## Escalation Rule

Escalate to a second skill only after the first one exposes a real boundary:

- retrieval works, but the model must decide when to search -> add `llamaindex-agents`
- single-agent logic gets tangled -> add `llamaindex-workflows`
- text extraction is poor because source docs are messy -> add `llamaindex-cloud-mcp`
- answers are unreliable and root cause is unclear -> add `llamaindex-observability`
