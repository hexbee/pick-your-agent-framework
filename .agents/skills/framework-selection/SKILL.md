---
name: framework-selection
description: "INVOKE THIS SKILL at the START of any LangChain, LangGraph, Deep Agents, or LlamaIndex project, before writing any agent code. Determines which framework layer is right for the task, including when to choose LlamaIndex for data-heavy RAG, document intelligence, graph retrieval, or data-centric agents, and routes to the correct next skill."
---

<overview>
LangChain, LangGraph, and Deep Agents are **layered**, while LlamaIndex is a complementary framework optimized for retrieval, document intelligence, and data-centric agent systems.

Think about them like this:

```
┌─────────────────────────────────────────────┐
│                 Deep Agents                 │  ← highest level: batteries included
│      (planning, memory, skills, files)     │
├─────────────────────────────────────────────┤
│                  LangGraph                  │  ← orchestration: graphs, loops, state
│       (nodes, edges, state, persistence)    │
├─────────────────────────────────────────────┤
│                  LangChain                  │  ← foundation: models, tools, chains
│         (models, tools, prompts, RAG)       │
└─────────────────────────────────────────────┘

┌─────────────────────────────────────────────┐
│                 LlamaIndex                  │  ← data and retrieval specialist
│  (loading, indexing, retrieval, agents,    │
│   workflows, parsing, graph/data systems)  │
└─────────────────────────────────────────────┘
```

Picking a higher layer does not cut you off from lower layers — you can use LangGraph graphs inside Deep Agents, and LangChain primitives inside both. LlamaIndex can also be mixed with all three when retrieval, indexing, document parsing, or graph-based querying is the main challenge.

> **This skill should be loaded at the top of any project before selecting other skills or writing agent code.** The framework you choose dictates which other skills to invoke next.

Read [references/selection-matrix.md](references/selection-matrix.md) when the request spans multiple frameworks or you need concrete routing examples.
</overview>

---

## Decision Guide

<decision-table>

Answer these questions in order:

| Question | Yes → | No → |
|----------|-------|-------|
| Does the task require breaking work into sub-tasks, managing files across a long session, persistent memory, or loading on-demand skills? | **Deep Agents** | ↓ |
| Is the main problem building retrieval, indexing, document parsing, graph retrieval, or question-answering over private data? | **LlamaIndex** | ↓ |
| Does the task require complex control flow — loops, dynamic branching, parallel workers, human-in-the-loop, or custom state? | **LangGraph** | ↓ |
| Is this a single-purpose agent that takes input, runs tools, and returns a result? | **LangChain** (`create_agent`) | ↓ |
| Is this a pure model call, chain, or retrieval pipeline with no agent loop? | **LangChain** (chain) | — |

</decision-table>

---

## Framework Profiles

<langchain-profile>

### LangChain — Use when the task is focused and self-contained

**Best for:**
- Single-purpose agents that use a fixed set of tools
- RAG pipelines and document Q&A
- Model calls, prompt templates, output parsing
- Quick prototypes where agent logic is simple

**Not ideal when:**
- The agent needs to plan across many steps
- State needs to persist across multiple sessions
- Control flow is conditional or iterative

**Skills to invoke next:** `langchain-models`, `langchain-rag`, `langchain-middleware`

</langchain-profile>

<langgraph-profile>

### LangGraph — Use when you need to own the control flow

**Best for:**
- Agents with branching logic or loops (e.g. retry-until-correct, reflection)
- Multi-step workflows where different paths depend on intermediate results
- Human-in-the-loop approval at specific steps
- Parallel fan-out / fan-in (map-reduce patterns)
- Persistent state across invocations within a session

**Not ideal when:**
- You want planning, file management, and subagent delegation handled for you (use Deep Agents instead)
- The workflow is straightforward enough for a simple agent

**Skills to invoke next:** `langgraph-fundamentals`, `langgraph-human-in-the-loop`, `langgraph-persistence`

</langgraph-profile>

<llamaindex-profile>

### LlamaIndex — Use when data access and retrieval are the hard part

**Best for:**
- RAG over private documents, APIs, or enterprise data
- Indexing, retrieval, and response synthesis
- Document parsing and extraction workflows
- GraphRAG or relationship-aware retrieval
- Data-centric agents that should use retrieval as a tool

**Not ideal when:**
- The main problem is long-running task execution with planning and filesystem work (use Deep Agents instead)
- The main problem is custom control flow over arbitrary steps with no strong retrieval/data layer (use LangGraph instead)
- The task is just a simple tool-calling assistant or plain model chain (use LangChain instead)

**Skills to invoke next:** `llamaindex-selection`, then one of `llamaindex-dependencies`, `llamaindex-fundamentals`, `llamaindex-rag`, `llamaindex-agents`, `llamaindex-workflows`, `llamaindex-structured-graph`, `llamaindex-observability`, or `llamaindex-cloud-mcp`

</llamaindex-profile>

<deep-agents-profile>

### Deep Agents — Use when the task is open-ended and multi-dimensional

**Best for:**
- Long-running tasks that require breaking work into a todo list
- Agents that need to read, write, and manage files across a session
- Delegating subtasks to specialized subagents
- Loading domain-specific skills on demand
- Persistent memory that survives across multiple sessions

**Not ideal when:**
- The task is simple enough for a single-purpose agent
- You need precise, hand-crafted control over every graph edge (use LangGraph directly)

**Middleware — built-in and extensible:**

Deep Agents ships with a built-in middleware layer out of the box — you configure it, you don't implement it. The following come pre-wired; you can also add your own on top:

| Middleware | What it provides | Always on? |
|------------|-----------------|------------|
| `TodoListMiddleware` | `write_todos` tool — agent plans and tracks multi-step tasks | ✓ |
| `FilesystemMiddleware` | `ls`, `read_file`, `write_file`, `edit_file`, `glob`, `grep` tools | ✓ |
| `SubAgentMiddleware` | `task` tool — delegate work to named subagents | ✓ |
| `SkillsMiddleware` | Load SKILL.md files on demand from a skills directory | Opt-in |
| `MemoryMiddleware` | Long-term memory across sessions via a `Store` instance | Opt-in |
| `HumanInTheLoopMiddleware` | Interrupt and request human approval before sensitive tool calls | Opt-in |

**Skills to invoke next:** `deep-agents-core`, `deep-agents-memory`, `deep-agents-orchestration`

</deep-agents-profile>

---

## Nested Routing for LlamaIndex

<llamaindex-nested-routing>
If the decision table points to **LlamaIndex**, do not stop there. Continue routing into the LlamaIndex skill suite:

| If the main LlamaIndex question is... | Go To |
|---------------------------------------|-------|
| package setup or version choice | `llamaindex-dependencies` |
| core abstractions and API structure | `llamaindex-fundamentals` |
| RAG, ingestion, retrieval, routing, synthesis | `llamaindex-rag` |
| tool-calling agents or multi-agent patterns | `llamaindex-agents` |
| event-driven orchestration, loops, concurrency | `llamaindex-workflows` |
| structured extraction or graph retrieval | `llamaindex-structured-graph` |
| tracing, debugging, evaluation, cost | `llamaindex-observability` |
| LlamaParse, LlamaCloud, or MCP | `llamaindex-cloud-mcp` |

When uncertain, invoke `llamaindex-selection` first and let it route within the LlamaIndex subtree.
</llamaindex-nested-routing>

---

## Mixing Layers

<mixing-layers>
Because these frameworks are complementary, they can be combined in the same project. The most common pattern is using Deep Agents as the top-level orchestrator while dropping down to LangGraph for specialized subagents. LlamaIndex often becomes the retrieval/data layer inside one of those systems.

### When to mix

| Scenario | Recommended pattern |
|----------|---------------------|
| Main agent needs planning + memory, but one subtask requires precise graph control | Deep Agents orchestrator → LangGraph subagent |
| Specialized pipeline (e.g. RAG, reflection loop) is called by a broader agent | LangGraph graph wrapped as a tool or subagent |
| High-level coordination but low-level graph for a specific domain | Deep Agents + LangGraph compiled graph as a subagent |
| Agent framework needs strong retrieval over private data | LangChain/LangGraph/Deep Agents + LlamaIndex RAG layer |
| Workflow system needs document parsing or GraphRAG | LangGraph or Deep Agents + LlamaIndex indexing/retrieval |

### How it works in practice

A LangGraph compiled graph can be registered as a subagent inside Deep Agents. This means you can build a tightly-controlled LangGraph workflow (e.g. a retrieval-and-verify loop) and hand it off to the Deep Agents `task` tool as a named subagent — the Deep Agents orchestrator delegates to it without caring about its internal graph structure.

LangChain tools, chains, and retrievers can be used freely inside both LangGraph nodes and Deep Agents tools — they are the shared building blocks at every level.

LlamaIndex query engines, retrievers, indexes, and parsing pipelines can be wrapped as tools or called from LangChain, LangGraph, or Deep Agents components when the system needs better data access than those frameworks provide out of the box.

</mixing-layers>

---

## Quick Reference

<quick-reference>

| | LangChain | LangGraph | Deep Agents | LlamaIndex |
|---|-----------|-----------|-------------|------------|
| **Primary strength** | Models, tools, chains | Orchestration and state | Long-running agent systems | Retrieval and data systems |
| **Control flow** | Fixed (tool loop) | Custom (graph) | Managed (middleware) | Moderate; retrieval-first plus agents/workflows |
| **Middleware layer** | Callbacks only | ✗ None | ✓ Explicit, configurable | Observability/settings, not middleware-first |
| **Planning** | ✗ | Manual | ✓ TodoListMiddleware | Limited; use workflows/agents as needed |
| **File management** | ✗ | Manual | ✓ FilesystemMiddleware | Data readers/loaders, not workspace files |
| **Persistent memory** | ✗ | With checkpointer | ✓ MemoryMiddleware | Storage/index persistence |
| **Subagent delegation** | ✗ | Manual | ✓ SubAgentMiddleware | AgentWorkflow / orchestration patterns |
| **On-demand skills** | ✗ | ✗ | ✓ SkillsMiddleware | ✗ |
| **Human-in-the-loop** | ✗ | Manual interrupt | ✓ HumanInTheLoopMiddleware | Via workflows or custom logic |
| **Custom graph edges** | ✗ | ✓ Full control | Limited | Not the main abstraction |
| **Best fit** | Simple agent or chain | Complex control flow | Open-ended execution | RAG, parsing, graph/data retrieval |
| **Setup complexity** | Low | Medium | Low | Medium |
| **Flexibility** | Medium | High | Medium | High in data/retrieval domain |

> **Middleware is a concept specific to LangChain (callbacks) and Deep Agents (explicit middleware layer). LangGraph has no middleware — you wire behavior directly into nodes and edges. LlamaIndex's center of gravity is retrieval/data architecture, not middleware or graph orchestration.**

</quick-reference>
