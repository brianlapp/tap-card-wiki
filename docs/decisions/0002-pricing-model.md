# 0002 — Pricing model: one-off vs subscription

**Status:** Accepted (demo pricing, per `0005`)
**Date:** 2026-09-20 · **Updated:** 2026-09-30
**Deciders:** Jordan (owner), Brian Lapp, Tim Miller

## Context

The catalogue records a planned $4.99 single card and $9.99/month subscription, with Stripe deferred. Competitive research (`research/competitive-landscape.md`) found:

- Blue Mountain: $7.99/mo or $35.99/yr, already shipping interactive kids' birthday ecards with mini-games, quizzes and name personalization
- Jacquie Lawson: $36/yr. Hallmark+: $79.99/yr
- Songfinch: ~$199 per custom song, already delivered inside an American Greetings digital card
- personalized-birthday-games.com: personalized browser birthday game for kids, shared by link, **free**

## Options

1. **One-off $4.99 per card** *(price superseded → $5.99)* — matches how a birthday gift is actually bought: impulse, occasion-driven, no commitment.
2. **$9.99/month subscription** *(now for two uncards)* — priced above Blue Mountain while offering a fraction of the library. Hard to defend on value.
3. **Free tier + paid upgrade** — needed if we're competing with a free direct competitor; unit economics unknown given AI generation cost.

## Decision

~~Pending.~~ Resolved 2026-09-30 by `0005` — the brand demo is the line of truth:

- **$5.99** per uncard, one-off
- **$9.99/month** for **two** uncards
- **3 months** hosting included; reminders at 30 and 7 days; then a **free** offline keepsake download, or **$3/year** to keep the link live

Both option 1 (one-off) and option 2 (subscription) survive, at new prices. Stripe work is still deferred until separately authorised.

## Consequences

Whatever we choose sets the cost ceiling per card. If AI generation plus a custom song costs more than the price, the model breaks. Cost per accepted card must be measured (catalogue task T-GEN-09) before pricing is locked.

## Update 2026-09-30 — three prices now in play

New sources added two more data points. Nothing above is withdrawn; the options still stand.

| Source | Single | Plan | Hosting |
|---|---|---|---|
| Build catalogue (original) | $4.99 | $9.99/month | — |
| Spec "approved baseline", as quoted in the brand notes | $4.99 | $9.99/month for **three** credits | 3 months included, then free keepsake download or $3/year |
| Brand demo (`../product/experience.md`) | **$5.99** | $9.99/month for **two** | same |

The demo followed its reference mockups, not the spec. The spec (`Tapcard_Product_and_Build_Spec_v2`) is superseded by the demo, so its baseline no longer applies.

The hosting model is consistent across sources: three months included, reminders at 30 and 7 days, then a free offline keepsake or $3/year to keep the link live. That is effectively a small recurring option already, independent of the plan question.

~~Still blocks Stripe work.~~ Resolved by `0005`: the demo's numbers are the baseline. The $4.99 figures are superseded.
