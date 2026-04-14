---
name: agno-agentos
description: "INVOKE THIS SKILL when an Agno system should be served, monitored, or managed through AgentOS. Covers runtime setup, control plane, sessions, knowledge, memory, and production-oriented architecture."
---

<overview>
AgentOS is Agno's runtime and operations layer:

- serve agents, teams, and workflows through a FastAPI-based runtime
- configure app-level behavior around chat, memory, and databases
- inspect sessions, traces, knowledge, and memories through the control plane

Use this skill when the question is no longer just "how do I build the agent?" but "how do I run and operate the system?"
</overview>

<capabilities>

| Capability | Why it matters |
|------------|----------------|
| Runtime serving | Expose agents, teams, and workflows as an application surface |
| Control plane | Test, inspect, and manage systems from one UI |
| Session tracking | Group runs and preserve conversation state |
| Knowledge and memory management | Operate retrieval and learned context in production |
| Tracing and approvals | Observe execution and control sensitive operations |

</capabilities>

---

## Minimal Shape

At this layer, think in terms of:

1. define agents, teams, and workflows
2. attach shared databases and configuration
3. register them with `AgentOS`
4. serve the runtime and manage it through the control plane

Use AgentOS when the app should feel like a real operating surface, not just a local script.

---

## Design Guidance

1. Keep application composition clear before exposing it through AgentOS.
2. Reuse shared persistence layers so sessions, memory, and knowledge stay aligned.
3. Treat the control plane as an operations and debugging surface, not as a substitute for good architecture.
4. Route runtime management concerns here even if the underlying system also needs `Agent`, `Team`, or `Workflow` help.

---

## Routing

- Use `agno-fundamentals` for the first-agent layer.
- Use `agno-teams-workflows` when the runtime composition itself is still unclear.
- Use `agno-knowledge-memory` when persistence or grounding design needs more attention.

Read [references/architecture.md](references/architecture.md) for a runtime-oriented view of how AgentOS fits on top of Agno systems.
