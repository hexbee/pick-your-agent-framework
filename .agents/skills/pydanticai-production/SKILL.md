---
name: pydanticai-production
description: "INVOKE THIS SKILL when tracing, testing, evaluating, productionizing, or making a Pydantic AI system durable. Covers Logfire, Pydantic Evals, durable execution, multi-agent reliability, and production-oriented debugging."
---

<overview>
Use observability and evaluation early.

For most production Pydantic AI systems, the hard problems are not only prompt wording. They are usually one of these:

- wrong tool choice
- bad runtime dependencies
- fragile multi-step behavior
- missing evaluation coverage
- workflows that need durability and restart safety

This skill is the production layer for Pydantic AI work.
</overview>

<debug-surface>

| Question | Inspect |
|----------|---------|
| What did the agent actually do? | Logfire traces, messages, tool calls, token usage |
| Is behavior stable across inputs? | Pydantic Evals datasets and evaluators |
| Can long-running work survive restarts or failures? | durable execution strategy |
| Are multiple agents interacting cleanly? | delegation boundaries, traces, and tool surfaces |

</debug-surface>

---

## Logfire

<python>

```python
import logfire

logfire.configure()
logfire.instrument_pydantic_ai()
```

</python>

Start here before making large prompt or architecture changes. A trace is usually more informative than another guess.

---

## Durable Execution

Pydantic AI supports durable agents for workflows that must survive transient failures, restarts, or long-running execution.

<python>

```python
from pydantic_ai import Agent
from pydantic_ai.durable_exec.prefect import PrefectAgent


agent = Agent(
    'gpt-5.2',
    instructions="You're an expert in geography.",
    name='geography',
)

prefect_agent = PrefectAgent(agent)
```

</python>

Reach for durable execution when reliability requirements are part of the product, not just a nice-to-have.

---

## Evaluation Strategy

- Use ad hoc local runs to shape the first version.
- Add Pydantic Evals when you need repeatable datasets and evaluators.
- Evaluate tool behavior and final outputs separately when possible.
- Treat multi-agent behavior as a system to trace and test, not as one giant prompt.

---

## Routing

- Use `pydanticai-fundamentals` if the production problem is really a weak core agent design.
- Use `pydanticai-tools-mcp` if traces show the real issue is tool design, dependencies, or MCP wiring.
- Use `pydanticai-dependencies` when production features depend on package or integration choices.

Read [references/eval-ops.md](references/eval-ops.md) for a staged production checklist.
