# Agno Knowledge, Memory, And Sessions

## Boundary Rules

- Knowledge is for stable external information.
- Memory is for learned durable user context.
- Sessions and summaries are for continuity between runs.

## Good Knowledge Signals

- the system should answer from documentation or indexed source material
- multiple agents or teams should share the same grounding layer
- retrieval quality matters more than conversational continuity

## Good Memory Signals

- the app should remember preferences, facts, or recurring user context
- future runs should benefit from what the system has learned before

## Good Session Signals

- recent history should shape the next run
- session continuity matters, but the information is not all long-term memory

## Anti-Patterns

- do not store everything as memory just because persistence is available
- do not use session history as a replacement for retrieval over real documents
- do not bury persistence logic in custom prompts when the shared database layer can handle it cleanly
