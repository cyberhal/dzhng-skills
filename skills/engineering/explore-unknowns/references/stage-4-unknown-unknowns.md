# Stage 4 — Unknown Unknowns: Hunt the Landmines

What neither of you knows to ask, the territory often does. This stage sweeps
the code the task will touch and turns silent traps into map entries.

## Procedure

1. Sweep every file the task touches (state the coverage: "the sweep covered
   the N files this task touches"). Hunt for:
   - **Landmines** — things that bite silently: wrong-by-default data,
     stale denormalizations, filters that pass bad rows, escaping that
     corrupts output.
   - **Unwritten conventions** — rules the code enforces that no doc states.
   - **Half-built or reverted prior attempts** at the same job, and *why*
     they died — the reason is usually your landmine.
   - **Findings beyond the feature** — latent bugs the task's code path
     inherits; record the fact and expose its task impact rather than silently
     absorbing it.
2. Verify each territory finding in the
   [fact ledger](fact-ledger.md), then report it as a card: the **evidence**
   (file and line), **why it bites**, and **what it changes** about the task.
   Worst first.
3. A finding that needs a user decision closes like a stage-2 question:
   lettered options with your recommendation. A finding that only needs
   awareness stays owned by the fact ledger; the map references it as a sharp
   edge instead of copying the claim.

Remember the global rule: findings that bear on decisions already in flight
should have been disclosed when found — this stage is where the *systematic*
sweep happens, not where disclosures wait.

**Done when** the sweep has covered the code the task will touch and every
finding is routed once — decided or OPEN on the map, or verified in the fact
ledger and referenced as a sharp edge.

## Technique

- **Blindspot pass** — the sweep packaged for reaction: landmine cards, each
  with the evidence, why it bites, and a copyable prompt fix; assembled into
  one better implementation prompt at the end.
