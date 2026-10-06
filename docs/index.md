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
| `product/scope.md` | What Tapcard is, tech stack, constraints, team, phases (partly superseded — see its update note) | Draft | 2026-10-06 |
| `product/live-product.md` | The MVP at uncard.app after build Phases 1–5: studio and giving built but shut, what's waiting on Jordan | Draft | 2026-10-02 |
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
| `brand/brand-guide.md` | v1.0 brand guide + system vs. `directions.md`: new tokens, components, conflicts flagged | Draft | 2026-10-06 |
| `brand/system/` | v1.0 assets not already in `logos/`: tokens, components, illustrations, fonts (OFL), favicon | Draft | 2026-10-06 |

## research/

| Doc | Summary | Status | Updated |
|---|---|---|---|
| `research/competitive-landscape.md` | Ecard incumbents, custom-song vendors, one free direct competitor, pricing implications | Draft | 2026-09-30 |
| `research/competitor-teardown-ari-gateaux.md` | Hands-on teardown of personalized-birthday-games.com | Not written | — |
| `research/parent-willingness-to-pay.md` | What adults actually pay for kids' digital gifts | Not written | — |
| `research/creation-flow.md` | Research-backed creation flow, landing to paid: intake, AI-disclosure penalty, pricing | Draft | 2026-10-06 |
| `research/checkout.md` | Checkout research: paywall placement, payment methods, price testing, tax | Draft | 2026-10-06 |
| `research/sharing-referral-loop.md` | Sharing and referral loop design, incentives, measurement | Draft | 2026-10-06 |
| `research/recipient-attention.md` | Holding the recipient's attention: generator rules, metrics, analytics events | Draft | 2026-10-06 |

Ingested 2026-10-06 from the 2026-10-02 Slack drop (`slack/ledger.md`). Each carries the research agent's own findings, not re-verified here — see each doc's Method line and Open questions.

## strategy/

| Doc | Summary | Status | Updated |
|---|---|---|---|
| `strategy/domain-tracking-seo.md` | Domain, tracking and SEO plan: uncard.gifts vs. uncard.app, measurement, SEO/AI-answer plan | Draft | 2026-10-06 |

**Held, not ingested:** "Uncard growth strategy" (.pdf) and "UNCARD investor deck" (.pdf), both posted by Jordan in Slack #non-build-stuff on 2026-10-02 — **Held: private, not for the public wiki** (this repo is public; see `slack/ledger.md`).

## slack/

Running summary of the team Slack. **Start with the ledger.**

| Doc | Summary | Status | Updated |
|---|---|---|---|
| `slack/README.md` | How the archive works, channels, who's who, how to update it (last-read timestamps) | Draft | 2026-10-06 |
| `slack/ledger.md` | Decisions made in Slack, open questions, action items, files waiting to be ingested | Draft | 2026-10-06 |
| `slack/2026-09.md` | Day-by-day log, 21–30 Sep: wiki, brand demos, build kickoff, Golden Pass, Oy's testing plan | Draft | 2026-10-06 |
| `slack/2026-10.md` | Day-by-day log from 1 Oct: research drop, Cloudflare Worker, uncard.gifts slice 1, music research | Draft | 2026-10-06 |

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
| `decisions/0006-gifts-on-uncard-gifts.md` | ~~Gift links via the `uncard-gifts` Worker~~ — superseded by Jordan's plan (`strategy/domain-tracking-seo.md`): uncard.gifts on a second Lovable project | Superseded | 2026-10-06 |

## Status values

- **Draft** — written, not reviewed by the team
- **Accepted** — reviewed and agreed
- **Open** — a decision not yet made
- **Superseded** — replaced; links to the doc that replaced it
