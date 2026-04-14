# Pydantic AI Production Checklist

Use this reference when a Pydantic AI system is moving beyond a prototype.

## Staged Rollout

### 1. Local correctness

- validate the base agent behavior
- confirm typed output shape
- confirm tool descriptions and arguments

### 2. Tracing

- instrument with Logfire
- inspect messages, tool calls, latency, and token usage
- debug with traces before rewriting architecture

### 3. Evaluation

- create a representative dataset
- evaluate failure modes, not only happy paths
- separate tool behavior from final-output quality when possible

### 4. Durability

- add a durable execution layer when tasks are long-running or restart-sensitive
- choose the runtime based on operational constraints, not novelty

### 5. Multi-agent reliability

- keep delegation boundaries explicit
- make each agent's tools and instructions narrow
- trace inter-agent behavior like a distributed system

## Anti-Patterns

- using more tools instead of better tool design
- changing prompts before reading traces
- skipping evals for systems that will be regression-prone
- treating durability as optional once reliability is a product requirement
