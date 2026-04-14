# CrewAI Route Map

Use this file when a CrewAI question touches more than one sub-area.

## Typical Routes

| Request shape | Start here | Then |
|---------------|------------|------|
| "Create my first crew" | `crewai-fundamentals` | `crewai-flows` if it should become a real app |
| "Build a workflow with branching and state" | `crewai-flows` | embed crews for complex steps |
| "Add search, file, or browser capabilities" | `crewai-tools-mcp` | then return to `crewai-fundamentals` |
| "Connect MCP servers to an agent" | `crewai-tools-mcp` | add `crewai-flows` if the app needs orchestration |
| "Ground the crew in company information" | `crewai-memory-knowledge` | use `crewai-flows` for durable execution |

## Escalation Rule

Start with `crewai-fundamentals` only when the user still needs the core object model.

If the user already knows `Agent`, `Task`, and `Crew`, route directly to:

- `crewai-flows` for orchestration
- `crewai-tools-mcp` for capability access
- `crewai-memory-knowledge` for grounding and persistence
