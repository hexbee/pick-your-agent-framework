---
name: llamaindex-selection
description: "INVOKE THIS SKILL at the START of any LlamaIndex project or question when it is not yet clear which LlamaIndex skill, architecture path, or product layer to use. Routes between dependencies, fundamentals, RAG, agents, workflows, structured/graph, observability, and cloud/MCP."
---

<overview>
LlamaIndex now spans multiple layers:

- core framework primitives
- RAG components
- agents
- event-driven workflows
- structured extraction and graph retrieval
- observability and evaluation
- LlamaParse, LlamaCloud, and MCP

Use this skill first when the user asks for "a LlamaIndex solution" but the correct path is still ambiguous.
</overview>

<selection-table>

| If the main question is... | Go To |
|----------------------------|-------|
| How do I install or choose packages? | `llamaindex-dependencies` |
| What are the main abstractions and imports? | `llamaindex-fundamentals` |
| How do I build retrieval over documents or data? | `llamaindex-rag` |
| How do I build a tool-calling agent? | `llamaindex-agents` |
| How do I orchestrate loops, branches, or concurrency? | `llamaindex-workflows` |
| How do I get typed output or graph-style retrieval? | `llamaindex-structured-graph` |
| How do I debug or evaluate the system? | `llamaindex-observability` |
| Should I use LlamaParse, LlamaCloud, or MCP? | `llamaindex-cloud-mcp` |

</selection-table>

---

## Decision Process

Ask these in order:

1. Is the problem mostly package/setup related?
2. Is the main deliverable retrieval over private data?
3. Is the hard part tool use or autonomous decision-making?
4. Is the hard part orchestration and state flow rather than agent reasoning?
5. Does the result need a schema or relationship traversal?
6. Is parsing, managed sync, or protocol-level tool interoperability the real bottleneck?

If more than one answer is yes, choose the first skill for the dominant concern and then chain to the next one.

---

## Common Routes

| User intent | Recommended route |
|-------------|-------------------|
| "Build a chatbot over my docs" | `llamaindex-rag` -> `llamaindex-agents` if tool use is needed |
| "Build a multi-step research agent" | `llamaindex-agents` -> `llamaindex-workflows` |
| "Need GraphRAG or entity relationships" | `llamaindex-structured-graph` -> `llamaindex-rag` |
| "Need better PDF extraction first" | `llamaindex-cloud-mcp` -> `llamaindex-rag` |
| "Need evals and tracing" | `llamaindex-observability` after the main build skill |

---

## Reference

Read [references/route-map.md](references/route-map.md) when the user request spans multiple LlamaIndex layers and you need concrete routing examples.
