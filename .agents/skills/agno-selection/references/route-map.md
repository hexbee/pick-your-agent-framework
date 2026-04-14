# Agno Route Map

Use this file when an Agno question touches more than one sub-area.

## Typical Routes

| Request shape | Start here | Then |
|---------------|------------|------|
| "Create my first Agno agent" | `agno-fundamentals` | `agno-teams-workflows` if it grows beyond one agent |
| "Build a multi-agent research system" | `agno-teams-workflows` | `agno-knowledge-memory` if grounding or persistence matters |
| "Add retrieval and user memory" | `agno-knowledge-memory` | return to `agno-fundamentals` for single-agent wiring |
| "Serve agents, teams, and workflows as an app" | `agno-agentos` | add `agno-teams-workflows` if runtime composition is still unclear |

## Escalation Rule

Start with `agno-fundamentals` only when the user still needs the core object model.

If the user already understands `Agent`, route directly to:

- `agno-teams-workflows` for collaboration and orchestration
- `agno-knowledge-memory` for grounding, sessions, and persistence
- `agno-agentos` for production runtime and management
