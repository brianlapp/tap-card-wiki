# 0005 — The brand demo is the line of truth

**Status:** Accepted · amended 2026-10-01
**Date:** 2026-09-30
**Deciders:** Brian Lapp

## Context

By 2026-09-30 the wiki held four generations of product thinking: the build catalogue (Sep 19), the section and theme catalogues, the brand directions notes, and the UNCARD brand demo (v0.1, Sep 29). They disagreed on card length, pricing, audience and sample decks. A wiki with unresolved contradictions is worse than one with gaps, because an agent cannot tell which statement to act on.

## Options

1. **Newest source wins.** The demo is the latest output and was built from all the others. Clear, but older detail it doesn't cover must survive.
2. **Leave conflicts open for Jordan.** Accurate, but blocks every agent that touches the conflicting areas.
3. **Spec wins.** Rejected: the spec (`Tapcard_Product_and_Build_Spec_v2`) is older, and the demo was built from it.

## Decision

**Option 1.** Where any doc disagrees with the brand demo, **the demo wins**. The older statement is marked superseded and kept, per `../conventions.md`. Where the demo is silent, the older docs stand.

> **Amended 2026-10-01 — newest wins.** The rule's reason was always *the newest output leads*. The live product repo ([`JNabsRepo/uncard-starter`](https://github.com/JNabsRepo/uncard-starter), commits to 2026-10-01) is now newer than the demo (2026-09-29), so **where the real product and the demo differ, the product wins**. The demo still defines what isn't built yet. Order: product repo → brand demo → catalogues → build catalogue.

Resolved on this basis:

| Question | Resolved as (demo) | Superseded |
|---|---|---|
| Card length | 8–10 scenes, default 9, on the nine-beat arc | 8-section decks in the catalogue workbooks |
| Price | $5.99 per uncard · $9.99/month for two · 3 months hosting, then free keepsake or $3/year | $4.99 single; $9.99/month (for three) |
| Audience | Anyone someone loves: the whole family, kids through 60+ | "Kids-first product" |
| Sample decks | The demo's six uncards | The catalogues' sample decks |
| Jamie's world | T02 Firmware · After Hours | T18 Case File |
| Name | UNCARD | Tapcard |
| Sample girl, 9 | **Steph** (product) | Riley (demo) |
| Scene count wording | **"usually 8 to 10"**, default 9; shorter when there's little to go on (product, D6) | "8–10, default 9" (demo) |
| Domains | **uncard.app** (site), **uncard.gifts** (gift links) (product) | uncard.com (demo sample links) |
| Words | scene, world, uncard, your person, give | section, theme, card, recipient, send (kept in file names and IDs) |

Resolved the same day: the brand is **Matinee** (`0004`). The product repo question is in `0001` (corrected 2026-10-01: the repo exists). The demo is saved at `examples/uncard-demo/`.

## Consequences

- `0002` (pricing) is accepted on the demo's numbers. Stripe stays deferred until someone authorises it.
- The **build plan** in `../tasks/` was written against the older model. Its task text is not rewritten here — changing the plan is a separate decision — but affected tasks are listed in `../tasks/README.md`.
- Confirmed with Jordan, 2026-09-30.
