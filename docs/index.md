# Doc Index

Every doc in this wiki, with a one-line summary so an agent can decide what to load without opening files. Keep this current — a doc that isn't listed here effectively does not exist.

## Start here

The working mockup — the line of truth — is outside `docs/`: `examples/uncard-demo/` (see `examples/README.md`).

| Doc | Summary | Status | Updated |
|---|---|---|---|
| `start-here.md` | Landing page: what this is, why it exists, how to use it | Draft | 2026-09-30 |

## product/

| Doc | Summary | Status | Updated |
|---|---|---|---|
| `product/scope.md` | What Tapcard is, tech stack, constraints, team, phases (partly superseded — see its update note) | Draft | 2026-09-30 |
| `product/live-product.md` | The MVP at uncard.app: what works, stack, access, generator, measurement, Jordan's decisions | Draft | 2026-10-01 |
| `product/experience.md` | Nine-beat arc, giver's five steps, Studio, sharing controls, hosting and keepsake | Draft | 2026-09-30 |
| `product/user-stories.md` | Stories for the first end-to-end slice | Not written | — |
| `product/card-schema.md` | Versioned card JSON contract and scene registry | Not written | — |

## catalogue/

What a card is made of. **Grep the CSVs; don't read them whole.**

| Doc | Summary | Status | Updated |
|---|---|---|---|
| `catalogue/README.md` | How sections and themes combine, how to query, the numbers | Draft | 2026-09-30 |
| `catalogue/sections.csv` | 50 sections: category, age fit, tone, effort, wave, wow | Draft | 2026-09-30 |
| `catalogue/section-details.csv` | Prompt template, example, giver inputs, watch-outs per section | Draft | 2026-09-30 |
| `catalogue/themes.csv` | 20 themes: family, age fit, tone fit, effort, look capacity | Draft | 2026-09-30 |
| `catalogue/theme-details.csv` | Prompt template, examples, fixed DNA, watch-outs per theme | Draft | 2026-09-30 |
| `catalogue/theme-kits.csv` | Every kit option: type, layout, motif, motion, interaction | Draft | 2026-09-30 |
| `catalogue/palettes.csv` | 120 palettes with contrast ratios | Draft | 2026-09-30 |
| `catalogue/theme-section-fit.csv` | 488 theme × section pairings | Draft | 2026-09-30 |
| `catalogue/prompts.md` | Shared prompt preambles, output shape, originality rule | Draft | 2026-09-30 |
| `catalogue/legend.md` | Columns, rating scales, gender note, author's assumptions | Draft | 2026-09-30 |
| `catalogue/samples.md` | Six imaginary recipients, catalogue vs demo builds | Draft | 2026-09-30 |
| `catalogue/reference.md` | Jordan.EXE lineage and parked ideas | Draft | 2026-09-30 |

## brand/

| Doc | Summary | Status | Updated |
|---|---|---|---|
| `brand/directions.md` | UNCARD brand (Matinee): logo, colour, type, voice | Accepted | 2026-09-30 |
| `brand/logos/` | v0.1 logo pack, SVG + PNG, both directions | Draft | 2026-09-30 |

## research/

| Doc | Summary | Status | Updated |
|---|---|---|---|
| `research/competitive-landscape.md` | Ecard incumbents, custom-song vendors, one free direct competitor, pricing implications | Draft | 2026-09-30 |
| `research/competitor-teardown-ari-gateaux.md` | Hands-on teardown of personalized-birthday-games.com | Not written | — |
| `research/parent-willingness-to-pay.md` | What adults actually pay for kids' digital gifts | Not written | — |

## tasks/

Exported from the build catalogue. **Read these instead of the spreadsheet.**

| Doc | Summary | Status | Updated |
|---|---|---|---|
| `tasks/README.md` | How to query the 526 tasks; which tasks rest on superseded assumptions | Draft | 2026-09-30 |
| `tasks/tasks.csv` | 526 tasks: phase, area, owner, status, size, dependency | Draft | 2026-09-20 |
| `tasks/task-details.csv` | Output, acceptance, tooling per task, keyed by task_id | Draft | 2026-09-20 |
| `tasks/legend.md` | Column meanings, code tables, near-constant columns | Draft | 2026-09-20 |

## decisions/

| Doc | Summary | Status | Updated |
|---|---|---|---|
| `decisions/0001-source-of-truth.md` | Product repo: JNabsRepo/uncard-starter (Lovable, Supabase, live at uncard.app) | Accepted | 2026-10-01 |
| `decisions/0002-pricing-model.md` | $5.99 per uncard, $9.99/month for two | Accepted | 2026-09-30 |
| `decisions/0003-task-catalogue-source.md` | Task list lives in the repo, not the spreadsheet | Accepted | 2026-09-20 |
| `decisions/0004-brand-direction.md` | UNCARD, Matinee | Accepted | 2026-09-30 |
| `decisions/0005-demo-is-source-of-truth.md` | Where docs disagree, the brand demo wins | Accepted | 2026-09-30 |

## Status values

- **Draft** — written, not reviewed by the team
- **Accepted** — reviewed and agreed
- **Open** — a decision not yet made
- **Superseded** — replaced; links to the doc that replaced it
