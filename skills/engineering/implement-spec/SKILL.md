---
name: implement-spec
description: Implement an existing spec to completion through committed, independently verified passes while maintaining its decision ledger and living handoff. Use for long or multi-pass specs that need parallel slices, maintenance checkpoints, risk-tiered review, visual-wave gates, or fresh-session continuation before context drift accumulates.
---

# Implement Spec

Build the active spec to completion, one reviewable pass at a time. The spec is
the source of truth, but the architecture is allowed to improve when the code
teaches you the plan is stale.

A pass (usually one slice) is a **commit checkpoint, not a stopping point.** The
job is the whole spec — every slice, every global TODO — not the first green
commit. Finishing a pass means starting the next one, not handing back to the
user. Only stop when the spec is fully implemented (or a genuine blocker needs a
decision only the user can make).

**Work in parallel wherever the graph allows.** Do not walk the ladder one slice
at a time when slices are independent. Read the spec's dependency graph as a
wavefront and **delegate independent passes to subagents that run concurrently**
(see Rules) — you orchestrate and integrate; only serialize what genuinely
depends on prior work.

## Workflow

1. Read the repo README, the spec README, and the next slice before editing.
   Load any skills named by the spec. Identify the current pickup point, global
   TODOs, required gates, and what must stay green. Give the pass a provisional
   risk tier using step 6. If a multi-slice spec lacks a live handoff prompt,
   add one before the first pass ends.
2. Reconcile the plan with the current code. If the slice would preserve a
   development-only shim, duplicated type, weak wrapper, or obsolete path,
   replace it with the simpler architecture and update the spec handoff.
   Type every newly exposed unknown before acting: verify a code fact against
   the territory; ask or default a product semantic, compatibility edge, or
   failure policy according to flip cost; follow repo convention for a
   low-cost detail. Record defaults that future passes must inherit.
3. Implement one coherent pass: usually one slice, one vertical checkpoint, or
   one architecture correction. Keep the review surface small enough to audit.
4. Verify the actual contract. For behavior changes, run the focused unit tests
   first; for browser-visible work, use the real browser/harness and inspect
   screenshots so the subject is framed and readable, not merely nonblank.
   A visual change also needs a byte/pixel diff against the pre-change baseline
   on the production route and current candidate captures for its visual wave;
   include the user's reported framing when the work answers their bug report.
   The independent visual critique happens once at the wave boundary in step 7,
   not once per slice. A claim of passing requires the verifying command run in
   this pass with its output in hand — “should pass,” a previous run, or a
   delegate's report never substitutes.
   Never weaken an existing default gate or repin a failing contract without
   proving the old contract is wrong.
5. **Review the change list and clean up after every pass, before committing.**
   Read `git status`/`git diff --stat` line by line and account for every path:
   one-off probes, shot scripts, scratch files, `nohup.out`, ad-hoc screenshot
   dirs, and SPIKE/debug notes never enter a commit — scratch stays out of the
   tree; review evidence belongs in the spec's `assets/`; anything else gets
   deleted. A file you can't name the durable purpose of does not ship.
   Delegated agents leak these; the integrating reviewer re-checks the merged
   tree with the same eye.
6. **Confirm the pass risk from the actual diff, then spend one review budget.**
   Classify upward when uncertain; a delegated implementer never counts as the
   independent reviewer.
   - **Low risk** — mechanical, local, reversible work with no shared behavior,
     persistent data, security boundary, or public contract. Run focused gates
     and a local diff/shape/docs check. Do **not** start an independent reviewer.
   - **Medium risk** — bounded behavior, UI, internal API, or nontrivial logic
     whose failure is contained and reversible. Choose exactly one independent lane:
     either one fresh subagent following
     [code-review](../code-review/SKILL.md), or one
     [Codex review](../codex/SKILL.md). Never stack both.
   - **High risk** — security, auth, privacy, permissions, destructive or
     persistent data changes, migrations, public/external contracts or
     compatibility, cross-service contracts, concurrency/safety invariants,
     hard rollback, or broad blast radius. Run the complete
     [review](../review/SKILL.md); its diff lens uses
     exactly one independent lane, fresh subagent or Codex, not both.

   Apply every accepted finding, state why any finding is dismissed, rerun
   affected checks, and repeat only the narrowed failed lens — not the entire
   reviewer stack.
7. **Close a visual wave once.** When this pass integrates the last slice in a
   coherent visual wave, run one unprimed
   [screenshot-critique](../../visual/screenshot-critique/SKILL.md) over the
   wave's current full shots and key crops. Do not run a fresh critique for
   every contributing slice. Apply its actionable findings and rerun affected
   gates before accepting the wave. A user-reported visual bug is not “fixed”
   before this wave gate passes.
8. Run [audit-choices](../audit-choices/SKILL.md) on decisions introduced by
   this pass where the spec was silent, including delegated agents' decisions
   found during integration. Append only those choices to
   `specs/<feature>/choices.md`; the audit changes no code. Redo unsound choices
   from their corrected decisions and take the reversible provisional call for
   needs-user entries without blocking the run. Rerun affected checks, then
   commit only the focused changes from this pass.
9. **Maintain the durable handoff at two resolutions.** After every pass,
   update its compact status, completed commit, gate result, and exact next
   pickup. After every two or three completed slice commits — or sooner after a
   red pass, rebase, resume, compaction, feature-area change, or contradicted
   plan — rewrite the full “Next Agent Prompt” with:
   - branch/base and current commit;
   - completed slices and exact next slice;
   - locked decisions, defaults, and plan deviations;
   - gates run with current evidence;
   - blockers, warnings, and any uncommitted state.

   This is pickup state, not a transcript. It is durable only when a fresh
   agent can choose the same next action without conversation history.
10. Run a **maintenance checkpoint** with each full handoff refresh. Clean both
    plan and code before more feature work:
    - Keep one current pickup, one priority order, and one compact evidence
      ledger; move play-by-play into slice files or assets.
    - Correct completed/rejected/next markers; delete stale TODOs, acceptance
      claims, duplicated status sections, and obsolete prompts.
    - Re-rank remaining work so the next red/high-risk contract is explicit.
    - Reslice any still-red, overloaded, or foggy slice before implementing
      past it.
    - Delete or collapse scaffolding that no longer owns a real contract.

    Commit the checkpoint as a focused pass when it materially changes the
    spec, code shape, or pickup state. If context is compacted or costly to
    reconstruct, the work changes feature area, or the current session's
    mental model conflicts with durable state, let a fresh session continue
    from this checkpoint when the harness supports it. Session turnover is
    continuation, not task completion; the next session re-reads the handoff
    instead of inheriting oral history.
11. **Continue.** If any slice or global TODO is open, return to step 1 in the
    current or fresh session without pausing for acknowledgement. Keep looping
    until every TODO is closed.
12. **Run final integration once.** Run complete
    [review](../review/SKILL.md) over the spec's full diff, even when every
    individual pass was low or medium risk. This is the only scope where
    cross-slice duplication, emergent shape problems, and increment-shaped docs
    are visible. If the feature has a visual surface, run one final
    [screenshot-critique](../../visual/screenshot-critique/SKILL.md) over the
    integrated final state, separate from the last wave critique. Apply fixes,
    rerun gates, and commit.
13. **Consolidate the choices ledger, then route closeout by owner.** When the
   last slice lands, the
   `choices.md` you've been appending to per pass is build-order sediment: entries
   banked early carry "provisional — revisit in slice N" verdicts that a later pass
   silently resolved, entries a later pass reverted still sit there, and the same
   choice may appear twice. The per-pass rule "banked is settled, never re-listed"
   is what let that drift accumulate — so the final consolidation is its deliberate
   exception. Before archiving, **rewrite `choices.md` from scratch** as the final
   ledger: re-audit every banked choice against the **final shipped code** (not the
   pass it landed in), collapse each provisional/needs-later entry to its actual
   end state, drop anything a later pass superseded or reverted, and merge
   duplicates. Keep it **choices only** — no gate results, e2e evidence, or
   review-finding narration; those are reported elsewhere and are not decisions the
   user now owns. Present it per [audit-choices](../audit-choices/SKILL.md): grouped
   by verdict, ranked least-confident-first, every entry ELI5 and standalone.
   Then:
   - use [review-guide](../review-guide/SKILL.md) only when a named external
     approver or explicit reviewer handoff requires it;
   - archive the implementation rationale with
     [close-spec](../close-spec/SKILL.md);
   - offer [calibrate](../calibrate/SKILL.md) separately only when durable
     evidence shows avoidable rework or a corrected default.

   These are not three closeout reviews: `audit-choices` owns current decisions,
   `review-guide` owns external reviewer context, and `calibrate` owns future
   task learning. None substitutes for or repeats another.

## Rules

- **Delegate independent work to subagents so passes run in parallel.** The
  spec's dependency graph is the map: whenever two or more slices, branches (e.g.
  frontend vs backend), sub-slices, replication spikes, or recon tasks have no
  unmet dependency on each other, hand them to subagents that run concurrently
  (spawn them in one message) instead of doing them yourself in sequence. Give
  each subagent its own git worktree when they touch files in parallel so their
  diffs don't collide, and keep work that shares the same files or API seam on a
  single agent to avoid merge chaos. Each delegated unit still owns its full pass
  — implement, verify, risk-tiered review gate, focused commit — and you integrate
  the results, resolve conflicts, rerun the affected gates on the merged tree, and
  keep the Next Agent Prompt coherent. Only serialize what the graph says must be
  serial; never idle a lane waiting on an unrelated one.
- Treat backward compatibility as non-goal for unshipped/dev scaffolding. Delete
  old paths, wrappers, aliases, fallback modes, and stale tests when the new
  architecture replaces them.
- Do not let tests get easier by accident. A split harness or new runner must
  preserve the old default coverage unless the spec explicitly changes it.
- Commit every clean pass, then immediately begin the next one. A green commit is
  a checkpoint, not permission to stop. If a pass is not green, do not commit it
  as finished; report the failing contract and exact evidence.
- Do not declare completion while work remains. "Slice N is done and committed" is not a
  finished task while later slices or TODOs are open — a single completed slice is
  a reason to continue, never to hand back as done. The only legitimate early stops are: a
  hard blocker that needs a user-only decision, a gate that cannot be made green
  with an honest fix, or the user interrupting. Context pressure is a reason to
  refresh the durable handoff and transfer to a fresh session when supported,
  not to abandon the goal. When you must pause, record exactly which slice is
  next and why.
- Keep visual evidence honest: contact sheets, GIFs, screenshots, and
  baselines must show the thing being judged at the intended camera/framing.
- Sweep every user-visible surface implied by the slice. A model, state, or
  data change is not done if the main view, cards, menus, reports, and
  verification fixtures now tell different stories.
- When the implementation touches shared behavior, leave docs or spec rationale
  using [write-docs](../write-docs/SKILL.md) principles: durable invariants and
  pointers, not copied inventories.
- For long specs, keep the spec itself reviewable as an invariant. Do not let
  the README become a transcript of every attempt; keep one current handoff, one
  TODO/graph, and one compact evidence ledger, with details in slice files or
  assets.
- **Human checkpoints never block.** At a slice's review or sign-off gate, open
  the relevant shots with [preview-shots](../../visual/preview-shots/SKILL.md),
  state the decision and the options, and give the user ~5 minutes to weigh in —
  keep building other non-blocked work meanwhile, never idle. If they don't
  answer, make the call yourself on the evidence, record the decision and its
  rationale in the spec (the checkpoint's resolution), and keep going — and close
  the shots you opened (preview-shots cleans up Preview) so a long unattended run
  never piles up windows. A goal or implementation NEVER stops to wait on the
  user; it documents the assumption, keeps it reversible, and lets the user
  course-correct later.

## Done

A **pass** is done when code, compact handoff status, verification evidence,
its risk-tiered review gate, and a focused commit all agree on the same current
truth — then you start the next pass.

The **spec** is done — and only then is this skill done — when every slice and
global TODO is closed, all gates are green, final integration review and any
final visual critique have run and their fixes have landed, the handoff shows
nothing left to pick up, and the spec has been archived with
[close-spec](../close-spec/SKILL.md).
Anything short of that is mid-implementation: keep going.

The final handback presents the choices ledger, not the diff, per
[audit-choices](../audit-choices/SKILL.md) — a days-long unsupervised run
earns its merge through this ledger; it is the user's review surface for
everything decided without them. Hand over the **consolidated** ledger from
step 13 (final state, verified against shipped code, choices only), never the
raw per-pass append — a ledger still carrying "will be done in a later slice"
verdicts tells the user you never went back to confirm it was.

**Slices are not the only unit of scope.** A spec also records *decisions* —
ledger rows, decision-table entries, invariants — and a decision can be agreed
in planning but never turned into a slice, especially when it's orthogonal to
the slices' theme. "All slices closed" then reads as done while that decision is
silently unbuilt. Before declaring the spec done, reconcile every recorded
decision against the shipped code, not just the slice list: each one is either
implemented, or explicitly marked "no code needed." A decision with no owning
slice is the classic silent miss — the close-spec audit is the backstop for it,
not the first line of defense.
