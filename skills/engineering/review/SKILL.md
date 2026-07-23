---
name: review
description: Final closeout for a finished high-risk pass or integrated substantive change — sequence refactor-clean (shape), one independent diff-review lane, and write-docs (docs) into one verdict. Use when a risk-tiered workflow requires complete review, or the user asks for final review, cleanup-and-document, or “review everything.” Do not run this full stack for every low- or medium-risk pass.
---

# Review

A high-risk or final integrated change earns “done” only after three lenses
pass: its **shape**, its **diff**, and its **docs**. Each has a specialist
skill. This skill owns only what they cannot: the order, one independent diff
reviewer, the loop between lenses, and one verdict.

## Workflow

1. **Scope.** Freeze the review target and confirm why complete review is due:
   high risk, final integration, or an explicit user request. For a bounded
   medium-risk diff whose caller did not request complete review, return to the
   caller's one-reviewer gate instead of silently expanding it into this stack.
2. **Shape — [refactor-clean](../refactor-clean/SKILL.md).** Run it first, while
   restructuring is cheap. If it changes the diff, refresh the frozen target
   before independent review.
3. **Diff — choose one independent lane.** Use either one fresh subagent
   following [code-review](../code-review/SKILL.md), or one
   [Codex review](../codex/SKILL.md). Do not run both. Give it the settled diff,
   contract, and neutral risk areas without the implementer's expected answer.
   Triage every finding against code and evidence. A structural finding returns
   to step 2. Accepted fixes rerun affected gates; dismissed findings get a
   stated reason.
4. **Docs — [write-docs](../write-docs/SKILL.md).** Update the docs this change
   touched. Trace the root-to-leaf link chain and confirm the flow still reads
   in order.
5. **Report.** Give one verdict across all three lenses: what each found, what
   changed, and what remains with its reason. Done only when every lens is clean
   or resolved.

## Rules

- When you enter a pass, read its skill — the rules live there, not here.
- Order governs presentation, not disclosure: surface a finding the moment you
  hit it, even when a later pass owns it.
- Loop, don't cascade: a later fix that reopens an earlier pass returns there.
  Recheck the narrowed failed lens and affected gates; do not restart extra
  reviewers. Stop when a full pass adds nothing.
- The implementation agent is not the independent reviewer. A fresh subagent
  and Codex are alternatives, never cumulative confidence theater.
