---
name: calibrate
description: Propose and, after explicit user confirmation, persist cross-task calibration from durable task evidence. Use after avoidable rework, a wrong default, or explicit user/reviewer feedback shows that a question was missing, should have been verified, or should not have blocked the task. This owns future-task learning, not current decisions or reviewer handoff.
---

# Calibrate

Turn explicit corrections and avoidable rework into reusable judgment for
future tasks. Calibration is optional follow-up: it never reopens or blocks the
task that produced the evidence.

## Boundaries

- [audit-choices](../audit-choices/SKILL.md) owns decisions in the current
  implementation.
- [review-guide](../review-guide/SKILL.md) owns context for an external
  reviewer.
- This skill owns only cross-task learning from durable evidence.

## Workflow

1. **Gather durable evidence.** Read the spec's choices ledger, recorded
   deviations, review findings, and explicit user corrections. Do not infer a
   reaction or failure from missing conversation memory.
2. **Separate adaptation from avoidable rework.**
   - `beneficial adaptation` — new evidence led to a better result;
   - `neutral divergence` — naming, slicing, or order changed without waste;
   - `avoidable rework` — an earlier reasonable question, verification, or
     execution step would have prevented wasted work.

   Keep beneficial adaptations in the spec rationale. Only avoidable rework
   enters the failure log.
3. **Attribute each avoidable rework item** to one primary cause:
   - `spec` — execution followed a wrong or incomplete plan;
   - `execution` — the plan was clear but implementation violated it;
   - `metacognition` — the agent missed a warranted question or fact check, or
     blocked on a decision that should have been defaulted.

   Record `too-big`, `too-small`, or `right-sized` only when delegation size
   contributed.
4. **Extract a reusable rule.** Convert explicit “you should have asked” into a
   positive question example, explicit “just do it” into a negative example,
   and missed fact checks into verify-before-asking examples. State the
   recurring situation, observable tell, and correct handling; omit
   task-specific files, functions, and chronology.
5. **Propose one compact diff** against `docs/plan/question-taste.md` and
   `docs/plan/failure-log.md`, creating them from the templates when missing.
   Sharpen an existing rule rather than stacking a near-duplicate. Present the
   proposal separately from task closeout.
6. **Persist only after explicit confirmation.** On confirmation, apply the
   diff. If the user skips or does not answer, leave the canonical files
   unchanged; the completed task remains complete.

## Templates

`question-taste.md`:

```markdown
# Question taste

## Worth blocking me

## Verify instead of asking or assuming

## Should not have been asked

## Standing defaults
```

`failure-log.md`:

```markdown
# Failure log

<!-- date | task pattern | avoidable rework | primary cause | granularity | durable lesson + evidence -->
```

## Done

Calibration is done when every proposal is grounded in durable evidence,
generalized beyond the source task, deduplicated against existing rules, and
either explicitly confirmed and persisted or left as a non-blocking proposal.
