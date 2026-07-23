# Fact Ledger — Territory Claims Need Evidence

The fact ledger records claims about the current observable territory: code,
system behavior, data, external constraints, and measured results. It travels
with the unknowns map as a section or linked artifact.

## Route claims before recording them

- **Intent, constraint, or taste** belongs in the unknowns map as a requirement
  or decision. The user owns it; it is not a territory fact.
- **Territory claim** belongs in the fact ledger and needs evidence before the
  plan treats it as true.
- **Conjecture or recollection** may enter the ledger only as `unverified`.
  Never promote it because it sounds plausible or went unchallenged.

## Entry contract

Each entry carries:

- **Claim** — one falsifiable statement.
- **State** — `verified`, `contradicted`, `unverified`, or `deferred`.
- **Evidence** — file/symbol, test, log, command output, primary source, or the
  missing check that prevents verification.
- **Scope and freshness** — where the claim holds and what change would make it
  stale.

`deferred` means the check is not worth its cost yet; record what would make it
worth checking. Silence never changes an entry's state.

## Boundaries

- Decisions and alternatives belong in the map during exploration and
  `choices.md` during implementation.
- Requirements and acceptance criteria belong in the map/spec.
- Current progress, gates, and next pickup belong in the durable handoff.
- The fact ledger contains none of those; it is evidence about the territory.

## Contradicted-claim protocol

When evidence contradicts the user's territory claim, show the claim, the
contradicting evidence, and plausible explanations. Ask whether the requirement
changes; never silently follow the code and reshape intent. Evidence is yours
to report. Intent is theirs to amend.

When new information arrives mid-walk, route it immediately, verify any
territory claim it contains, and update every map entry that depended on the
old state.
