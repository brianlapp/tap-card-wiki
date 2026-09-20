# Tapcard Wiki

Project context for **Tapcard** — personalized, interactive birthday cards that adults create for kids. A slideshow player renders themed scenes from a versioned card JSON; kids just open a link.

This repo is the shared brain: scope, research, decisions and conventions that people and AI agents both read.

## Docs only, on purpose

No code, no `package.json`, no scaffolding. Everything here is Markdown.

That's deliberate — the product itself lives elsewhere (see `docs/decisions/0001-source-of-truth.md`, still open). Keeping this repo code-free means it can be merged into the product repo later as a plain `docs/` folder, with nothing to untangle.

## Start here if you're an agent

**`CLAUDE.md` is the entry point.** Read it first. It carries the project summary, the current milestone, the rules for working on Tapcard, and a map of which doc to load for which question. Load only the docs relevant to your task.

## File tree

```
CLAUDE.md                                  Agent entry point: project, rules, doc map
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
```

## Adding a doc

Follow `docs/conventions.md` — header block, confidence markers, naming — and add a row to `docs/index.md`. A doc that isn't listed in the index effectively doesn't exist.
