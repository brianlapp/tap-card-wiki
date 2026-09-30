# Catalogue Legend

**Status:** Draft
**Updated:** 2026-09-30
**Owner:** Brian Lapp
**Method:** Column keys, rating keys and notes copied from the "How to use" sheets of both catalogue workbooks. Ratings, Wow, Effort and Build wave are the author's judgment and have **not been tested with real recipients** (unverified).

## Format notes

- Every CSV is one record per line. Line breaks inside a cell are stored as the two characters `\n`.
- `*-details.csv` files are keyed by `id` and hold the long fields. Load them only for the rows you need.
- `theme-kits.csv` is long format: one row per option (`theme_id, axis, n, option`). Palettes live in `palettes.csv` with contrast ratios recomputed during export.
- `theme-section-fit.csv` is long format: `shines` = native to the theme, `works` = fits well, `avoid` = clashes with the DNA. Pairs not listed are neutral.

## Added from the brand demo

| Column | Meaning |
|---|---|
| `site_line` | In `sections.csv` and `themes.csv`. The one-line description the UNCARD site shows for that scene or world. Canonical product copy (`../decisions/0005-demo-is-source-of-truth.md`). |

## Section columns

| Key | Meaning |
|---|---|
| `ID` | S01 to S50. Stable, so other sheets can refer to it. |
| `Section` | The name the site uses for the section. |
| `Category` | Openers, Stories & Cartoons, Roasts & Reveals, Fake Formats, Games, Quizzes, Music & Sound, Heart & Words, Finales. |
| `What it is` | What the recipient sees and does, and why it lands. |
| `Kids 4-8 ... Seniors 60+` | How well the section suits the RECIPIENT's age band (rating key below). For 4 to 8 year olds a grown-up may sit beside them. |
| `Gender fit` | See the gender note below. 'Neutral' unless the default look leans one way, in which case it says how to re-skin. |
| `Best for` | The giver-to-recipient relationships where the section works best. |
| `Prompt template` | Paste-ready instruction for the writing model. {PREAMBLE} is the shared rules further down this sheet. {curly} words are placeholders. The OUTPUT line is the JSON the card player would expect: ["x7"] means an array of exactly 7 strings, and [""] means a list within the limits given. |
| `When it makes sense` | Three situations where the section is a good pick. |
| `Example in action` | A short sample of what the section could say, for an imaginary recipient (Jamie, Riley, Mum and so on). Not real data. |
| `What we need from the giver` | The minimum facts. If they are missing, the section is skipped. |
| `How they use it` | What the recipient does: watch, tap, drag, type, scroll or read. |
| `Tone` | The default mood. The giver's tone choice overrides it. |
| `Sound` | None, Optional, or Core (the section is mostly sound). Anything with sound starts on a tap and needs a visual fallback. |
| `Photo` | None, Optional, or Needed. |
| `Effort` | S, M or L (key below). Relative sizes, not quotes. |
| `Build wave` | 1, 2 or 3 (key below): what the section depends on. |
| `Wow (1-5)` | My estimate of how strongly it lands. Test it with real people before trusting it. |
| `Lineage` | The part of Jordan.EXE it grows from, or 'New'. |
| `Watch-outs` | Safety, consent, accessibility and technical risks to design for. |

## Theme columns

| Key | Meaning |
|---|---|
| `ID` | T01 to T20. Stable, so other sheets can refer to it. |
| `Theme` | The name the site uses for the look. |
| `Family` | Paper & Print, Keepsakes & Handmade, Play & Games, Screens & Stage, Loud & Graphic. Themes in one family share a mood, not a look. |
| `What it is` | What the recipient sees and how it feels. |
| `Kids 4-8 ... Seniors 60+` | How well the theme suits the RECIPIENT's age band (rating key below). |
| `Gender fit` | See the gender note below. 'Neutral' unless the default look leans one way, in which case it says how to re-skin. |
| `Best for` | The recipients and relationships where the theme works best. |
| `Tone fit` | The moods the theme carries well. The giver's tone choice always wins. |
| `Prompt template` | Paste-ready instruction for the art-director model. {THEME_PREAMBLE} and {THEME_JSON} are on the 'How to use' sheet, and {KIT} stands for the six kit columns of the same row. The OUTPUT line is the JSON the card player would expect. |
| `When it makes sense` | Three situations where the theme is a good pick. |
| `Example card A / B` | Two imaginary cards from the SAME theme. Each pick is an item from the kit, and the two cards differ on all six axes. Not real data. |
| `Facts that drive the look` | Which facts about the recipient decide which kit items. This is what makes each card original. |
| `Fixed DNA` | What never changes in the theme. Everything else in the kit can bend. |
| `Palettes` | Named palettes in the form 'Name: background ink accent'. See the Palettes sheet for swatches and live contrast checks. |
| `Type pairings` | Display face + text face (+ accent face). All open-licence Google Fonts, embedded as subsets. |
| `Layouts, Motifs, Motion, Interaction` | The other four kit axes (definitions below). |
| `#Pal ... #Int` | How many options each axis has. Live formulas that count the lines in the kit cells. |
| `Look capacity` | The most cards that could all differ pairwise on at least 4 axes. An upper bound: the product of the three smallest kit sizes. |
| `Shines with / Works with / Avoid` | Sections that look best in the theme, sections that fit well, and sections that clash with the DNA. IDs refer to the Sections catalogue. The 'Theme x Section' sheet draws all 1,000 pairings. |
| `Sound, Photo, Effort, Build wave, Wow` | Same scales as the Sections catalogue, applied to the theme (key below). Wow is my estimate. |
| `Lineage` | The earlier look, spec direction or Jordan.EXE part the theme grows from, or 'New'. |
| `Watch-outs` | Safety, accessibility, legal and technical risks to design for. |

## Fit rating (age bands)

| Key | Meaning |
|---|---|
| `Great` | A natural fit. People in this age band usually love it as it is. |
| `Good` | Works well, sometimes with simpler wording, bigger targets or a grown-up reading aloud. |
| `OK` | Only if the person likes this style. Otherwise pick something else. |
| `No` | Skip for this age band (usually too much reading, too abstract, or the wrong humour). |

## Effort and build wave

Sections and themes use the same letters on **different scales**.

### Sections
| Key | Meaning |
|---|---|
| `Effort S` | Mostly text plus a small script. About a day. |
| `Effort M` | A custom interaction or animation. One to three days. |
| `Effort L` | Needs a small engine (sprites, a grid generator, music synthesis, a collection flow). Three days or more. |
| `Wave 1` | Text and code only. Simple synthesized sound effects are fine. |
| `Wave 2` | Needs photos, uploaded or recorded audio, or a synthesized music track. |
| `Wave 3` | Needs a bigger engine, generated art, an external data pack, or a way for several people to contribute. |

### Themes
| Key | Meaning |
|---|---|
| `Effort S` | Design tokens, fonts and inline SVG plus a few scene components. Days. |
| `Effort M` | A full kit of illustrated parts and scene layouts. A week or so. |
| `Effort L` | Needs a small engine or asset set (music synthesis, a character or illustration kit). Two weeks or more. |
| `Wave 1` | CSS, inline SVG, canvas and fonts only. Simple synthesized sound effects are fine. |
| `Wave 2` | Needs synthesized music, recorded audio or careful photo handling. |
| `Wave 3` | Needs a bigger engine or a generated art set (a character kit, an illustration set). |
| `Note` | Effort covers the theme's look only. Sections are built separately (Sections catalogue). |

## Why there is no gender score

I did not score sections by gender. There is no reliable rule that a boy, a girl or anyone else will like a particular section, and scoring it would push stereotypes into the product. What the site should ask for is pronouns (once, for the copy) and interests (to choose the sections). Where a section's default look can lean one way (for example arcade-style games read as 'gamer'), the Gender fit column says so and suggests a re-skin. Sections that put words in real people's mouths or lean on pronouns say that in Watch-outs.

I did not score themes by gender, for the same reason as the sections: there is no reliable rule that a boy, a girl or anyone else will like a particular look, and scoring it would push stereotypes into the product. What the site should ask for is pronouns (once, for the copy) and interests, and it should pick palettes and motifs from the person's own favourites. Where a theme's default look can lean one way (Firmware and Blueprint can read male-coded, Sticker Book can read girl-coded), the Gender fit column says so and names the re-skin. Every palette in every kit stands on its own, so no theme depends on pink for girls or blue for boys.

## Author's assumptions

**Sections**

- Ratings, Wow scores, Effort and Build wave are my judgment. Nothing here has been tested with real recipients yet. The hand-made test cards are the way to check them.
- Examples use imaginary recipients. Nothing in them is real data.
- Lineage comes from the public Jordan.EXE page and the project's Components and Inspection sheets. Those sheets note that the page's 3D stages, adult language and injury and body jokes are left out on purpose.
- Every section outputs JSON that a framework-free card player renders, so one card can still be one self-contained HTML file.
- Only Group Signature Wall (S44) needs the site to collect input from several people. Everything else is complete once the giver approves it.

**Themes**

- Ratings, Wow, Effort and Build wave are my judgment. Nothing here has been tested with real recipients yet. The hand-made test cards are the way to check them.
- Palettes were checked when built (ink on background at least 4.5:1, accent on background at least 3:1) and the Palettes sheet re-checks all 120 of them live.
- All fonts come from Google Fonts under open licences (SIL OFL or Apache 2.0) and were confirmed to exist when this file was built. Each card embeds only the subsets it uses.
- Example cards A and B use imaginary recipients. Each pair differs on all six axes.
- Look capacity is an upper bound. As a check, a simple greedy search at build time found at least 66 mutually different looks for every theme (differing pairwise on 4 or more axes), well above the 20 the fingerprint rule compares against.
- Themes change look and pacing only. Copy comes from the sections and tone comes from the giver's brief, so the same theme can be warm or roasty.
- Every theme must work inside the scene-based player (Next and Back, reader mode). Themes that suggest a hub or a map (Passport, Carnival Midway, Gallery Wall) still have a plain linear order.
- No theme uses third-party characters, logos, real brands, real films or real songs. Styles are described in general terms (pixel art, halftone, synthwave).
