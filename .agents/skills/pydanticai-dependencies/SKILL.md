---
name: pydanticai-dependencies
description: "INVOKE THIS SKILL when setting up a new Pydantic AI project or when asked about packages, extras, providers, installation, or environment requirements. Covers `pydantic-ai`, `pydantic-ai-slim`, provider extras, `pydantic-graph`, and `pydantic-evals`."
---

<overview>
Pydantic AI is Python-first and package choices matter early.

Use this skill to choose between:

- `pydantic-ai` for the default batteries-included install
- `pydantic-ai-slim[...]` when you want a tighter dependency footprint
- `pydantic-graph` when advanced graph work becomes a first-class concern
- `pydantic-evals` when evaluation becomes part of the build loop

For most new projects, start simple and only add extras that match the provider and production features you actually use.
</overview>

<selection-guide>

| Need | Install / Package Choice |
|------|--------------------------|
| Default project setup with minimal decision overhead | `pydantic-ai` |
| Slim install with only selected providers or integrations | `pydantic-ai-slim[...]` |
| Direct access to advanced graph APIs | `pydantic-graph` |
| Dataset- and evaluator-driven testing | `pydantic-evals` |

</selection-guide>

---

## Environment Requirements

| Requirement | Guidance |
|-------------|----------|
| Python | **3.10+** |
| Package manager | `uv` preferred, `pip` acceptable |
| Provider strategy | install only the model-provider extras you need |
| Production extras | add integrations like tracing, MCP, or durable execution only when required |

---

## Package Guidance

- Prefer `pydantic-ai` when you want the simplest setup and do not care about trimming dependencies.
- Prefer `pydantic-ai-slim[...]` when you want to be explicit about providers and integrations.
- Keep provider extras narrow. Common examples in the docs include provider extras such as `openai`, `anthropic`, or `google`, and integration extras such as `logfire`, `mcp`, or `temporal`.
- Reach for `pydantic-graph` only when explicit graph authoring becomes part of the design. It is more advanced than the default Pydantic AI path.
- Add `pydantic-evals` when you need repeatable evaluation rather than ad hoc prompt testing.

---

## Minimal Installs

<python>

Default install.
```bash
uv add pydantic-ai
```

Slim install with only selected integrations.
```bash
uv add "pydantic-ai-slim[openai,logfire]"
```

Add evaluation support.
```bash
uv add pydantic-evals
```

</python>

---

## Routing

- Use `pydanticai-fundamentals` once package setup is settled and you are ready to build the first agent.
- Use `pydanticai-tools-mcp` when the next question is about tools, dependencies, or MCP servers.
- Use `pydanticai-production` when setup choices depend on tracing, durable execution, or evaluation.

Read [references/install-matrix.md](references/install-matrix.md) for a compact install matrix and recommended starter combinations.
