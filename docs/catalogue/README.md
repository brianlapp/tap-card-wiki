# Card Catalogue

**Status:** Draft
**Updated:** 2026-09-30
**Owner:** Brian Lapp
**Method:** Exported from `Card_Sections_Catalogue.xlsx` (50 sections) and `Card_Themes_Catalogue.xlsx` (20 themes), uploaded 2026-09-30. Export validated against both workbooks' own Summary sheets — counts, age-band ratings, effort × wave, sound/photo, kit sizes and prompt structure all match; all 120 palettes re-pass WCAG contrast; all 488 theme × section pairings match the matrix cell for cell. Ratings and Wow scores are the author's judgment, untested with real recipients (unverified).

## TL;DR

What an uncard is made of. **Sections** are the content blocks (a game, a roast, a letter). **Themes** are the look that wraps them. An uncard is **8–10 scenes (default 9), one per beat of the nine-beat arc**, inside one world. See `../product/experience.md`.

```bash
grep '^S15,' docs/catalogue/sections.csv            # one section
grep '^T03,' docs/catalogue/themes.csv              # one theme
grep '^T03,' docs/catalogue/theme-kits.csv          # a theme's kit options
grep ',S15,' docs/catalogue/theme-section-fit.csv   # which themes suit a section
```

## Words

The catalogues and the site use different words for the same things. IDs are the stable bridge.

| Catalogue | Site (brand demo) | IDs |
|---|---|---|
| section | **scene** | S01–S50 |
| theme | **world** | T01–T20 |
| card | **uncard** | — |

## Read this much, and no more

| You need | Read | Cost |
|---|---|---|
| What's in here, how to query | this file | ~1,000 tokens |
| One section or theme | `grep` one line | **~100 tokens** |
| A theme's full kit | `grep '^T03,' theme-kits.csv` | ~250 tokens |
| Every section, short form | `sections.csv` | ~5,517 tokens |
| To generate a card | `prompts.md` + the rows you picked | ~2,000 + rows |
| Both source workbooks, whole | — | ~59,000 tokens |

## Files

| File | What |
|---|---|
| `sections.csv` | 50 sections: category, what it is, fit per age band, tone, sound, photo, effort, wave, wow, lineage |
| `section-details.csv` | Per section: prompt template, when to use, example, what the giver must supply, watch-outs |
| `themes.csv` | 20 themes: family, fit per age band, tone fit, effort, wave, wow, look capacity |
| `theme-details.csv` | Per theme: prompt template, two example cards, facts that drive the look, fixed DNA, watch-outs |
| `theme-kits.csv` | Every kit option: type pairings, layouts, motifs, motion, interaction (long format) |
| `palettes.csv` | All 120 palettes with recomputed contrast ratios |
| `theme-section-fit.csv` | 488 theme × section pairings: shines / works / avoid |
| `prompts.md` | The shared prompt preambles, output shape, placeholders, originality rule |
| `legend.md` | Column meanings, rating scales, effort/wave keys, gender note, author's assumptions |
| `samples.md` | Six imaginary recipients built both ways (catalogue decks vs demo) |
| `reference.md` | Where sections and themes came from; parked ideas — check before proposing a "new" one |

## The numbers

**Sections by category:** Openers 5 · Stories & Cartoons 7 · Roasts & Reveals 8 · Fake Formats 5 · Games 7 · Quizzes 4 · Music & Sound 4 · Heart & Words 6 · Finales 4

**Themes by family:** Paper & Print 5 · Keepsakes & Handmade 5 · Play & Games 4 · Screens & Stage 3 · Loud & Graphic 3

**Build waves** — what can ship first:

| | Wave 1 (text + code) | Wave 2 (photos, audio, music) | Wave 3 (engines, generated art, multi-person) |
|---|---|---|---|
| Sections | 40 | 5 | 5 |
| Themes | 17 | 1 | 2 |

Wave 1 is the first-milestone pool.

## Rules that matter

- **Facts vs flourish.** Real facts come only from the giver. Jokes may exaggerate a real fact but never invent a new one. Missing fact → skip the section.
- **The theme never writes copy.** Tone always comes from the giver's brief.
- **No two cards look alike.** Each card picks one option on six axes; it must differ from the last 20 cards in that theme on at least 4. Picks are driven by the person's facts, not randomness.
- **One self-contained file.** Fonts embedded as subsets, art as inline SVG/CSS/canvas. No third-party characters, logos or real brands.
- **No gender scores.** Ask pronouns once, pick from interests. See `legend.md`.

## Open questions

1. ~~8 sections or 9 scenes?~~ Resolved by `0005`: 8–10 scenes, default 9. The workbooks' "about 8 sections" is superseded.
2. Both workbooks cite `Tapcard_Product_and_Build_Spec_v2` (§4.2 arc, §5.1 visual worlds, §6 design direction, Appendix A). That spec is not in this wiki.
3. Ratings and Wow scores need testing with real people before they drive section picks.
