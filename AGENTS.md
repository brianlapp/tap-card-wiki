# AGENTS.md

Context for AI agents working in this repo. Read this first, then load only the linked docs relevant to the task.

## Project

**UNCARD** (working name since 2026-09-29; formerly Tapcard) — personalized, interactive birthday cards that adults create for someone they love. A player renders 8–10 scenes from a versioned card JSON: sections (the content) inside a theme (the look). Recipients open a link. No child accounts.

The repo, file names and older docs still say Tapcard. Same product.

**Current milestone:** one synthetic test card working end to end (create → preview → publish → play → export). Nothing else ships first.

## Doc map

| Need | Read |
|---|---|
| What we're building, stack, constraints | `docs/product/scope.md` |
| Who we compete with, pricing reality | `docs/research/competitive-landscape.md` |
| What the giver and recipient actually experience | `docs/product/experience.md` |
| What a card is made of: 50 sections, 20 themes | `docs/catalogue/` — **grep, do not read whole** |
| Generating a card: prompt rules and output shapes | `docs/catalogue/prompts.md` |
| Name, logo, colours, voice (brand: **Matinee**) | `docs/brand/directions.md` |
| What's built and being built now, the active work list | Product repo: `docs/review-2026-09-30/` in [`uncard-starter`](https://github.com/JNabsRepo/uncard-starter) |
| The working mockup — what the build reproduces | `examples/uncard-demo/` (~1 MB; content already extracted into the docs above) |
| Why a choice was made | `docs/decisions/` (numbered ADRs) |
| How to write/update these docs | `docs/conventions.md` |
| A task: what it is, who owns it, what blocks it | `docs/tasks/` — **grep, do not read whole** |
| Full 526-task build catalogue | `docs/tasks/tasks.csv` (exported; do not use the Sheet) |

`docs/index.md` lists every doc with a one-line summary. When you add a doc, add it there too.

## Rules for agents

- **The brand demo is the line of truth.** Where docs disagree, the UNCARD brand demo wins; older statements are marked superseded (`docs/decisions/0005-demo-is-source-of-truth.md`). If you find a new contradiction, don't pick a side silently — flag it.
- **The brand is Matinee.** Yellow Marquee field, Ink type, Tomato full stop. Midnight is rejected. The gift itself wears its world, not the brand.
- **Speak the product's words.** In anything user-facing: *uncard, scene, world, your person, give*. Never *e-card, template, AI-generated, content, user*. File names and IDs keep *section/theme*.

- **The product lives in [`JNabsRepo/uncard-starter`](https://github.com/JNabsRepo/uncard-starter)** — Lovable + TanStack Start + Supabase, live at uncard.app (`docs/decisions/0001`). This wiki holds no code. Lovable and a build agent commit there continuously: never force-push or rewrite its history.
- **Two sources, two jobs.** The brand demo (`examples/uncard-demo/`) says what UNCARD *should be*. The product repo says what *is built* — its `docs/review-2026-09-30/` is the source of truth for build status, the work list and phase reports. Link to those; don't copy them here.
- **Staging only.** Never run against production data, credentials or billing.
- **No invented facts.** If a number, status or capability is unverified, write "unverified" rather than guessing.
- **Server-side AI only.** No generated code executes in the recipient's browser.
- **Privacy is a hard gate.** No child logins, no child contact data, no PII in telemetry.
- **Stripe is deferred.** Do not scaffold, connect or mock payments.
- **Small slices.** One thin vertical slice, working, before any parallel expansion.
- **Every change needs a rollback path.**
- **Facts come only from the giver.** In anything generated, real names, events and numbers come from the giver's facts. Flourish may exaggerate a fact, never invent one. Missing fact → skip. See `docs/catalogue/prompts.md`.
- **Never load the build catalogue spreadsheet.** It costs ~118,000 tokens and needs Jordan's Drive. Everything useful is in `docs/tasks/` — `grep '^T-002,' docs/tasks/tasks.csv` costs about 40.

## Task sizing

S = 1–2h, M = 2–4h. Anything larger gets split. A task is Done only when its acceptance criteria are met and evidence is linked — not when the code compiles.
