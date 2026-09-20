# Tapcard Wiki

Project context for **Tapcard** — personalized, interactive birthday cards that adults create for kids. A slideshow player renders themed scenes from a versioned card JSON; kids just open a link.

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
  product/
    scope.md                               What Tapcard is, stack, constraints, phases, team
  research/
    competitive-landscape.md               Ecard incumbents, custom-song vendors, direct competitors, pricing implications
  decisions/
    0001-source-of-truth.md                Which Lovable project, repo and branch are authoritative (open)
    0002-pricing-model.md                  One-off purchase vs subscription (open)
    0003-task-catalogue-source.md          The task list lives here, not in the spreadsheet
  tasks/
    README.md                              How to query the 526 tasks without loading them all
    tasks.csv                              526 tasks: phase, area, owner, status, dependency
    task-details.csv                       Output, acceptance and tooling per task
    legend.md                              Column meanings and code tables
index.html                                 Renders the docs above for humans; holds no content
```

## Adding to this wiki

1. Follow `docs/conventions.md` — header block, confidence markers, naming.
2. Add a row to `docs/index.md`. **A doc that isn't listed there effectively doesn't exist.**
3. Commit to `main`. No branch or review process — this is a docs repo, not production code.

**Don't hand-edit these:**

- `docs/tasks/*.csv` — exported from the build catalogue. See `docs/decisions/0003-task-catalogue-source.md`.
- `index.html` — the display wrapper. It reads the markdown at runtime and holds no content of its own.

**If you can't answer something, say so rather than guessing.** Mark it `(unverified)` or `(assumption)`, or add it to the `## Open questions` list at the bottom of the relevant doc. Several things in here — the backend choice in `product/scope.md`, the column meanings in `tasks/legend.md` — are inferences waiting on someone who actually knows.
