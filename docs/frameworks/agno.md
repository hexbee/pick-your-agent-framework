# Agno

## What It Is

Agno is a Python framework for building agents, teams, and workflows with built-in support for tools, memory, knowledge, sessions, and a production runtime layer through AgentOS.

In this repository, treat Agno as a strong fit when you want one framework surface that can span both agent construction and runtime operations.

## Best For

- integrated agent systems that may grow from one agent into teams and workflows
- multi-agent applications that should stay inside one framework family
- apps that need knowledge, memory, and session-aware context
- production-oriented systems that benefit from an attached runtime and control plane

## Not Ideal For

- the lightest possible model-and-tool composition
- graph-first orchestration where every edge and state transition should be hand-controlled
- retrieval-first systems where indexing and data access dominate the design
- long-running coding workers centered on files, subagents, and skill loading

## Core Concepts

The Agno mental model is:

- start with an `Agent`
- add tools, instructions, and persistence
- grow into a `Team` when multiple specialists should collaborate
- grow into a `Workflow` when execution should be staged explicitly
- add knowledge, memory, and sessions as context layers
- run and manage the system through AgentOS when it becomes an application surface

This gives Agno a more integrated center of gravity than frameworks that focus only on prompts, only on orchestration, or only on retrieval.

## How It Fits In This Repository

Agno is covered here as a focused sub-suite:

- [agno-selection](../../.agents/skills/agno-selection/SKILL.md)
- [agno-fundamentals](../../.agents/skills/agno-fundamentals/SKILL.md)
- [agno-teams-workflows](../../.agents/skills/agno-teams-workflows/SKILL.md)
- [agno-knowledge-memory](../../.agents/skills/agno-knowledge-memory/SKILL.md)
- [agno-agentos](../../.agents/skills/agno-agentos/SKILL.md)

## Relationship to Other Frameworks

- Compared with [LangChain](./langchain.md), Agno is more integrated and less primitive-first.
- Compared with [CrewAI](./crewai.md), Agno is less flow-first and more centered on a unified agent-runtime stack.
- Compared with [LangGraph](./langgraph.md), Agno is higher-level and less about hand-wiring graph logic.
- Compared with [Deep Agents](./deep-agents.md), Agno is less centered on coding-style file work and delegated worker harnesses.
- Compared with [LlamaIndex](./llamaindex.md), Agno is not the best retrieval-first framework, though it can still use knowledge and vector-backed context.

## Common Upgrade Path

Start with Agno when:

- one integrated Python framework should cover both build-time and run-time concerns
- the system may evolve from a single agent into teams or workflows
- memory, sessions, and runtime operations are part of the design from the start

Then add:

- LlamaIndex when retrieval quality or document/data access becomes the real hard problem
- LangGraph only when orchestration needs lower-level custom control than Agno's higher-level surfaces provide

## Where To Go Next

- Read [When to Use What](../selection/when-to-use-what.md) for scenario-based routing.
- Start with [agno-selection](../../.agents/skills/agno-selection/SKILL.md) if you know you want Agno but not which sub-path.
