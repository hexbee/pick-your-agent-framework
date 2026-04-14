---
name: pydanticai-tools-mcp
description: "INVOKE THIS SKILL when connecting Pydantic AI agents to function tools, dependency-injected tools, toolsets, or MCP servers. Covers `@agent.tool`, `@agent.tool_plain`, `RunContext`, `deps_type`, `toolsets`, and MCP integration."
---

<overview>
Pydantic AI gives you two closely related capability layers:

- function tools defined directly in Python
- toolsets, including MCP-backed tool sources

Use direct tools when the capability is local, explicit, and deterministic.
Use MCP when the capability lives in an external protocol-compatible server.
</overview>

<selection-guide>

| Need | Use |
|------|-----|
| Local helper with no runtime dependencies | `@agent.tool_plain` |
| Tool that needs request-scoped data | `@agent.tool` with `RunContext[...]` |
| Shared capability source | `toolsets=[...]` |
| Remote standardized tool interface | MCP server inside `toolsets` |

</selection-guide>

---

## Function Tools

<python>

```python
import random

from pydantic_ai import Agent, RunContext


agent = Agent(
    'google-gla:gemini-3-flash-preview',
    deps_type=str,
    instructions='Use tools to play the dice game and mention the player by name.',
)


@agent.tool_plain
def roll_dice() -> str:
    return str(random.randint(1, 6))


@agent.tool
def get_player_name(ctx: RunContext[str]) -> str:
    return ctx.deps
```

</python>

---

## MCP Quick Start

<python>

```python
from pydantic_ai import Agent
from pydantic_ai.mcp import MCPServer


mcp_server = MCPServer('http://localhost:8080')

agent = Agent(
    'openai:gpt-5.2',
    toolsets=[mcp_server],
)
```

</python>

The docs also expose transport-specific MCP helpers. Use the helper that matches your deployment shape rather than forcing one transport everywhere.

---

## Safety Guidance

1. Keep the tool surface narrow and role-specific.
2. Use `deps_type` for request-scoped context instead of hidden globals.
3. Treat MCP servers as external dependencies that can fail, time out, or expose more capability than you want.
4. Prefer explicit tool descriptions and names so the agent can choose correctly.

---

## Routing

- Use `pydanticai-fundamentals` when the user still needs the basic agent mental model.
- Use `pydanticai-production` when tool-heavy systems now need tracing, evals, or durable execution.
- Use `pydanticai-dependencies` if the open question is which extras or integrations need to be installed first.

Read [references/patterns.md](references/patterns.md) for direct-tool vs MCP selection guidance.
