# Agno Fundamentals Architecture

## Canonical Call Chain

1. Choose a model adapter
2. Define an `Agent`
3. Add instructions and tools
4. Decide whether history, sessions, or persistence should be enabled
5. Run the agent through a direct call or inside a larger runtime

## Boundary Rules

- `Agent` is the baseline unit of behavior.
- Tools extend capability, but they do not replace agent design.
- Session and history settings shape how much prior context is reused.
- Persistence belongs in the shared storage layer, not in ad hoc prompt hacks.

## Anti-Patterns

- Do not start with teams when one agent can still solve the task clearly.
- Do not mix runtime operations concerns into a first-agent tutorial.
- Do not treat knowledge and memory as the same feature just because both add context.
