# CLAUDE.md

Context for AI agents working in this repo. Read this first, then load only the linked docs relevant to the task.

## Project

**Tapcard** — personalized, interactive birthday cards that adults create for kids. A slideshow player renders themed scenes (opening boot, greeting, mini-games, mixtape, certificate, candles finale, closing note) from a versioned card JSON. Recipients open a link. No child accounts.

**Current milestone:** one synthetic test card working end to end (create → preview → publish → play → export). Nothing else ships first.

## Doc map

| Need | Read |
|---|---|
| What we're building, stack, constraints | `docs/product/scope.md` |
| Who we compete with, pricing reality | `docs/research/competitive-landscape.md` |
| Why a choice was made | `docs/decisions/` (numbered ADRs) |
| How to write/update these docs | `docs/conventions.md` |
| Full 526-task build catalogue | Google Sheet (see scope.md) |

`docs/index.md` lists every doc with a one-line summary. When you add a doc, add it there too.

## Rules for agents

- **Verify before rebuilding.** A Lovable project and backend already exist. Confirm the authoritative project/branch before changing anything.
- **Staging only.** Never run against production data, credentials or billing.
- **No invented facts.** If a number, status or capability is unverified, write "unverified" rather than guessing.
- **Server-side AI only.** No generated code executes in the recipient's browser.
- **Privacy is a hard gate.** No child logins, no child contact data, no PII in telemetry.
- **Stripe is deferred.** Do not scaffold, connect or mock payments.
- **Small slices.** One thin vertical slice, working, before any parallel expansion.
- **Every change needs a rollback path.**

## Task sizing

S = 1–2h, M = 2–4h. Anything larger gets split. A task is Done only when its acceptance criteria are met and evidence is linked — not when the code compiles.
