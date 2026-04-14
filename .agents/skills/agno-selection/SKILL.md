---
name: agno-selection
description: "INVOKE THIS SKILL at the START of any Agno project or question when it is not yet clear which Agno skill or architecture path to use. Routes between fundamentals, teams/workflows, knowledge/memory, and AgentOS."
---

<overview>
Agno spans several connected layers:

- single agents with models, tools, and instructions
- teams and workflows for coordinated execution
- knowledge, memory, sessions, and persistence
- AgentOS for runtime, serving, and production management

Use this skill first when the user asks for "an Agno solution" but the right sub-path is still unclear.
</overview>

<selection-table>

| If the main question is... | Go To |
|----------------------------|-------|
| How do I install Agno or build a first agent? | `agno-fundamentals` |
| How do I coordinate multiple agents or structure a workflow? | `agno-teams-workflows` |
| How do I ground agents in knowledge, persist sessions, or use memory? | `agno-knowledge-memory` |
| How do I run, serve, monitor, or manage the system with AgentOS? | `agno-agentos` |

</selection-table>

---

## Decision Process

Ask these in order:

1. Is the user still trying to understand the basic `Agent` model?
2. Is the hard part multi-agent coordination or workflow design?
3. Is grounding, recall, or persistence the main problem?
4. Is the main concern runtime operations, control plane, or serving?

If more than one answer is yes, choose the skill for the dominant concern first and then chain to the next one.

---

## Common Routes

| User intent | Recommended route |
|-------------|-------------------|
| "Build my first Agno app" | `agno-fundamentals` -> `agno-teams-workflows` if it grows beyond one agent |
| "Turn one agent into a collaborating system" | `agno-teams-workflows` -> `agno-fundamentals` |
| "Ground an Agno assistant in docs or user context" | `agno-knowledge-memory` -> `agno-fundamentals` |
| "Deploy and operate agents in production" | `agno-agentos` -> `agno-teams-workflows` if runtime structure matters |

---

## Reference

Read [references/route-map.md](references/route-map.md) when the request spans multiple Agno layers and you need concrete routing examples.
