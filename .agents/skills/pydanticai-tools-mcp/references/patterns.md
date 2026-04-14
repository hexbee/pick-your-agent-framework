# Pydantic AI Tool Patterns

Use this reference when the user knows they need capabilities beyond plain prompting.

## Decision Rule

Choose the narrowest mechanism that solves the problem:

- one local deterministic helper -> direct function tool
- request-scoped context required -> function tool with `RunContext`
- shared or remote capability source -> `toolsets`
- protocol-based interoperability -> MCP server in `toolsets`

## Good Tool Shapes

- narrow input schema
- concrete name
- description that says when to use the tool
- deterministic return values when possible

## MCP Boundaries

MCP is the right fit when:

- tools live outside the current process
- multiple clients should consume the same tool surface
- protocol-level interoperability matters more than local convenience

Stay with direct tools when:

- the logic is local Python
- you control the code directly
- the capability does not need protocol standardization

## Escalation

- wrong tool choices or debugging issues -> move to `pydanticai-production`
- basic agent shape still unclear -> move to `pydanticai-fundamentals`
