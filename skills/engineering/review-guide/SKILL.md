---
name: review-guide
description: Write a reviewer-facing buy-in or handoff guide after final review is clean. Use when a finished change needs a named external approver, a long diff must be handed to someone who did not follow implementation, or the user explicitly asks for a pitch, explainer, merge-readiness guide, or sign-off document. Do not use for a normal diff audit or routine closeout.
---

# Review Guide

Transfer the decision surface a diff cannot show: what changed, which
alternatives lost and why, where evidence changed the plan, and exactly what an
external reviewer must approve.

## Boundaries

- [review](../review/SKILL.md) owns shape, diff, and docs quality.
- [audit-choices](../audit-choices/SKILL.md) owns the current implementation's
  decision ledger.
- This skill runs only after final review is clean and only when an external
  reviewer needs context. A normal closeout does not generate a guide.

## Workflow

1. **Fix the audience and ask.** Name the reviewer or reviewer role, the exact
   approval requested, and the immutable commit or resolved base/head commit
   range they are reviewing. If the user names a branch, resolve and record its
   current commit SHA before writing; never leave a moving branch name as the
   review target.
2. **Gather authoritative inputs.** Read the spec, choices ledger, recorded
   deviations, final review result, verification evidence, and actual diff.
   Do not reconstruct decisions from memory when durable evidence exists.
3. **Write an inverted pyramid** whose layers remain useful if the reader stops
   early:
   1. Three sentences: what changed, why, and what it touches of the reviewer's
      code or responsibility.
   2. Decision surface: key decisions, rejected alternatives, reasons, and
      evidence. Lead with what contradicts the likely mental model.
   3. Deviations: where the build left the plan and the forcing fact.
   4. Per-file guide: one line per meaningful file; mark mechanical changes as
      skippable.
   5. Verification and residual risk: what ran, what did not, and why.
   6. Sign-off matrix: reviewer, decision requested, and linked evidence.
   7. Raw artifact links: spec, ledger, diff, tests, and visual evidence.
4. **Model the reviewer from evidence.** When the reviewer is known, inspect
   when they last touched affected modules and what changed since. Add a
   “since you last touched this” section only when history proves a meaningful
   mental-model gap. Otherwise write for a codebase-familiar reviewer who did
   not follow the work.
5. **Verify the guide.** Every change claim points to the diff or a file;
   every history claim points to commits; every requested sign-off has one
   owner, one decision, and enough evidence to decide.

## Rules

- Carry the forcing fact for a deviation, not the discovery narrative.
- Compress context the reviewer likely knows; never omit a load-bearing
  decision merely because they probably know it.
- Do not use the guide to rerun code review, re-audit choices, or propose
  cross-task calibration.

## Done

The guide is done when the named reviewer can decide the requested sign-off
without reading the implementation transcript, and every claim and evidence
link resolves against the review target.
