---
name: crewai-selection
description: "INVOKE THIS SKILL at the START of any CrewAI project or question when it is not yet clear which CrewAI skill or architecture path to use. Routes between fundamentals, flows, tools/MCP, and memory/knowledge."
---

<overview>
CrewAI spans several closely related layers:

- agent, task, and crew composition
- flow-first orchestration
- tools and MCP-connected capabilities
- memory and knowledge grounding

Use this skill first when the user asks for "a CrewAI solution" but the correct sub-path is still unclear.
</overview>

<selection-table>

| If the main question is... | Go To |
|----------------------------|-------|
| How do I install CrewAI, scaffold a project, or build a first crew? | `crewai-fundamentals` |
| How do I structure a production app around `Flow`? | `crewai-flows` |
| How do I connect tools, `crewai_tools`, or MCP servers? | `crewai-tools-mcp` |
| How do I use memory, preload knowledge, or ground agents in domain data? | `crewai-memory-knowledge` |

</selection-table>

---

## Decision Process

Ask these in order:

1. Is the user still trying to understand the core `Agent` / `Task` / `Crew` model?
2. Is the real question about app structure, state, branching, or long-running execution?
3. Is the hard part external capabilities such as tools, MCP servers, or data access?
4. Is the hard part grounding and persistence rather than orchestration?

If more than one answer is yes, start with the dominant concern and then chain to the next skill.

---

## Common Routes

| User intent | Recommended route |
|-------------|-------------------|
| "Build my first CrewAI app" | `crewai-fundamentals` -> `crewai-flows` |
| "Add role-based agents to a production workflow" | `crewai-flows` -> `crewai-fundamentals` |
| "Connect GitHub, search, or local tools to agents" | `crewai-tools-mcp` -> `crewai-fundamentals` |
| "Ground the crew in company docs or reusable context" | `crewai-memory-knowledge` -> `crewai-flows` |
| "Use CrewAI with external MCP servers" | `crewai-tools-mcp` |

---

## Reference

Read [references/route-map.md](references/route-map.md) when the request spans multiple CrewAI layers and you need concrete routing examples.
