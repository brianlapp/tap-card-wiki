# Generation Prompts

**Status:** Draft
**Updated:** 2026-09-30
**Owner:** Brian Lapp
**Method:** Copied verbatim from the "How to use" sheets of `Card_Sections_Catalogue.xlsx` and `Card_Themes_Catalogue.xlsx`. Nothing here has been run against a model yet (unverified).

Load this only when you are generating or reviewing a card. Every section and theme prompt template (in `section-details.csv` / `theme-details.csv`) starts with one of the preambles below.

## How a card is generated

1. The site interviews the giver and builds a list of **facts** about the person.
2. It picks about **8 sections** that suit them (`sections.csv`). Missing facts → that section is skipped, never invented.
3. For each section it runs the **section prompt** → JSON copy.
4. It picks one **theme** (`themes.csv`) and runs the **theme prompt** → a ThemeSpec (the look). The theme never writes copy.
5. The player renders the sections inside the ThemeSpec as one self-contained HTML file.

## Section prompts: shared `{PREAMBLE}`

```
You write ONE section of a birthday card for {name} ({pronouns}), turning {age}, from {from} ({relationship}).
FACTS vs FLOURISH. Facts (real names, events, places, quotes, numbers about their life) may come ONLY from {facts}. Never invent them. Flourish (jokes, exaggeration, fake ticket numbers, timestamps, ratings, scores) is welcome, as long as it hangs on a real fact and does not claim a new one about their life. If you float a guess about them, set "guess": true on that item.
Never mention or hint at anything in {avoid}. No jokes about appearance, weight, health, money, death or romance unless {facts} say they are welcome. Tease kindly: the giver laughs and the recipient feels seen.
Tone: {tone}. Reading level: {reading_level}. Short sentences, plain words, no emoji, no markdown, no cliches.
If a fact this section needs is missing, return {"skip": true, "reason": "..."} instead of inventing.
Return valid JSON only, matching the OUTPUT shape in the task, plus a top-level "used_facts": [ids from {facts}].
```

### Placeholders

| Key | Meaning |
|---|---|
| `{name}` | How the giver names them (nicknames are fine). |
| `{pronouns}` | he/him, she/her or they/them. Ask once. |
| `{age}` | The age they are turning, or 'unknown'. |
| `{birthday_date}` | Day and month. |
| `{birth_year}` | Only for The Year You Were Born. |
| `{relationship}` | The giver's relationship, e.g. best friend, mum, coworker. |
| `{from}` | How the giver signs (one or more names). |
| `{facts}` | The fact list the interview built: id, kind (obsession, habit, memory, phrase, person, pet, value), label, detail. |
| `{habit} {obsession} {memory} {phrase} {person} {pet_or_object}` | The single best fact of that kind. |
| `{subject}` | Who the section is about: the recipient, a pet or a beloved object. |
| `{tone}` | For example: roasty, warm ending. |
| `{avoid}` | Things never to mention or hint at. |
| `{reading_level}` | Set from the age: picture-first for 4 to 8; simple for 9 to 12; casual for teens; plain for adults and seniors. |
| `{DATA_PACK}` | A vetted set of facts about a year (prices, songs, events). Never taken from the model's memory. |

## Theme prompts: shared `{THEME_PREAMBLE}`

```
You are the art director for ONE birthday card for {name} ({pronouns}), turning {age}, from {from} ({relationship}). You do not write the copy. You design the LOOK: a ThemeSpec that the card player renders.
ORIGINAL EVERY TIME. Pick exactly one option per axis from the KIT (palette, type, layout, motif, motion, interaction). Choose from {facts} and {tone}, not from habit, and list the fact ids behind each pick in "because". Compare with {recent_fingerprints} (the last 20 cards in this theme). Your fingerprint must differ from EVERY one of them on at least 4 of the 6 axes. If it does not, re-pick before answering.
FIXED DNA never changes. Everything else may bend. You may invent small extras (a motif drawn from a real fact, a border, a sound) if they sit inside the DNA and use only the kit's fonts.
RULES: live selectable text only, never text baked into art. Body text contrast at least 4.5:1. The name, long names and accents must fit. Motion reveals meaning and never blocks reading. Sound is opt-in with a visual fallback. No third-party characters, logos or trademarks. One self-contained file: embedded font subsets, art as inline SVG, CSS or canvas.
Tone comes from {tone}, not from the theme. Never use anything in {avoid}. Return valid JSON only.
```

### Shared output shape: `{THEME_JSON}`

Each theme adds its own extra fields after this.

```json
{"theme_id":"","fingerprint":{"palette":"","type":"","layout":"","motif":"","motion":"","interaction":""},"because":{"palette":["fact ids"],"type":[],"layout":[],"motif":[],"motion":[],"interaction":[]},"tokens":{"bg":"#","ink":"#","accent":"#","display_font":"","text_font":"","accent_font":""},"motif_seeds":["3 to 6 nouns taken from the facts"],"differs_on":0}
```

### Placeholders

| Key | Meaning |
|---|---|
| `{name}, {pronouns}, {age}, {from}, {relationship}` | As in the Sections catalogue. |
| `{facts}` | The fact list the interview built: id, kind (obsession, habit, memory, phrase, person, pet, value), label, detail. |
| `{tone}` | For example: roasty, warm ending. |
| `{avoid}` | Things never to mention or hint at. |
| `{recent_fingerprints}` | The six-axis fingerprints of the last 20 cards made in this theme, as JSON. This is what enforces originality. |
| `{KIT}` | The theme's six kit lists (Palettes, Type pairings, Layouts, Motifs, Motion, Interaction), pasted in from its row. |
| `{THEME_PREAMBLE}` | The shared rules below. |
| `{THEME_JSON}` | The shared output shape below. Each theme adds its own extra fields after it. |

## The originality rule

| Key | Meaning |
|---|---|
| `Palette` | A named set of three colours: background, ink (text) and accent. Ink on background must be at least 4.5:1 and accent on background at least 3:1 (checked live on the Palettes sheet). |
| `Type` | A display face and a text face, sometimes an accent face. Open-licence fonts only, embedded as subsets so the card stays one self-contained file. |
| `Layout` | How a scene is composed on a phone screen. |
| `Motif` | The drawn or decorative vocabulary, chosen from the recipient's own world (their habits, places and objects). |
| `Motion` | How things arrive and change. One signature move per scene. Always off or reduced when the device asks for reduced motion. |
| `Interaction` | What the recipient does to move on or reveal something. Every interaction has a plain Next button as a fallback. |
| `Fingerprint rule` | A card's fingerprint is its one pick per axis. The site rejects a card that differs on fewer than 4 axes from ANY of the last 20 cards in that theme, and re-picks. |
| `Where variety comes from` | Not from randomness. Each axis has a derivation rule tied to the recipient's facts ('Facts that drive the look'), so two different people land on different picks for reasons the giver can recognize. |

## Reading the templates in the CSVs

Templates are stored one per line: real line breaks are written as the two characters `\n`. Swap them back before sending a template to a model.
