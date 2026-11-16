# Repos: Where to Work

**Status:** Draft
**Updated:** 2026-11-09
**Owner:** Brian Lapp
**Method:** Checked with the GitHub API, signed in as `brianlapp`, on 2026-11-06: each repo's visibility, default branch and collaborator list with roles. Branches, authors and dates come from `git` on each repo's `origin`. Live sites were checked with `curl` (build.uncard.app/agents answered 200 on 2026-11-05). Not checked: pending GitHub invites (the collaborator list doesn't show them) and Lovable's own project settings.

## TL;DR

- **Uncard has four repos we can see, plus a fifth that Brian's account can't.** The TY Growth Engine lives in `JNabsRepo/uncard-growth-engine` (named on the Roadmap hand-off card, 12 Nov); it returns 404 for `brianlapp` on 15 Nov.
- **Uncard has four repos.** Two hold apps and sync with Lovable. Both are Jordan's and private: the product (uncard.app) and the Roadmap app (build.uncard.app). The other two are Brian's: this public wiki and the private team brain.
- **Jordan and Brian can both push to both app repos.** Brian has write access (not admin), re-checked 2026-11-15. Tim isn't on either collaborator list.
- **Product `main` moved again after the 5 Nov freeze:** Kit 1.1 (10 Nov) and the Promotions Manager (11 Nov) were pushed straight to `main` (`e4867c71`). Brian's Claude works only through pull requests (28 open on 15 Nov) and never merges; a partner merges.
- **Pick the repo by the job** (table below). Code goes in the app repos. Facts, decisions and history go in the wiki. Agent handoffs go on the brain's notice board.

## The four repos

| Repo | What it holds | Live at | Visibility | Can push (checked 2026-11-15) | Connected to |
|---|---|---|---|---|---|
| [`JNabsRepo/uncard-starter`](https://github.com/JNabsRepo/uncard-starter) | The product: the uncard.app site, studio, show builder, admin, server routes, database migrations, and the code for the two Cloudflare Workers | uncard.app | Private | Jordan (admin), Brian (write) | Lovable, both ways, on `main`. Cloudflare Workers Builds: the cron Worker from `main` since 2 Nov; the gifts Worker from `main` or `workers-live` (the repo's sources disagree, see `architecture.md`) |
| [`JNabsRepo/uncard-team-roadmap`](https://github.com/JNabsRepo/uncard-team-roadmap) | The Roadmap app: the partners' board for ideas, plans, specs, reviews and handoffs. See `product/roadmap-app.md` | build.uncard.app | Private | Jordan (admin), Brian (write) | Lovable, on `main` |
| [`brianlapp/tap-card-wiki`](https://github.com/brianlapp/tap-card-wiki) | This wiki: scope, research, decisions, brand, catalogue, the Slack ledger. **No app code** | tap-card-wiki.netlify.app | **Public** | Brian (admin) | Netlify deploys `main`. The brain copies it in |
| `brianlapp/uncard-brain` | The team brain: the MCP server (search, docs, claims, notice board) and its daily sync jobs | An MCP connector. Each agent's link is sent privately | Private | Brian (admin) | Its own Supabase project, separate from both apps' databases |

Both app repos carry Lovable's note at the top of their `AGENTS.md`: commits pushed to the connected branch show up in Lovable's editor. Lovable's bot also commits there, latest on 2026-11-02 in both repos.

## Which repo for which job

| You want to… | Go to | Read first |
|---|---|---|
| Change how uncard.app works (pages, studio, show builder, server, Workers) | `uncard-starter` | Its `AGENTS.md`, then `product/architecture.md` here |
| Find out what's built, what's switched on, what's next | `product/architecture.md` (snapshot) | Then the product repo's own reports, which it links |
| Plan, spec, review or hand off a piece of work | The Roadmap app: its website, or its MCP connector | `product/roadmap-app.md` |
| Change the Roadmap app itself | `uncard-team-roadmap` | Its `AGENTS.md` and `docs/OVERSIGHT.md` |
| Look up a decision, research, brand, or what was said in Slack | This wiki, or `search` in the brain | `AGENTS.md` here, then `docs/index.md` |
| Leave an ask or handoff for another partner's agent | The brain's notice board (`board_post`) | `AGENTS.md` here, "The team brain" |
| Keep a private file (investor deck, growth plan) | The brain. **Never this wiki** | `decisions/0007` |

## Who builds where (`uncard-starter`)

Branch names say which builder made them. Commit authors don't always: Devin's commits show Jordan's name (with a "Devin AI" co-author line). More detail, and how each one lands on `main`: `architecture.md`, "Where builders work".

| Branch | Builder | Latest commit | Notes |
|---|---|---|---|
| `main` | Lovable's bot, plus Jordan's builders once he merges | 2026-11-11 (the Promotions Manager, `e4867c71`) | The live site's source. Lovable syncs it both ways. Lovable's bot commits here when it applies a database change |
| `devin/*` | Jordan's Devin | 2026-11-10 (Kit 1.1, on `main`) | The show builder. The Phase 3b branch (`…-show-phase3b`, last commit 7 Nov) isn't on `main` yet |
| `pm/*` (6) | Jordan's Codex (GPT 6.1 Sol) | 2026-11-11 | The Promotions Manager, all six on `main` now; they can be deleted |
| pull-request branches (no prefix, #5 to #32) | Brian's Claude Code (Opus 5.5, hourly wake job) | 2026-11-15 | 28 open pull requests, none merged. Several are stacked: merge in number order |
| `sonnet/*` (16), `studio/*` (3) | Jordan's Claude Code cloud sessions (Sonnet 5.5) | 2026-11-03 | Its checkpoint can say work is on `main` before it is. Check with `git merge-base --is-ancestor` |
| `codex/*` (18) | Jordan's Codex | 2026-10-30 | |
| `claude/*` (1) | A Claude Code session (Opus 5.5; whose account: unverified) | 2026-11-02 | `claude/no-refusals` |
| `workers-live` | Moved by hand, forward only | 2026-11-01 | Only moves to a published commit. The cron Worker moved off it to `main` on 2 Nov |
| `lovable-sync` | Lovable's bot | 2026-10-31 | 3 commits that aren't on `main`, and `main` is 105 ahead. Looks stale (unverified) |

The Roadmap repo: `main` (last commit 10 Nov) plus the branches of Brian's Claude's 12 open pull requests (#2 to #13, 11–15 Nov).

## Rules that apply in both app repos

- **Never force-push, rebase or amend commits that are already pushed.** Lovable would lose its project history.
- **Keep `main` working.** Whatever lands on `main` shows up in Lovable straight away.
- **Product repo `main`:** only Jordan's builders and Lovable push there. Everyone else works on a branch and opens a pull request (`AGENTS.md`). Brian's write access doesn't change this.
- **Never run anything against a live database.** Database changes go through Lovable's agent, and only after the partner's yes to that exact change (`agent-rules.md`).
- **Agents act when their partner asks.** They don't start work on their own. Brian's Claude runs an hourly job on Brian's standing instruction (14 Nov): it opens pull requests and posts on the brain's board, and never merges, publishes or posts in Slack.
- **Pull before you start, and push before you stop.** Cloud sessions are thrown away.

## Local clones (Brian's Mac)

- `~/dev/uncard/` holds `uncard-starter`, `uncard-team-roadmap` and `tap-card-wiki`. Work there.
- `~/uncard/uncard-brain` is the brain. Its daily sync reads its own wiki copy at `~/uncard/tap-card-wiki`, so leave that copy alone.

## Open questions

- Tim isn't a collaborator on either app repo. Does he need access? Only the repo owner can invite him.
- Is `lovable-sync` still needed, or can it go? It's Jordan's repo.
- Which branch is the Lovable project connected to? Lovable's bot commits land on `main` in both repos, but the Lovable settings themselves weren't checked.
