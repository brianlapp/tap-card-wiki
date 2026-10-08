# AGENTS.md

Context for AI agents working in this repo. Read this first, then load only the linked docs relevant to the task.

## Project

**UNCARD** (working name since 2026-09-29; formerly Tapcard) — personalized, interactive birthday cards that adults create for someone they love. A player renders usually 8 to 10 scenes from a versioned card JSON: sections (the content) inside a theme (the look). Recipients open a link. No child accounts.

The repo, file names and older docs still say Tapcard. Same product.

**Team:** Jordan, Brian and Tim are equal partners. Jordan holds the app's single *owner* login, so switches that need that login wait on him; decisions don't. Brian leads engineering and infrastructure.

**Current milestone:** one synthetic test card working end to end (create → preview → publish → play → export). Nothing else ships first.

## Agent rules: read these first

`docs/agent-rules.md`, agreed by all three partners on 2026-10-07. In short: production is Brian's lane; agents never change a database without their partner's yes to that exact change; **agent-to-agent talk goes on the notice board, not Slack** (Slack is for the partners); **no Slack post without the partner's approval, written in plain words a 10-year-old could follow, with no bare code names** (say "the team brain decision", not "0007"); nothing is agreed until all three partners say yes.

## Workspace: two repos, one set of instructions

| Repo | What it holds | Who pushes to `main` |
|---|---|---|
| [`brianlapp/tap-card-wiki`](https://github.com/brianlapp/tap-card-wiki) (this one) | Project context: scope, research, decisions, catalogue, brand, the demo. **No code.** | Brian's agents, directly |
| [`JNabsRepo/uncard-starter`](https://github.com/JNabsRepo/uncard-starter) | The product, live at **uncard.app**. Lovable-synced. Has its own build docs in `docs/review-2026-09-30/` | **Jordan's build agent and Lovable only.** Everyone else: branch, then pull request |

This file is the shared instructions for both. There is no orchestrator agent: one agent, plugged straight into the repos, reading this. *(Proposed change, Open: Brian's Claude Code as team lead with sub-agents — `docs/decisions/0008-agent-team-orchestrator.md`.)*

Two private support repos sit beside these, for Brian's agents: `brianlapp/uncard-brain` (the team brain, `0007`) and `brianlapp/agent-team` (the orchestrator template, `0008`). Locally they live in `~/uncard/` too.

**How the workspace is laid out**
- **Local:** `~/uncard/` holds both clones and a one-line `CLAUDE.md` that points here. Run `claude` from `~/uncard/`.
  Keep the clones out of iCloud-synced folders (`~/Documents`, `~/Desktop`): iCloud offloads git's pack files and git then hangs or reports a corrupt repo.
- **Cloud or phone:** start the session with **both repos selected**.

**Habits**
- **Pull both repos before you start. Commit and push before you stop** or switch device. Cloud sessions are thrown away; unpushed work is lost.
- **Product repo:** never push to `main`, never force-push, never rewrite history. `main` is the live site and Lovable syncs it. Work on a branch and open a PR.
- **Where the repos disagree:** build status and code → the product repo. Project context and history → this wiki. On any fact, newest wins (`docs/decisions/0005`). Flag a contradiction; don't silently pick a side.
- **Don't copy the product repo's build docs here.** They change daily. Link to them.

## Doc map

| Need | Read |
|---|---|
| What we're building, stack, constraints | `docs/product/scope.md` |
| Who we compete with, pricing reality | `docs/research/competitive-landscape.md` |
| What's built and live today (snapshot) | `docs/product/live-product.md` |
| What the giver and recipient should experience (designed) | `docs/product/experience.md` |
| What a card is made of: 50 sections, 20 themes | `docs/catalogue/` — **grep, do not read whole** |
| Generating a card: prompt rules and output shapes | `docs/catalogue/prompts.md` |
| Name, logo, colours, voice (brand: **Matinee**) | `docs/brand/directions.md` (v1.0 guide + system detail: `docs/brand/brand-guide.md`) |
| Business/growth plans not for the public (domain, SEO, growth, investor) | `docs/strategy/` — **growth-strategy and investor-deck stay out of this public wiki; everything else in there is fine to read** |
| What's built and being built now, the active work list | Product repo: `docs/review-2026-09-30/` in [`uncard-starter`](https://github.com/JNabsRepo/uncard-starter) |
| The working mockup — what the build reproduces | `examples/uncard-demo/` (~1 MB; content already extracted into the docs above) |
| Why a choice was made | `docs/decisions/` (numbered ADRs) |
| What the team said in Slack: decisions, open asks, who owes what | `docs/slack/ledger.md` (day logs beside it) |
| How to write/update these docs | `docs/conventions.md` |
| A task: what it is, who owns it, what blocks it | `docs/tasks/` — **grep, do not read whole** |
| Full 526-task build catalogue | `docs/tasks/tasks.csv` (exported; do not use the Sheet) |

`docs/index.md` lists every doc with a one-line summary. When you add a doc, add it there too.

## The team brain (shared memory + agent bulletin board)

If your client has the **Uncard brain** connector (an MCP server; see `docs/decisions/0007-team-brain-on-supabase.md`):
- **At session start:** call `whoami`, then `board_read`, and ack what you read. Posts there are asks and handoffs from the other partners' agents.
- **Before you stop:** check the board again, and post handoffs, asks or FYIs for the agent who should pick them up.
- **Before asking a partner something,** `search` the brain: it holds this wiki, the Slack history and the private files that can't live here.
- Record decisions and open questions with `add_claim`, always with evidence. Never put secrets on the board or in claims.
- No connector yet? Ask Brian for your agent's link (sent privately, never in a channel).

## Rules for agents

- **Newest wins.** Where sources disagree: product repo → brand demo → catalogues → build catalogue. Older statements are marked superseded, not deleted (`docs/decisions/0005`).
- **The brand is Matinee.** Yellow Marquee field, Ink type, Tomato full stop (main button colour under review). Midnight is rejected. The gift itself wears its world, not the brand.
- **Speak the product's words.** In anything user-facing: *uncard, scene, world, your person, give*. Never *e-card, template, AI-generated, content, user*. File names and IDs keep *section/theme*.

- **There is no staging.** The product publishes straight to the live site. Never run anything against the live database, production credentials or billing. AI spending, anyone's access and legal text are partner decisions: agents never make them alone. Need something from a partner? Post the ask with the link and steps; don't stall.
- **No invented facts.** If a number, status or capability is unverified, write "unverified" rather than guessing.
- **Server-side AI only.** No generated code executes in the recipient's browser.
- **Privacy is a hard gate.** No child logins, no child contact data, no PII in telemetry.
- **Stripe is deferred.** Do not scaffold, connect or mock payments.
- **Small slices.** One thin vertical slice, working, before any parallel expansion.
- **Every change needs a rollback path.**
- **Facts come only from the giver.** In anything generated, real names, events and numbers come from the giver's facts. Flourish may exaggerate a fact, never invent one. Missing fact → skip. See `docs/catalogue/prompts.md`.
- **Never load the build catalogue spreadsheet.** It costs ~118,000 tokens and needs Jordan's Drive. Everything useful is in `docs/tasks/` — `grep '^T-002,' docs/tasks/tasks.csv` costs about 40.

## Task sizing

S = 1–2h, M = 2–4h. Anything larger gets split. A task is Done only when its acceptance criteria are met and evidence is linked — not when the code compiles.
