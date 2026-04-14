# Pydantic AI Install Matrix

Use this reference when the user is still deciding what to install.

## Default Rule

Start with the smallest package set that matches the real problem:

- plain agent app: `pydantic-ai`
- dependency-sensitive service: `pydantic-ai-slim[...]`
- advanced graph authoring: add `pydantic-graph`
- evaluation workflow: add `pydantic-evals`

## Common Starting Points

| Project shape | Recommended baseline |
|---------------|----------------------|
| First typed Python agent | `pydantic-ai` |
| Service pinned to one provider and one tracing stack | `pydantic-ai-slim[...]` with only needed extras |
| Tool-heavy service with MCP | `pydantic-ai-slim[...]` plus the MCP extra |
| Durable or workflow-backed service | base package plus the durable-execution integration you actually use |
| Team that wants formal evals early | base package plus `pydantic-evals` |

## Upgrade Rule

Add packages when a real boundary appears:

- provider not installed -> add that provider extra
- tracing needed -> add the Logfire integration
- MCP server/client support needed -> add the MCP integration
- durable execution needed -> add the durable-execution integration
- repeatable quality testing needed -> add `pydantic-evals`

Do not front-load every extra into a small project.
