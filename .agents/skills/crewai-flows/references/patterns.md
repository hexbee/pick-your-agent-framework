# CrewAI Flow Patterns

## Recommended Pattern

Use a flow as the outer shell and trigger a crew only for work that benefits from agent collaboration.

Good fit:

- request enters flow
- flow validates or enriches state
- one step invokes a crew for research, drafting, or analysis
- flow persists the result and continues

## Common Anti-Patterns

- putting the whole app into one oversized crew
- using many agents when one agent plus a flow step is enough
- storing derived prose instead of durable structured state
- reaching for complex crews before defining the outer workflow

## Escalation Rule

If the system mainly needs:

- branching, typed state, resumption, or external triggers -> stay in `Flow`
- role-based collaboration on a bounded task -> invoke a `Crew`
