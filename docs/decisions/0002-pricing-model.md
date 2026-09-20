# 0002 — Pricing model: one-off vs subscription

**Status:** Open
**Date:** 2026-09-20
**Deciders:** Jordan (owner), Brian Lapp, Tim Miller

## Context

The catalogue records a planned $4.99 single card and $9.99/month subscription, with Stripe deferred. Competitive research (`research/competitive-landscape.md`) found:

- Blue Mountain: $7.99/mo or $35.99/yr, already shipping interactive kids' birthday ecards with mini-games, quizzes and name personalization
- Jacquie Lawson: $36/yr. Hallmark+: $79.99/yr
- Songfinch: ~$199 per custom song, already delivered inside an American Greetings digital card
- personalized-birthday-games.com: personalized browser birthday game for kids, shared by link, **free**

## Options

1. **One-off $4.99 per card** — matches how a birthday gift is actually bought: impulse, occasion-driven, no commitment.
2. **$9.99/month subscription** — priced above Blue Mountain while offering a fraction of the library. Hard to defend on value.
3. **Free tier + paid upgrade** — needed if we're competing with a free direct competitor; unit economics unknown given AI generation cost.

## Decision

Pending. Must be decided before any Stripe work is authorized.

## Consequences

Whatever we choose sets the cost ceiling per card. If AI generation plus a custom song costs more than the price, the model breaks. Cost per accepted card must be measured (catalogue task T-GEN-09) before pricing is locked.
