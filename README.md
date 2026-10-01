# Tapcard Wiki

Project context for **UNCARD** (working name; formerly Tapcard) — personalized, interactive birthday cards that adults create for someone they love. A slideshow player renders themed scenes from a versioned card JSON; kids just open a link.

This repo is the shared brain: scope, research, decisions and conventions that people and AI agents both read.

## Docs only, on purpose

No code, no `package.json`, no scaffolding. Everything here is Markdown.

That's deliberate — the product itself lives elsewhere (see `docs/decisions/0001-source-of-truth.md`, still open). Keeping this repo code-free means it can be merged into the product repo later as a plain `docs/` folder, with nothing to untangle.

## Start here if you're an agent

**`AGENTS.md` is the entry point.** Read it first. It carries the project summary, the current milestone, the rules for working on Tapcard, and a map of which doc to load for which question. Load only the docs relevant to your task.

It is named `AGENTS.md` rather than `CLAUDE.md` because that is the filename every coding agent looks for — Claude Code, Codex, Cursor, Copilot and Gemini included. `CLAUDE.md` is a one-line pointer to it.

## File tree

```
AGENTS.md                                  Agent entry point: project, rules, doc map
CLAUDE.md                                  One-line pointer to AGENTS.md
README.md                                  This file
docs/
  index.md                                 Every doc with a one-line summary and status
  conventions.md                           How to write and update docs in this wiki
  start-here.md                            Landing page for human readers
  product/
    scope.md                               What Tapcard is, stack, constraints, phases, team
    live-product.md                        The MVP at uncard.app: what's built, stack, access, decisions
    experience.md                          Nine-beat arc, giver flow, Studio, sharing, hosting (designed)
  catalogue/
    README.md                              How sections and themes combine; how to query
    sections.csv / section-details.csv     50 sections (short form / prompts, examples)
    themes.csv / theme-details.csv         20 themes (short form / prompts, examples)
    theme-kits.csv, palettes.csv           Each theme's options on six axes
    theme-section-fit.csv                  Which sections suit which themes
    prompts.md                             Shared generation rules and output shapes
    legend.md, samples.md, reference.md    Column keys; worked examples; lineage and parked ideas
  brand/
    directions.md                          UNCARD brand: Matinee
    logos/                                 v0.1 logo pack, SVG + PNG
  research/
    competitive-landscape.md               Ecard incumbents, custom-song vendors, direct competitors, pricing implications
  decisions/
    0001-source-of-truth.md                Product repo: JNabsRepo/uncard-starter
    0002-pricing-model.md                  $5.99 per uncard, $9.99/month for two (accepted)
    0003-task-catalogue-source.md          The task list lives here, not in the spreadsheet
    0004-brand-direction.md                UNCARD, Matinee
    0005-demo-is-source-of-truth.md        Where docs disagree, the brand demo wins
  tasks/
    README.md                              How to query the 526 tasks without loading them all
    tasks.csv                              526 tasks: phase, area, owner, status, dependency
    task-details.csv                       Output, acceptance and tooling per task
    legend.md                              Column meanings and code tables
examples/
  README.md                                What the mockup is and how to use it
  uncard-demo/index.html                   The working UNCARD mockup — the line of truth (~1 MB)
index.html                                 Renders the docs above for humans; holds no content
```

## Adding to this wiki

1. Follow `docs/conventions.md` — header block, confidence markers, naming.
2. Add a row to `docs/index.md`. **A doc that isn't listed there effectively doesn't exist.**
3. Commit to `main`. No branch or review process — this is a docs repo, not production code.

**Don't hand-edit these:**

- `docs/tasks/*.csv` and `docs/catalogue/*.csv` — exported from spreadsheets. See `docs/decisions/0003-task-catalogue-source.md`.
- `examples/uncard-demo/` — a saved copy of the claude.ai artifact. Replace it with a newer save; don't edit it.
- `index.html` — the display wrapper. It reads the markdown at runtime and holds no content of its own.

**If you can't answer something, say so rather than guessing.** Mark it `(unverified)` or `(assumption)`, or add it to the `## Open questions` list at the bottom of the relevant doc. Several things in here — the backend choice in `product/scope.md`, the column meanings in `tasks/legend.md` — are inferences waiting on someone who actually knows.
