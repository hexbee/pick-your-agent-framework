# LlamaIndex Workflow Patterns

## Core Shapes

| Shape | When to Use |
|-------|-------------|
| Linear steps | deterministic multi-step flow |
| Branch | next step depends on validation or classification |
| Loop | retry, reflection, or corrective behavior |
| Fan-out / fan-in | parallel subtasks with collection |
| Planner / executor | explicit plan generation and execution |

## Good Workflow Boundaries

- Each step should have one clear job.
- Events should carry only the payload needed downstream.
- Shared evolving state should live in `Context`.

## Prefer Workflows Over Agents When

- branching logic is the hard part
- concurrency matters
- steps need explicit collection or join behavior
- you want deterministic control over orchestration
