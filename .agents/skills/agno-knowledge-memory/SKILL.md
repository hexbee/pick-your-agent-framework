---
name: agno-knowledge-memory
description: "INVOKE THIS SKILL when an Agno project needs knowledge bases, retrieval grounding, memory, sessions, or persistent context across runs."
---

<overview>
Agno separates several related context layers:

- **Knowledge**: stable external information the agent or team should search
- **Memory**: learned user or interaction context that should persist across conversations
- **Sessions/history**: prior run context and summaries that shape the current interaction

Use this skill when grounding and persistence are the real design challenge.
</overview>

<distinction-table>

| Need | Use |
|------|-----|
| Ground answers in docs, URLs, or indexed content | Knowledge |
| Preserve learned user context across runs | Memory |
| Reuse recent conversation state | Sessions/history |
| Share the same retrieval layer across an agent or team | Shared knowledge plus persistence |

</distinction-table>

---

## Knowledge Pattern

Use `Knowledge` when the app should retrieve stable domain information through a vector database or related store.

Keep knowledge sources stable, queryable, and shared where possible.

---

## Memory And Sessions Pattern

Use memory when the system should accumulate durable information about users or recurring context.

Use session history and summaries when the current run needs continuity with prior interactions, but you do not want to treat every past detail as long-term memory.

---

## Design Guidance

1. Start with knowledge when the app needs grounding in reference material.
2. Add memory only for user- or interaction-specific information worth preserving across conversations.
3. Treat sessions and summaries as runtime continuity, not as a substitute for a real knowledge base.
4. Put persistence decisions in the shared `db` layer so agents, teams, and workflows can reuse the same backing store.
5. Pair with `agno-agentos` when operators need to inspect knowledge, memory, or sessions in production.

---

## Routing

- Use `agno-fundamentals` for baseline agent construction.
- Use `agno-teams-workflows` when multi-agent or staged execution is the bigger question.
- Use `agno-agentos` when the user is asking about runtime management, inspection, or operations.

Read [references/patterns.md](references/patterns.md) for knowledge-versus-memory heuristics and persistence boundaries.
