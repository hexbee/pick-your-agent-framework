# CrewAI Memory and Knowledge Patterns

## Use Memory When

- the system learns useful facts during execution
- later steps should recall prior findings
- relevance, recency, and importance should influence recall

## Use Knowledge When

- the system should be grounded before execution starts
- the source material is relatively stable
- multiple tasks will reuse the same reference material

## Placement Rule

- use crew-level knowledge for shared context
- use agent-level knowledge for specialist context
- keep memory in the flow or runtime path when it should evolve over time
