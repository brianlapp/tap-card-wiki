# Brand system assets (v1.0, October 2026)

What's here, copied from `UNCARD-brand-system.zip` (posted by Jordan in Slack #non-build-stuff on 2026-10-02). See `../brand-guide.md` for how this compares with `../directions.md` and `../logos/`.

| Folder / file | What's inside |
|---|---|
| `voice.md` | Writing rules, ready-made lines. Overlaps with `../directions.md`'s Voice section; this is the primary-source version. |
| `logo.md` | Wordmark and app-icon rules, in the system's own words. |
| `tokens/tokens.json` | Source-of-truth design tokens: colour, type, spacing, radius, shadow, stroke. |
| `tokens/tokens.css` | The same tokens as CSS variables and type-style classes, plus `@font-face` rules. |
| `components/bundle.css` | CSS for the six components below. |
| `components/Button/`, `Chip/`, `Headline/`, `Pill/`, `SceneFrame/`, `Ticket/` | Each has a `preview.html` and a `README.md` explaining when to use it. |
| `components/Cover/` | Has a `preview.html` only — the system shipped with no README for this one. |
| `illustrations/*.svg` | The nine approved outlined illustration objects (cake, gift, balloons, rocket, star, envelope, cassette, card, confetti). |
| `fonts/` | Archivo in three widths (variable `.woff2`), under the SIL Open Font License 1.1 (`OFL.txt`) — free to use, embed and share; not to resell as a font on its own. |
| `logos/favicon.ico` | Not in the existing `../logos/matinee/` pack. |
| `logos/uncard-stacked-reversed.svg` | A reversed stacked mark; the existing pack only had the non-reversed stacked mark. |

**Skipped as duplicates:** the zip's `logos/uncard-icon-*.png/svg`, `uncard-wordmark*.png/svg` and `uncard-stacked.svg`/`uncard-stacked-1600.png` are the same wordmark and app icon already in `../logos/matinee/`, just at different export sizes. Also skipped: `UNCARD-brand-guide.pdf` and `brand-guide.html` (the guide itself — already covered by `../brand-guide.md`, and the source PDF stays in Slack/Drive rather than being duplicated here) and the zip's own top-level `README.md` (superseded by this one).

**Note on sample copy:** several files here (`voice.md`'s ready-made lines, the Button/Ticket component READMEs) still use "Riley" as the example recipient name. That's the Midnight-era demo name; `../../decisions/0005-demo-is-source-of-truth.md` resolved the product's sample girl to "Steph." These files are kept as delivered, not rewritten — swap the name if you reuse a line.
