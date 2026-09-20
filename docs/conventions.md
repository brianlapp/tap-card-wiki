# Doc Conventions

These exist so an agent can parse any doc in this wiki without guessing. Follow them exactly when creating or updating docs.

## Every doc starts with this header

```
# <Title>

**Status:** Draft | Accepted | Open | Superseded
**Updated:** YYYY-MM-DD
**Owner:** <name>
**Method:** how this was produced — web research, hands-on test, team decision, vendor docs. Say what was NOT verified.
```

The `Method` line is the important one. It tells a future agent how much to trust the contents.

## Marking confidence inline

- Plain statement = verified, with a source or a test behind it
- `(unverified)` = believed true, not confirmed
- `(assumption)` = we chose to proceed as if this were true
- Never state a number, status or capability without one of the above

## Structure

- `## TL;DR` at the top of any doc longer than a screen
- `## Implication` after any research section — raw findings without a "so what" are not useful to an agent
- `## Open questions` and `## Not yet researched` at the bottom, so gaps are explicit rather than invisible

## Naming

- Lowercase, hyphenated: `competitive-landscape.md`
- Decisions numbered: `0001-source-of-truth.md`
- One topic per file. Split rather than append indefinitely.

## Decision records (ADRs)

```
# <NNNN> — <Decision title>

**Status:** Open | Accepted | Superseded by <NNNN>
**Date:** YYYY-MM-DD
**Deciders:** <names>

## Context
What forced the choice.

## Options
Each option with its trade-off.

## Decision
What we chose.

## Consequences
What this commits us to, and what it rules out.
```

Record the rejected options. Six months from now, the rejected options are the valuable part.

## When updating

- Change the `Updated` date
- Update the row in `docs/index.md`
- Don't silently rewrite a finding — mark the old one superseded and say why
