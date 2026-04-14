# LlamaIndex Agent Patterns

## Pattern Selection

| Need | Pattern |
|------|---------|
| One tool-calling assistant | `FunctionAgent` |
| Several specialists with handoff | `AgentWorkflow` |
| One controller that calls specialists | orchestrator agent |
| Fully custom planning/execution | custom workflow or planner |

## Tool Rules

- Tool descriptions matter as much as tool names.
- Wrap retrieval as a tool instead of copying context into prompts.
- Use narrow tools with obvious boundaries.

## State Rules

- Store compact facts, not giant prompt transcripts.
- Use per-run state for local coordination.
- Use workflows if state transitions become the real complexity.

## Escalation Clues

Move from single agent to multi-agent when:

- tools represent distinct roles
- outputs need review/revision cycles
- one agent prompt becomes overloaded with switching instructions
