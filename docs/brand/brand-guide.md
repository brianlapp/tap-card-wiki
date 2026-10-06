# Brand Guide and System (v1.0)

**Status:** Draft
**Updated:** 2026-10-06
**Owner:** Jordan
**Method:** From `UNCARD-brand-guide.pdf` (v1.0, October 2026, text extracted with `pdftotext`) and `UNCARD-brand-system.zip` (v1.0, October 2026), both posted by Jordan in Slack #non-build-stuff on 2026-10-02. Compared against the existing `directions.md` and `logos/` pack. Contrast ratios are as stated in the source, not re-verified here.

## TL;DR

- This is a **v1.0 production release of the already-decided Matinee direction** (`decisions/0004-brand-direction.md`) — one theme now, not two. Midnight doesn't appear at all; it's fully dropped here, not just marked rejected.
- Adds what `directions.md` and the old v0.1 logo pack didn't have: a **design-token system** (`tokens/tokens.json` + `tokens/tokens.css`), **six CSS components** (Button, Chip, Pill, Ticket, Headline, SceneFrame), and **nine outlined illustration SVGs**.
- Adds **four colours not in `directions.md`**: Cream `#FFF9E6`, Ink-70 `#57524A` (secondary text), plus three `-soft` illustration tints (Sky-soft `#BFE5FF`, Bubblegum-soft `#FFD1E8`, Mint-soft `#C6F2DC`) and a focus-ring blue `#2F6BFF`.
- Nearly all the new system's sample copy still uses **"Riley"** as the example recipient ("Riley, you have one birthday transmission," reminder and share-caption examples) — the superseded Midnight-demo name; `decisions/0005` resolved the product's sample girl to **Steph**.
- Treats **Tomato as the fixed, only main-button colour**, with no mention of the red-vs-green trial that `directions.md` and `product/live-product.md` both still list as open (D5).

## What's new versus `directions.md`

| Area | `directions.md` (existing) | Brand guide / system v1.0 (new) |
|---|---|---|
| Colour | Marquee, Ink, Tomato, Paper, Butter + Sky/Bubblegum/Mint (illustration only) | Adds **Cream** `#FFF9E6`, **Ink-70** `#57524A` (secondary text, 7.7:1 on Paper), and `-soft` tints of Sky/Bubblegum/Mint for illustration frames/tiles, plus a **focus-ring** `#2F6BFF` (3px outline, 3px offset) |
| Contrast detail | Only Ink-on-X ratios given | Adds that **Tomato on Marquee is only 2.4:1** — fine for the decorative full stop, never for Tomato text or thin lines on Marquee — and that **white on Tomato is 3.7:1** (not the 5.1:1 Ink-on-Tomato figure `directions.md` quotes), so white only works at 19px bold or larger |
| Type | Archivo Condensed Black (display); Archivo Regular/Semibold (text); "Archivo Semi-expanded **Bold** caps, **+8%** tracking" (labels) | Same display/text; labels respecified as **Archivo SemiExpanded Extra Bold**, **13px**, **9%** tracking — a small weight/tracking drift from `directions.md`, not a different direction |
| Components | None documented | **Button** (main/dark/ghost/small), **Chip**, **Pill**, **Ticket**, **Headline** (wraps the sentence-ending full stop in Tomato), **SceneFrame** (filmstrip frame: number, name, illustration, caption) — each with working CSS and a preview |
| Spacing / radius / shadow | Not documented | Full token scale: 7 spacing steps, 6 radius tokens, 3 hard-offset shadow tokens (4px button, 6px sticker, 8px prompt-focus), 2 stroke widths |
| Illustration | "Flat objects, 2.5-unit Ink outline, small hard shadow, ≤5 colours," no asset list | Nine named SVGs: cake, gift, balloons, confetti (celebration); rocket, star (adventure/games); envelope, card (giving/sharing); cassette (music) |
| Logo files | v0.1 pack: wordmark (5 variants) + stacked + app icon, 2000w PNGs | Same wordmark/icon set at 2400w/1600w, plus a **new stacked-reversed** mark and a **favicon.ico** not in the old pack |
| Fonts | "Archivo and Saira are SIL OFL" (stated, not shipped) | Ships the actual **Archivo variable fonts** (regular, condensed, semi-expanded) under OFL 1.1 — redistribution is fine, confirmed by `fonts/OFL.txt` |
| Button colour | D5 open: red (Tomato) trialled beside green on the live site | Guide shows **only Tomato**, presented as settled |
| Sample recipient name | `decisions/0005`: resolved to **Steph** | Guide/system copy still says **Riley** throughout |

New assets not already in `docs/brand/logos/` were copied into `docs/brand/system/` (illustrations, fonts, tokens, components, voice.md, logo.md, a favicon and the stacked-reversed mark) — see `docs/brand/system/README.md` for exactly what's there and what was skipped as a duplicate of the existing logo pack.

## Implication for Uncard

- **Operationalizes 0004, doesn't contradict it.** Nothing here reopens the Matinee decision — it fills in implementation detail (tokens, components, contrast math) that `directions.md` and the v0.1 logo pack never had, which is genuinely useful for anyone wiring the brand into code.
- **The fonts are safe to redistribute.** Archivo ships under the SIL Open Font License 1.1, which explicitly allows embedding and sharing (not reselling the font alone) — confirmed from the licence text, not just asserted.
- **"Riley" needs a swap before reuse.** None of the copied files were rewritten (they're kept as delivered, per the ingestion rule for source material), but anyone lifting a ready-made line from `voice.md` or a component README should use "Steph" per `decisions/0005`, not "Riley."
- **Button colour reads as more settled than the wiki treats it.** D5 (red vs. green) is still open in `directions.md` and `product/live-product.md`. This guide isn't necessarily wrong — Tomato may still win the trial — but it shouldn't be read as resolving D5 on its own.

## Open questions

- "Riley" as the sample recipient throughout the new brand-system copy vs. "Steph" (`decisions/0005`) — cosmetic, but worth fixing before reusing any line verbatim.
- Button colour: the guide shows Tomato as final; D5 (`directions.md`, `product/live-product.md`) is still an open red-vs-green trial on the live site.
- Label type spec drift: `directions.md` says "Bold," "+8%" tracking; the new guide/tokens say "Extra Bold," "9%" tracking, 13px. Minor, but worth folding into `directions.md` next time it's updated.
- The new colour tokens (Cream, Ink-70, the `-soft` tints, the focus-ring blue) aren't yet in `directions.md`'s colour table — flagged here, not edited there, per the ingestion instructions for this pass.
- The `Cover` component shipped with no README (every other component has one) — not investigated further here.
