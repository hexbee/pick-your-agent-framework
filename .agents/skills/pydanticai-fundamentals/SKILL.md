---
name: pydanticai-fundamentals
description: "INVOKE THIS SKILL when building a basic Pydantic AI agent. Covers `Agent`, `instructions`, typed output, basic tools, `RunContext`, message history, and the default single-agent path."
---

<overview>
Pydantic AI centers the `Agent` class.

The default mental model is:

- define an `Agent`
- give it `instructions`
- add tools only when needed
- use typed output when downstream code depends on structure
- pass dependencies through `deps_type` instead of hiding runtime state in globals

Start here for most first-agent questions.
</overview>

<core-shapes>

| Need | Use |
|------|-----|
| A basic agent with no tool calls | `Agent(...).run_sync(...)` or `await agent.run(...)` |
| Structured output | `output_type=...` |
| A tool with no runtime dependencies | `@agent.tool_plain` |
| A tool that needs per-run dependencies | `@agent.tool` with `RunContext[...]` |
| Conversation continuity | carry message history between runs |

</core-shapes>

---

## Basic Typed Agent

<python>

```python
from pydantic import BaseModel
from pydantic_ai import Agent


class CityInfo(BaseModel):
    city: str
    country: str
    summary: str


agent = Agent(
    'openai:gpt-5.2',
    instructions='Answer as a concise geography assistant.',
    output_type=CityInfo,
)

result = agent.run_sync('Tell me about Paris.')
print(result.output.country)
```

</python>

---

## Tool With Dependencies

<python>

```python
from dataclasses import dataclass

from pydantic_ai import Agent, RunContext


@dataclass
class UserContext:
    customer_tier: str


agent = Agent(
    'openai:gpt-5.2',
    deps_type=UserContext,
    instructions='Use tools when account context matters.',
)


@agent.tool
def get_customer_tier(ctx: RunContext[UserContext]) -> str:
    return ctx.deps.customer_tier
```

</python>

---

## Guidance

- Use typed output when another function, API, or UI depends on structured fields.
- Add tools sparingly. Prefer a small, well-described tool set over a large generic bundle.
- Put request-scoped data in `deps_type`, not module globals.
- Treat message history as application state you choose to persist and replay intentionally.

---

## Routing

- Use `pydanticai-dependencies` if the real question is still package setup.
- Use `pydanticai-tools-mcp` when the hard part becomes tools, `RunContext`, toolsets, or MCP.
- Use `pydanticai-production` when tracing, evals, durable execution, or production reliability become the next bottleneck.

Read [references/architecture.md](references/architecture.md) for the main single-agent patterns and escalation points.
