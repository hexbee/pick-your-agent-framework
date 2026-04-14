# Agno Teams And Workflows Patterns

## Team vs Workflow

| If the hardest part is... | Prefer |
|---------------------------|--------|
| Choosing the right specialist at runtime | `Team` |
| Keeping work in a fixed stage order | `Workflow` |
| Collaborating across roles | `Team` |
| Building a repeatable pipeline | `Workflow` |

## Good Team Signals

- specialist agents have different tools or instructions
- one lead surface should coordinate several members
- users benefit from role separation more than process diagrams

## Good Workflow Signals

- the app must move through named phases
- steps should be explicit and inspectable
- one stage's output naturally becomes the next stage's input

## Anti-Patterns

- do not use a team when one agent plus a couple of tools would be simpler
- do not use a workflow just to simulate delegation between specialists
- do not collapse every concern into the same lead agent instructions
