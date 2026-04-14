# CrewAI

## What It Is

CrewAI is a Python framework for building flow-first AI applications with role-based agents, tasks, crews, and production-oriented workflows.

In this repository, treat CrewAI as the strongest fit when you want structured business automation or multi-step app logic where autonomous agent teams operate inside a larger workflow.

## Best For

- flow-first application architecture
- role-based multi-agent collaboration
- business workflows with typed state and routing
- production automation that mixes deterministic steps and agent work
- Python teams that want an opinionated framework surface

## Not Ideal For

- the lightest possible model-and-tool composition
- custom low-level orchestration where every edge should be hand-wired
- long-running coding or research workers centered on files and subagent systems
- retrieval-first systems where indexing and data access dominate the design

## Core Concepts

The CrewAI mental model is:

- define agents with roles, goals, tools, and optional knowledge
- define tasks with clear expected outputs
- assemble a crew for bounded collaborative work
- run that crew inside a flow when the full application needs state, routing, or resumption

The flow is the application shell. The crew is the intelligent work unit inside it.

## How It Fits In This Repository

CrewAI is covered here as a focused sub-suite:

- [crewai-selection](../../.agents/skills/crewai-selection/SKILL.md)
- [crewai-fundamentals](../../.agents/skills/crewai-fundamentals/SKILL.md)
- [crewai-flows](../../.agents/skills/crewai-flows/SKILL.md)
- [crewai-tools-mcp](../../.agents/skills/crewai-tools-mcp/SKILL.md)
- [crewai-memory-knowledge](../../.agents/skills/crewai-memory-knowledge/SKILL.md)

## Relationship to Other Frameworks

- Compared with [LangChain](./langchain.md), CrewAI is more opinionated and more workflow-oriented.
- Compared with [LangGraph](./langgraph.md), CrewAI gives you a higher-level flow-and-crew model instead of raw graph orchestration.
- Compared with [Deep Agents](./deep-agents.md), CrewAI is more app- and automation-centric, while Deep Agents is stronger for open-ended long-running work with files and delegation.
- Compared with [LlamaIndex](./llamaindex.md), CrewAI is an execution framework, while LlamaIndex is strongest as the retrieval and data layer.

## Common Upgrade Path

Start with CrewAI when:

- the app should be flow-first
- teams want role-based agents and explicit tasks
- a bounded crew should be embedded inside a broader workflow

Then add:

- LlamaIndex when grounding and retrieval become first-class concerns
- LangGraph only when the orchestration model truly needs lower-level custom control

## Where To Go Next

- Read [When to Use What](../selection/when-to-use-what.md) for scenario-based routing.
- Start with [crewai-selection](../../.agents/skills/crewai-selection/SKILL.md) if you know you want CrewAI but not which sub-path.
