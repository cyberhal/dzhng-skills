# After the Walk

The map lives on past planning. Three moves for the phases that follow.

- **Implementation state** (during the build) — do not start a generic running
  log. Current pickup and gates go in the durable handoff; unplanned decisions
  go in `choices.md`; newly verified territory claims update the fact ledger
  and any map entries they invalidate. A deviation can touch all three, but
  each fact is recorded once in its owner.
- **The buy-in doc** (before shipping) — other people inherit your unknowns;
  use [review-guide](../../review-guide/SKILL.md) to re-synthesize prototype,
  spec, decisions, and evidence for a named external reviewer. It is not a
  second decision audit or a routine closeout artifact.
- **Quiz before merge** (before merging someone else's or a long diff) — a
  merge-readiness report — mental model, non-obvious behaviors introduced,
  what to watch after deploy — ending in a quiz the user must pass; wrong
  answers point back to the section they skimmed.
