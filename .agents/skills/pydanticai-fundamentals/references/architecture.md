# Pydantic AI Architecture Patterns

Use this reference when the user knows they want Pydantic AI, but the first implementation shape is still fuzzy.

## Default Starting Point

Start with one `Agent` and add only the minimum surrounding features:

- `instructions` for role and behavior
- `output_type` when the result must be machine-readable
- 1-3 tools when the model truly needs external capability
- `deps_type` when per-run context should reach tools or dynamic instructions

## Common Patterns

### Typed extractor

Use this when the main value is reliable structured output.

Typical cases:

- extract entities from text
- classify requests into a Pydantic model
- return API-ready JSON-like structures

### Tool-backed assistant

Use this when the model should decide when to call a small set of deterministic helpers.

Typical cases:

- internal support assistant
- account-aware helper with request-scoped context
- lightweight workflow assistant

### Stateful conversation shell

Use this when the app owns conversation history and chooses what to replay.

Typical cases:

- chat UI backed by an app server
- support flows where history should be filtered or summarized

## Escalation Rules

- tools or MCP become the hard part -> move to `pydanticai-tools-mcp`
- tracing, evals, or durable execution become the hard part -> move to `pydanticai-production`
- package or extras confusion appears first -> move to `pydanticai-dependencies`
