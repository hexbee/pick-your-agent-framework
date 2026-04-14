# LlamaIndex

## What It Is

LlamaIndex is a framework for building retrieval, indexing, document intelligence, and data-centric agent systems.

In this repository, treat LlamaIndex as the strongest option when the hard part is giving models high-quality access to private data.

## Best For

- RAG over documents, APIs, and private knowledge
- indexing and retrieval design
- document parsing and extraction
- graph-aware retrieval and data relationships
- data-centric agents that should use retrieval as a tool

## Not Ideal For

- the simplest tool-calling assistants with no meaningful data layer
- execution systems whose main challenge is long-running planning and delegation
- orchestration-heavy apps where retrieval is only a minor feature

## Core Concepts

The LlamaIndex mental model is:

- load data
- turn data into documents and nodes
- index and store it
- retrieve relevant pieces
- synthesize the answer
- expose retrieval through query engines, chat engines, tools, agents, or workflows

This gives it a strong center of gravity around data access rather than generic agent execution.

## How It Fits In This Repository

LlamaIndex is covered as a full sub-suite because it now spans several related layers:

- setup and package selection
- core framework abstractions
- RAG
- agents
- workflows
- structured extraction and graph retrieval
- observability
- cloud and MCP integrations

The main routing entry point is:

- [llamaindex-selection](../../.agents/skills/llamaindex-selection/SKILL.md)

## Relationship to Other Frameworks

- Compared with [LangChain](./langchain.md), LlamaIndex is more specialized for retrieval and data systems.
- Compared with [LangGraph](./langgraph.md), LlamaIndex is less about orchestration and more about data access.
- Compared with [Deep Agents](./deep-agents.md), LlamaIndex is not the best top-level execution framework, but it is an excellent retrieval layer inside one.

## Common Upgrade Path

Start with LlamaIndex when:

- the app is really a private-data system
- RAG quality matters
- document parsing or extraction matters
- graph/data relationships matter

Then add:

- LangGraph if orchestration becomes custom and complex
- Deep Agents if the system grows into a long-running worker
- LangChain only when you specifically want to standardize other app primitives around it

## Where To Go Next

- Read [LangChain vs LlamaIndex](../comparisons/langchain-vs-llamaindex.md) if both feel plausible.
- Read [When to Use What](../selection/when-to-use-what.md) for scenario-based routing.
- Browse the LlamaIndex skill tree through [llamaindex-selection](../../.agents/skills/llamaindex-selection/SKILL.md).
