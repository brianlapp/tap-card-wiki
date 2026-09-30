# Brand Directions

**Status:** Open — two directions, one to be chosen
**Updated:** 2026-09-30
**Owner:** Brian Lapp
**Method:** From `UNCARD_Brand_Directions.md` (v0.1, Sep 29, 2026), the logo pack, and the brand-guide pages of the demo artifact. The guide calls itself "a working guide for review, not a final standard". Contrast ratios are as stated in the guide (unverified here).

## TL;DR

Working name change: **Tapcard → UNCARD**. Two directions, same product, different voice:

- **A · Matinee** — big, warm, sure of itself. For the whole family.
- **B · Midnight** — fast, funny, in on the joke. Built for the group chat.

Decision tracked in `../decisions/0004-brand-direction.md`. Demo: <https://claude.ai/artifact/WNJACScZP1etR5EmdV4qaX>

<p>
<img src="/docs/brand/logos/matinee/png/uncard-matinee-wordmark-on-yellow-2000w.png" alt="UNCARD Matinee wordmark" width="320">
<img src="/docs/brand/logos/midnight/png/uncard-midnight-wordmark-on-void-2000w.png" alt="UNCARD Midnight wordmark" width="320">
</p>

## Shared rules

- **The gift looks like its world, not like the UNCARD brand.** The brand dresses the site; each uncard wears its own theme (spec §6.1, as quoted in the demo's source).
- **The wordmark is the whole logo.** No symbol, badge or mascot beside it.
- A separate app icon exists for app icons, favicons and avatars only, and **never sits next to the wordmark**.
- Clear space: half the cap height on every side. Minimum: 96 px on screen, 24 mm in print.
- All logo type is outlined, so files need no fonts. Archivo and Saira are SIL OFL.
- Write "uncard" lowercase in sentences. UNCARD in capitals is the logo's job.
- No stock photos. Never a real child's photo in marketing.
- No fake social proof, no invented replay counts, no "gone viral".

## Side by side

| | A · Matinee | B · Midnight |
|---|---|---|
| Modelled on | Yellow "Tenfold" reference | Dark neon "Encore" reference |
| Headline | Not a card. A whole little world. | Cards get recycled. Uncards get replayed. |
| Brand line | A whole little world. Made for one person. | One link. One person. A whole little world. |
| Wordmark | `UNCARD.` Archivo Expanded 112, Black 900, tracking −12, outlined | `UNCARD_` Saira Expanded 125, ExtraBold 800, tracking +50, outlined |
| Signature | Tomato full stop, tucked 10 units in | Hot Pink cursor: blinks six times on load, then holds |
| Icon | `U.` on Marquee | `U_` on Void |
| Primary button | Make one | Drop one |
| Verb | give | drop ("deploy" for finales only) |
| Motifs | Tickets, filmstrip, flat outlined objects | Terminal windows, pixel sprites, ticket stickers |
| Illustration | Flat objects, 2.5-unit Ink outline, small hard shadow, ≤5 colours | Pixel sprites on a strict grid, ≤5 colours, glow only on Void |
| Motion | Pop, don't wobble. 180 ms ease-out. Nothing loops | Snap, glitch once, settle. 120 ms steps. Only the cursor blinks |

## Colour

**Matinee**

| Name | Hex | Use | Contrast |
|---|---|---|---|
| Marquee | `#FFCB0A` | The field. ~60% of most screens | Ink on Marquee 12.4:1 |
| Ink | `#121114` | Type, outlines, dark button | Ink on Paper 18.8:1 |
| Tomato | `#F2442E` | Full stop and main button. **Never body text** | Ink on Tomato 5.1:1 · white only at 19 px bold |
| Paper | `#FFFFFF` | Cards, forms, tickets | |
| Butter | `#FFF3C4` | Quiet studio surfaces | Ink on Butter 16.9:1 |
| Sky / Bubblegum / Mint | `#49B2F5` `#FF8CC6` `#33C584` | Illustration only | |

**Midnight**

| Name | Hex | Use | Contrast |
|---|---|---|---|
| Void | `#08080B` | The field | |
| Acid | `#C4F23A` | Wordmark, primary buttons, live states | Acid on Void 15.3:1 |
| Hot Pink | `#FF2E93` | Cursor, second button, stickers | Pink on Void 5.8:1 |
| Paper | `#F3F3EF` | Body text | Paper on Void 18.0:1 |
| Smoke | `#A0A0AC` | Secondary text, metadata | Smoke on Void 7.7:1 |
| Cyan / Violet / Panel | `#34E4FF` `#8C5CFF` `#121218` | Support | |

## Type

| Role | Matinee | Midnight |
|---|---|---|
| Display | Archivo Condensed Black — sentence case, ends on a full stop (Tomato on screen) | Saira Semi-condensed ExtraBold — sentence case, no exclamation marks |
| Text | Archivo Regular/Semibold, 17–20 px, 1.5 leading | Saira Regular, 16–19 px, 1.55 leading |
| Labels | Archivo Semi-expanded Bold caps, +8% tracking | JetBrains Mono caps with a middle dot: `SCENE 04 · PLAYABLE` |
| Special | — | Silkscreen, game HUDs only. Never paragraphs |

## Voice

| | Matinee | Midnight |
|---|---|---|
| Traits | Warm · Bold · Specific · Playful | Hype with receipts · Internet-native · System-speak with a heart · Roast gently |
| Say | uncard, scene, world, your person, give, keep, play | drop, scene, replay, patch, uptime, keepsake, the group chat |
| Avoid | e-card, template, AI-generated, content, user, experience, magical | viral, epic, literally, AI-powered, content, user, e-card |
| Never | Greeting-card poetry; caps lock; "amazing"; jokes about bodies, money or age | Fake stats; "slay/bestie/no cap"; cold jargon all the way down; punching down |

**Before / after**

| | Before | After |
|---|---|---|
| Matinee | Create a magical AI-powered personalised e-card experience for your loved ones in minutes! | Tell us about someone you love. We'll make them a whole little world. |
| Midnight | OMG!!! Make an EPIC AI birthday card that'll go VIRAL!!! | Make them a nine-scene birthday drop. One link. Built to be replayed. |

**Lines for real moments**

| Moment | Matinee | Midnight |
|---|---|---|
| Prompt | Who are we celebrating? Tell us what makes them them. | `> who are we celebrating?` |
| Follow-up | What's the most Jamie thing they've done lately? | What's the most Jamie thing they've done recently? |
| Error | That photo didn't upload. Try a JPG or PNG under 20 MB. | Upload failed: that file isn't a photo. Try a JPG or PNG under 20 MB. |
| Empty state | No uncards yet. Somebody deserves one. | 0 drops. Somebody's birthday is loading. |
| Reminder | Riley's uncard has 30 days of hosting left | jamie-40: 30 days of uptime left |
| Recipient opening | Riley, you have one birthday transmission. | Press any key. Or pick one. |

## Logo files

`logos/` — the v0.1 pack. SVG masters plus PNG exports (2000 px wordmarks; icons at 32/180/512/1024).

| Matinee | Midnight |
|---|---|
| wordmark: primary, on-yellow, reversed, one-colour ink, one-colour white; stacked (UN / CARD.) for square spaces | wordmark: primary, on-void, reversed, one-colour white; **glitch** (motion and hero moments only) |
| app icon `U.` | app icon `U_` |

## Open questions

1. Matinee or Midnight? (`0004`)
2. Is UNCARD final, and does it clear trademark and domain checks? (unverified)
3. The demo prices at $5.99; the spec baseline is $4.99. (`0002`)
