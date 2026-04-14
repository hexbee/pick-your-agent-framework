# When to Use What

## Purpose

This page is the practical selection guide for the frameworks currently covered in this repository.

Use it when you know roughly what you want to build, but you are not yet sure which framework should be your starting point.

## Quick Rule

| If the hardest part is... | Start here |
|---------------------------|------------|
| model and tool composition | LangChain |
| one integrated agent stack plus runtime operations | Agno |
| flow-first business automation with role-based agents | CrewAI |
| orchestration, loops, and state | LangGraph |
| long-running execution, planning, files, delegation | Deep Agents |
| retrieval, indexing, parsing, private-data access | LlamaIndex |

## Scenario Guide

### Use LangChain when

- you want a simple assistant or agent
- you mostly need models, prompts, and tools
- you do not yet need custom graph orchestration

### Use Agno when

- you want one framework to cover agents, teams, workflows, and runtime operations
- the system should carry knowledge, memory, or session-aware context from the start
- a control plane and managed runtime are part of the target architecture

### Use CrewAI when

- the application should be organized around flows and crews
- role-based agents and explicit tasks are part of the design
- you want a production-friendly Python framework for automations
- agent collaboration should sit inside a broader workflow

### Use LangGraph when

- the application needs explicit branching
- the flow includes retries, reflection, or fan-out/fan-in
- state transitions are part of the core design

### Use Deep Agents when

- tasks are long-running and open-ended
- the system should manage files as working memory
- planning and subagent delegation are core requirements

### Use LlamaIndex when

- the app lives or dies on retrieval quality
- private data access is the central feature
- documents, parsing, extraction, or graph/data retrieval dominate the design

## Combination Patterns

### LangGraph + LlamaIndex

Use this when custom orchestration sits on top of a strong retrieval layer.

### CrewAI + LlamaIndex

Use this when CrewAI is the application shell, but document retrieval or private-data grounding deserves a stronger dedicated data layer.

### Deep Agents + LlamaIndex

Use this when a long-running agent system needs a serious private-data backend.

### LangChain + LlamaIndex

Use this when the app shell is simple, but retrieval still deserves a dedicated framework.

### Agno + LlamaIndex

Use this when Agno should stay the application and runtime shell, but retrieval or document grounding deserves a specialized data layer.

## Common Mis-Selections

- choosing LangChain when the real problem is document retrieval quality
- choosing Agno when one lightweight agent would already solve the problem
- choosing CrewAI when one simple tool-calling agent would be enough
- choosing LangGraph when CrewAI's flow model would already cover the workflow cleanly
- choosing LlamaIndex when the app barely has a data layer
- choosing LangGraph too early for a problem that could stay simple
- choosing Deep Agents for a task that is not actually long-running or open-ended

## Suggested Reading Order

- Read [LangChain](../frameworks/langchain.md)
- Read [Agno](../frameworks/agno.md)
- Read [CrewAI](../frameworks/crewai.md)
- Read [LangGraph](../frameworks/langgraph.md)
- Read [Deep Agents](../frameworks/deep-agents.md)
- Read [LlamaIndex](../frameworks/llamaindex.md)
- Read [LangChain vs LlamaIndex](../comparisons/langchain-vs-llamaindex.md)

## Skill Entry Points

For the current skill-based routing logic, start here:

- [framework-selection](../../.agents/skills/framework-selection/SKILL.md)
- [framework-selection reference matrix](../../.agents/skills/framework-selection/references/selection-matrix.md)

If the first answer is LlamaIndex, continue here:

- [llamaindex-selection](../../.agents/skills/llamaindex-selection/SKILL.md)

If the first answer is CrewAI, continue here:

- [crewai-selection](../../.agents/skills/crewai-selection/SKILL.md)

If the first answer is Agno, continue here:

- [agno-selection](../../.agents/skills/agno-selection/SKILL.md)
