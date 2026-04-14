---
name: framework-selection
description: "INVOKE THIS SKILL at the START of any LangChain, Pydantic AI, LangGraph, Deep Agents, CrewAI, LlamaIndex, or Agno project, before writing agent code. Determines which framework is the right starting point and routes to the correct next skill."
---

<overview>
LangChain, LangGraph, and Deep Agents are **layered**, while Pydantic AI, CrewAI, LlamaIndex, and Agno are complementary frameworks with different centers of gravity:

```
┌─────────────────────────────────────────────┐
│                 Deep Agents                 │  ← highest level: long-running work
│      (planning, memory, skills, files)     │
├─────────────────────────────────────────────┤
│                  LangGraph                  │  ← orchestration: graphs, loops, state
│       (nodes, edges, state, persistence)    │
├─────────────────────────────────────────────┤
│                  LangChain                  │  ← foundation: models, tools, chains
│         (models, tools, prompts, RAG)       │
└─────────────────────────────────────────────┘

┌─────────────────────────────────────────────┐
│                   CrewAI                    │  ← flow-first multi-agent automation
│   (flows, crews, tasks, tools, MCP, ops)   │
└─────────────────────────────────────────────┘

┌─────────────────────────────────────────────┐
│                Pydantic AI                  │  ← typed Python agent framework
│ (typed output, tools, deps, MCP, evals,    │
│   observability, durable execution)        │
└─────────────────────────────────────────────┘

┌─────────────────────────────────────────────┐
│                 LlamaIndex                  │  ← data and retrieval specialist
│  (loading, indexing, retrieval, agents,    │
│   workflows, parsing, graph/data systems)  │
└─────────────────────────────────────────────┘

┌─────────────────────────────────────────────┐
│                    Agno                     │  ← integrated agent/runtime stack
│ (agents, teams, workflows, knowledge,      │
│  memory, sessions, AgentOS runtime)        │
└─────────────────────────────────────────────┘
```

Use this skill before selecting sub-skills or writing framework-specific code.

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
| Is the app best served by one integrated framework spanning agents, teams, workflows, persistence, and a runtime/control-plane layer? | **Agno** | ↓ |
| Is the app best described as flow-first automation with role-based agents, explicit tasks, and crews inside a broader Python workflow? | **CrewAI** | ↓ |
| Is the app best described as a typed Python agent service with explicit tools, dependency injection, structured output, and production tracing/evals without graph-first orchestration? | **Pydantic AI** | ↓ |
| Does the task require complex control flow such as loops, dynamic branching, parallel workers, human-in-the-loop, or custom state? | **LangGraph** | ↓ |
| Is this a single-purpose agent that takes input, runs tools, and returns a result? | **LangChain** (`create_agent`) | ↓ |
| Is this a pure model call, chain, or retrieval pipeline with no agent loop? | **LangChain** (chain) | — |

</decision-table>

---

## Framework Profiles

### LangChain — Use when the task is focused and self-contained

**Best for:**
- single-purpose agents that use a fixed set of tools
- RAG pipelines and document Q&A
- model calls, prompt templates, output parsing
- quick prototypes where agent logic is simple

**Not ideal when:**
- the agent needs to plan across many steps
- state needs to persist across multiple sessions
- control flow is conditional or iterative

**Skills to invoke next:** `langchain-dependencies`, `langchain-fundamentals`, `langchain-middleware`, `langchain-rag`

### Pydantic AI — Use when you want typed Python agents with explicit boundaries

**Best for:**
- Python-first agent services with structured or validated outputs
- tool-driven apps that benefit from dependency injection and request-scoped context
- production-oriented systems that want tracing, evals, and durable execution without starting from a graph model
- teams that like a FastAPI-style developer experience for agent code

**Not ideal when:**
- graph orchestration, branching, or state machines are the real hard problem
- the main problem is retrieval architecture rather than agent/service ergonomics
- the application is primarily a flow/task/crew system

**Skills to invoke next:** `pydanticai-dependencies`, `pydanticai-fundamentals`, `pydanticai-tools-mcp`, `pydanticai-production`

### CrewAI — Use when the app should be flow-first and role-based

**Best for:**
- production-oriented Python automations
- role-based agents working through explicit tasks
- crews embedded inside a broader application workflow
- tools, MCP connectivity, and operational workflows around agent work

**Not ideal when:**
- one simple tool-calling agent would already solve the problem
- you want low-level custom control over every orchestration edge
- the task is really retrieval-first rather than workflow-first

**Skills to invoke next:** `crewai-selection`, then one of `crewai-fundamentals`, `crewai-flows`, `crewai-tools-mcp`, or `crewai-memory-knowledge`

### Agno — Use when you want one framework to cover build and runtime concerns

**Best for:**
- integrated agent systems that may grow into teams and workflows
- apps that need knowledge, memory, sessions, and runtime operations in one stack
- production-oriented systems that benefit from a control plane and managed runtime

**Not ideal when:**
- one lightweight tool-calling agent would already solve the problem
- you want low-level custom orchestration over every branch and state edge
- the main problem is retrieval quality rather than integrated agent/runtime design

**Skills to invoke next:** `agno-selection`, then one of `agno-fundamentals`, `agno-teams-workflows`, `agno-knowledge-memory`, or `agno-agentos`

### LangGraph — Use when you need to own the control flow

**Best for:**
- agents with branching logic or loops
- multi-step workflows where different paths depend on intermediate results
- human-in-the-loop approval at specific steps
- parallel fan-out / fan-in patterns
- persistent state across invocations within a session

**Not ideal when:**
- you want planning, file management, and subagent delegation handled for you
- the workflow is straightforward enough for a higher-level abstraction

**Skills to invoke next:** `langgraph-fundamentals`, `langgraph-human-in-the-loop`, `langgraph-persistence`

### Deep Agents — Use when the task is open-ended and multi-dimensional

**Best for:**
- long-running tasks that require a todo list
- agents that need to read, write, and manage files across a session
- delegating subtasks to specialized subagents
- loading domain-specific skills on demand
- persistent memory that survives across multiple sessions

**Not ideal when:**
- the task is simple enough for a single-purpose agent
- you need precise, hand-crafted control over every graph edge

**Skills to invoke next:** `deep-agents-core`, `deep-agents-memory`, `deep-agents-orchestration`

### LlamaIndex — Use when data access and retrieval are the hard part

**Best for:**
- RAG over private documents, APIs, or enterprise data
- indexing, retrieval, and response synthesis
- document parsing and extraction workflows
- GraphRAG or relationship-aware retrieval
- data-centric agents that should use retrieval as a tool

**Not ideal when:**
- the main problem is long-running task execution with planning and filesystem work
- the main problem is custom control flow over arbitrary steps with no strong retrieval/data layer
- the task is just a simple tool-calling assistant or plain model chain

**Skills to invoke next:** `llamaindex-selection`, then one of `llamaindex-dependencies`, `llamaindex-fundamentals`, `llamaindex-rag`, `llamaindex-agents`, `llamaindex-workflows`, `llamaindex-structured-graph`, `llamaindex-observability`, or `llamaindex-cloud-mcp`

---

## Nested Routing

### If the answer is CrewAI

| If the main CrewAI question is... | Go To |
|-----------------------------------|-------|
| package setup, CLI, or first project | `crewai-fundamentals` |
| flow-first app structure and state | `crewai-flows` |
| tools, `crewai_tools`, or MCP | `crewai-tools-mcp` |
| memory, recall, or knowledge sources | `crewai-memory-knowledge` |

When uncertain, invoke `crewai-selection` first and let it route within the CrewAI subtree.

### If the answer is Pydantic AI

| If the main Pydantic AI question is... | Go To |
|----------------------------------------|-------|
| package setup, extras, or providers | `pydanticai-dependencies` |
| first agent, output types, or message history | `pydanticai-fundamentals` |
| tools, `RunContext`, toolsets, or MCP | `pydanticai-tools-mcp` |
| tracing, evals, durable execution, or multi-agent reliability | `pydanticai-production` |

### If the answer is Agno

| If the main Agno question is... | Go To |
|---------------------------------|-------|
| package setup, first agent, or baseline architecture | `agno-fundamentals` |
| multi-agent coordination or staged execution | `agno-teams-workflows` |
| knowledge bases, memory, sessions, or persistence | `agno-knowledge-memory` |
| runtime serving, control plane, or operations | `agno-agentos` |

When uncertain, invoke `agno-selection` first and let it route within the Agno subtree.

### If the answer is LlamaIndex

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

---

## Mixing Frameworks

These frameworks can be combined, but only after a primary framework has been chosen for the dominant concern.

| Scenario | Recommended pattern |
|----------|---------------------|
| Main system needs planning + memory, but one subtask requires graph control | Deep Agents orchestrator -> LangGraph subagent |
| Typed Python agent shell needs stronger private-data retrieval | Pydantic AI + LlamaIndex |
| App shell is flow-first, but retrieval over private docs is the real data challenge | CrewAI + LlamaIndex |
| Simple app shell, but retrieval still deserves a dedicated layer | LangChain + LlamaIndex |
| Custom orchestration sits on top of a serious retrieval backend | LangGraph + LlamaIndex |
| Integrated agent/runtime stack, but retrieval becomes the real hard backend | Agno + LlamaIndex |

Start with one framework. Add a second only when a real boundary appears.

---

## Quick Reference

| | LangChain | Pydantic AI | CrewAI | LangGraph | Deep Agents | LlamaIndex | Agno |
|---|-----------|-------------|--------|-----------|-------------|------------|------|
| **Primary strength** | Models, tools, chains | Typed Python agents | Flow-first automations | Orchestration and state | Long-running agent systems | Retrieval and data systems | Integrated agent/runtime stack |
| **Control flow** | Fixed tool loop | Agent loop with typed boundaries | Managed by flows | Custom graph | Managed by middleware | Moderate; retrieval-first plus agents/workflows | Agent/team/workflow surfaces |
| **Built-in collaboration model** | Light | Light; multi-agent patterns available | Crews and tasks | Manual | Subagents | Agent/workflow patterns | Teams |
| **Planning** | ✗ | ✗ | Optional crew planning | Manual | ✓ Built in | Limited; use workflows/agents as needed | Limited; use teams/workflows as needed |
| **File-centered work** | ✗ | Possible, but not the center | Possible, but not the center | Manual | ✓ Strong fit | Data loaders, not workspace files | Possible, but not the center |
| **MCP / external tools** | Via integrations | ✓ First-class via tools, toolsets, and MCP | ✓ First-class option | Manual integration | Via tools/subagents | Via adapters/tools | Via tool ecosystem and integrations |
| **Best fit** | Simple assistant or chain | Typed Python agent service | Workflow automation with agent teams | Complex control flow | Open-ended execution | RAG, parsing, graph/data retrieval | Agents that should grow into a managed runtime |
| **Setup complexity** | Low | Low-Medium | Medium | Medium | Low | Medium | Medium |
