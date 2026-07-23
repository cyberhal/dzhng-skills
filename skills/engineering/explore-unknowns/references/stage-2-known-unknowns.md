# Stage 2 — Known Unknowns: The Questions You Can Name

The questions that must be answered but aren't yet. You know the question;
the answer lives with the user or in the territory.

## Procedure

1. Inventory the questions the task cannot proceed without, and disclose the
   queue ("still queued after this: …") so the user sees how much walk
   remains.
2. Route territory-answerable questions to a targeted fact check instead of
   asking the user.
3. Resolve **high-blast-radius questions one at a time, worst first**. A
   question earns its own turn when its answer can reshape the architecture,
   scope, safety, migration, or later questions. Give a recommendation and
   lettered options the user can answer in a few characters.
4. Batch related medium/low-impact leaf questions **3–5 at a time** when that
   many remain; use one smaller final batch rather than padding it. Each row in
   the compact decisions table carries an id, recommended default, one-line
   basis, and flip cost. Let the user reply “accept all” or edit row ids; do
   not make them compose each answer.
5. Close every question one of three ways:
   - **Answered by the user** — record the decision and why on the map.
   - **Resolved by the territory** — go read it instead of asking, verify and
     store the claim once in the fact ledger, then show the user the question
     and found evidence. The map points to that entry; it does not copy the
     claim into its decision ledger. A question closed off-screen isn't closed.
   - **Recorded as OPEN on the map** — explicitly deferred, with what
     unblocks it.

   A batch row left unanswered remains provisional/OPEN. Silence never turns a
   recommended default into the user's decision.

**Done when** every named question is closed one of those ways, in front of
the user. Announce the stage closed (a small decisions table recaps it well)
before crossing into stage 3.

## Techniques

- **The interview** — one turn per architecture-shaping question, ordered by
  blast radius; related leaf questions ride in batches of 3–5, each with a
  recommendation and cheap response id.
- **Brainstorm the intervention** — when the question is "which solution?":
  search the codebase first, then plot ~10 interventions from
  ship-this-afternoon to quarter-long bet, each grounded in what actually
  exists (half-built features behind flags and disconnected wiring are the
  cheapest wins); resonate-checkboxes assemble the reply.
- **Point at a reference** — when an existing implementation encodes the
  wanted behavior: produce a semantics map proving you understood it — what
  it does with excerpts, how each behavior maps to the target stack, every
  place the port cannot be literal. Nothing gets ported until sign-off.
