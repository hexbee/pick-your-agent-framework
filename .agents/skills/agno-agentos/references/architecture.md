# Agno AgentOS Architecture

## Runtime Shape

1. Build agents, teams, or workflows
2. Attach shared persistence and configuration
3. Register them with `AgentOS`
4. Serve the runtime
5. Operate it through the control plane and API resources

## Core Managed Resources

- Agents
- Teams
- Workflows
- Sessions
- Memory
- Knowledge
- Evals

## Boundary Rules

- AgentOS is the runtime layer, not a replacement for good agent design.
- Sessions, memory, and knowledge should be configured coherently around shared storage.
- Control-plane visibility is most useful when agents and workflows already have clear responsibilities.
