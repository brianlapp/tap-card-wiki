# How Uncard Fits Together (Architecture)

**Status:** Draft. This is a snapshot, and the product repo is the source of truth.
**Updated:** 2026-10-21
**Owner:** Brian Lapp
**Method:** Read from the product repo [`JNabsRepo/uncard-starter`](https://github.com/JNabsRepo/uncard-starter) at `origin/main` = **`84977d9`** (2026-10-19, the last Phase 3 commit). Sources: the completion folder (`CHECKPOINT.md`, `LIVE-STATE.md`, `ACTIVATION.md`, `FLAGS.md`), the Phase 3 completion report, the Stage 10 report, the build spec's architecture section, and the READMEs for the repo, `db/`, `gifts/`, `cron/`, `src/uncard/` and `tools/ci/`. The folder layout comes from `git ls-tree`. Branch `codex/m13` was read too: it is **not** on main (checked with `git merge-base --is-ancestor`). Nothing was checked in a browser or against the live database. "Live" facts are what the build agent recorded, and its last live database read was **16 Oct**. Anything newer is marked unknown.

## TL;DR

- **Almost everything is built. Almost nothing is switched on.** Phase 3 (Stages 0 to 10) is on `main` as code. It was finished by a completion run, milestones M0 to M12, from 15 to 19 Oct. The final check run passed all 71 steps on code commit `441c701`.
- **What is live:** uncard.app on Lovable, at commit **`72f02dd`** (published 18 Oct). Its database sits at **80 applied migrations** (as last read on 16 Oct). On 20 Oct Jordan reported in Slack that Phase 3 is finished and that Manus and Devin are live-testing uncard.app, so a newer publish is likely, but no commit is recorded. The studio is closed. No model is called and no payment is possible. The new features stay off.
- **What waits:** **64 SQL files** for Stages 4 to 10 are written, reviewed and rehearsed, but none is applied. Each wave goes out at a release point: **R1** (studio, part done), **R2** (privacy, checkout in test mode, recipients) or **R3** (gallery, contributors, memory, agents). Each one needs publishes, Cloudflare steps and secrets (done with the owner login or Jordan's accounts), plus a named yes for its SQL.
- **uncard.gifts is built but not serving cards.** The `uncard-gifts` Worker code is in the repo. Cloudflare has not rebuilt it since 2 Oct, and the nightly `uncard-cron` Worker does not exist yet.

## The moving parts

| Part | What it is | State (as of the sources) |
|---|---|---|
| **uncard.app** | The website, the studio, the account and admin pages, and every server route. TanStack Start (React, Vite, TypeScript), built and hosted by **Lovable**. Commits sync both ways with GitHub `main`. | Published commit **`72f02dd`** (code `2412961`, through M7). Main's head `84977d9` (with the M8 to M12 code) is **not confirmed published**. Publishing it is optional before R2. |
| **Database** | **Lovable Cloud = Supabase Postgres** (PostgreSQL 17.11 on the 15 Oct read). Migrations are Drizzle files Lovable writes when it applies one. | 80 migrations (0000 to 0079), with the fingerprint equal to the repo on 16 Oct. Two more files (0080, 0081) are staged in `db/pending/`. |
| **uncard.gifts** | Cloudflare Worker **`uncard-gifts`** (`gifts/`). It serves the card page, the PIN form, the "not here" page and, later, the gallery. It has **no database key**. It asks uncard.app through a private API (`/api/gifts/v1/*`) with a shared secret. | Code is ready. In Cloudflare, `uncard-gifts` was last changed on 2 Oct. Whether it builds from `workers-live` is **unknown**. Card links still open on `uncard.app/c/<id>` until the owner switch `cards_on_gifts` is on. |
| **Nightly job** | Cloudflare Worker **`uncard-cron`** (`cron/`). Every day at 07:17 UTC it calls uncard.app's `/api/cron/*` routes. They copy data to a private R2 bucket, **`uncard-lake`**, and roll up the metrics. | **Not created.** Whether the bucket exists is unknown. |
| **`workers-live` branch** | The branch both Workers deploy from. It only ever moves forward, to a commit that has already been published. | At `72f02dd` (matches the published site). |
| **AI** | The **Lovable AI gateway**. The default model in code is `openai/gpt-6-astra` (`src/uncard/generator/model.ts`). Tests use a pretend gateway. | Closed. Generation is off, the conversation budget is off, and no prompt pack is approved. Studio spend (OD-03) is "Not yet". |
| **Payments** | Stripe, **test mode only** (Stage 5). | Built, closed. Nothing is set up. Real money is a later gate (S5-X1). |
| **DNS** | Both domains are on Cloudflare. | See `live-product.md`. |

## The diagram

```
 WHO               LANDS ON                                  TALKS TO
 ───────────────   ───────────────────────────────────────   ──────────────────────────────────
 Sender         ─► uncard.app (Lovable hosting)             ─► Lovable Cloud Postgres (Supabase)
                   pages, /make studio, /account, /admin,       row-level security on every table;
                   /api/*  (server code holds the keys)         writes only through server code or
                                                                security-definer functions
                                                            ─► Lovable AI gateway (spend closed)

 Recipient      ─► uncard.gifts (Worker "uncard-gifts")     ─► uncard.app /api/gifts/v1/*
                   card page, PIN form, gallery later           (shared secret; the Worker has
                   strict CSP; AI crawlers get 403              no database key)
                   (until then: uncard.app/c/<id>)

 Outside AI app ─► uncard.app /oauth, /api/v1, /mcp         ─► the same server code and database
 (built, off)      owner approves it on /account/agents         the studio uses

 Nightly job    ─► Worker "uncard-cron", 07:17 UTC          ─► uncard.app /api/cron/*  ─►  R2 "uncard-lake"
 (not created)
```

## How a card gets made and given

This is the path as built. Where a step is switched off today, it says so.

1. **A sender opens uncard.app.** The home page asks who they are making something for, and their answer opens the studio at `/make`.
2. **The studio asks the server whether it is open.** The server checks the studio status, so the code never decides this. Today the answer is **closed**: `studio_settings.open` and `generation_settings.enabled` are both off, so the sender sees the invite-only screen. When it opens, it lets in staff and Golden Pass holders who are 18+.
3. **The sender talks about their person.** A studio "partner" (an AI, through the gateway) asks one question at a time. Facts, messages and the birthday are saved as the conversation goes. Partner replies also need a conversation budget and an approved prompt pack. Neither is set yet.
4. **Ideas, then a build.** The partner offers idea cards. The sender picks one, and the creative engine writes an **UncardSpec v2** design. It is checked by a validator against 25 building blocks (primitives), and its pictures go through an SVG cleaner. It plays live in the preview on the **v2 player**. Every model call is recorded with its role, model, pack and cost.
5. **Shape it.** Edit text by tapping it, lock moments, try another direction and compare, undo. Each change is a new saved version.
6. **Ready to give.** A review card shows the exact uncard and a checklist, and the sender approves it. Checkout comes next: built, but test mode and closed. Staff and Golden Pass holders skip payment.
7. **Give.** The approved version is published as an "edition" with a private link and an optional PIN. Who can see it (private, link, shareable, gallery) is Stage 4/6 work, and it is off.
8. **The recipient opens the link.** Today that is `uncard.app/c/<id>`. Once the gifts Worker is live and the owner turns on `cards_on_gifts`, links move to `uncard.gifts/<id>`. The Worker asks uncard.app for the card through the private API, then plays it with the same player code the site uses. Card pages load no sign-in code.
9. **Later, all built and off:** the recipient taps "It's mine" to save it on uncard.app (Stage 6). Friends sign or add a memory at `/add/<token>` (Stage 8). The studio remembers people for next year (Stage 9). Senders offer uncards to the gallery, and staff write search pages at `/discover/<slug>` that the owner approves (Stage 7). Or the sender does it all from ChatGPT or Claude (Stage 10).

## Where things live in the code

| Path | What it holds |
|---|---|
| `src/routes/` | One file per page or API route (TanStack file routing). Includes `/make`, `/account`, `/admin*`, `/c/$cardId`, `/mine/$cardId`, `/add/$token`, `/discover/$slug`, `/memory`, `/agents`, `/mcp`, `/oauth.*`, `/api/v1/*`, `/api/gifts/v1/*`, `/api/cron/*` |
| `src/lib/*.functions.ts` | Server functions the pages call (studio, creative, billing, gallery, contributors, admin and more) |
| `src/uncard/site/` | Pages, the studio's screens (`site/make/`), the admin screens |
| `src/uncard/conversation/`, `studio/`, `ops/` | The studio partner loop and its gateway, studio state, and the command layer every surface uses |
| `src/uncard/creative/`, `generator/` | UncardSpec v2 (validator, primitives, SVG, pipeline, prompt packs), plus the older generator and the model plan |
| `src/uncard/player/`, `player-v2/` | The card players. They are plain code with no framework, so the Worker can use the same files |
| `src/uncard/delivery/`, `measure/`, `billing/` | Links and the gifts contract, gallery doors, crawler list; measurement, consent, ad adapters; checkout (test mode) |
| `src/uncard/contributors/`, `memory/`, `agents/` | Stages 8, 9 and 10 |
| `gifts/`, `cron/` | The two Cloudflare Workers, each with its own packages and deploy |
| `drizzle/migrations/` | The 80 applied migrations (0000 to 0079) |
| `db/pending/`, `db/proposals/`, `db/tests/` | 2 staged files, 141 proposal files (the unapplied Stage 3 to 10 SQL and the reviewed originals of applied ones), 73 SQL test files |
| `tools/ci/`, `tools/db/`, `tools/qa/` | The check runner, the database checks (races and mutation kits), and the browser journeys |
| `docs/phase-3/` | The build spec, the stage reports, and `completion/` (checkpoint, flags, packets, receipts) |

## The data layer

- **Main table groups:** accounts and roles (`profiles`, `user_roles`, `golden_passes`, `admin_audit`); the studio and cards (`card_roots`, `card_versions`, `card_publications`, `conversations`, `messages`, `facts`, `people`); generation and spend (`generation_*`, `creative_*`, `studio_spend_*`, `model_prices`, `prompt_packs`); measurement and the lake (`analytics_*`, `lake_*`, `modelled_*`); evaluation (`eval_*`); and switches (`studio_settings`, `generation_settings`, `conversation_budget_settings`). The 15 Oct fingerprint counted **73 tables and 356 functions** at migration 0076.
- **The security pattern** (`db/README.md`, "Rules the schema follows"):
  - Every table has row-level security on, and people read only their own rows.
  - **The browser never writes** account, job, allowance or card tables. Writes go through `security definer` functions, or through server code that checks the caller first and then uses the service role. Server code passes in who is asking (`_actor`), and the browser never names itself.
  - **The browser can call only a short allow-list of database functions.** Every migration is checked against that list.
  - Roles live only in `user_roles`. Exactly one owner exists, enforced by a unique index. Every admin change writes an `admin_audit` row in the same transaction.
  - A new table that holds personal data must join the account-erase path in the same migration.
- **How SQL reaches the live database:** each file is sent to Lovable's agent, one per message. Before that comes a rolled-back rehearsal on the live database. After it come a byte-for-byte compare, the schema fingerprint and Lovable's security scan. The process stops on any difference. Files stay under about 35 KB.

## Feature switches, and what each stage turns on

There are five kinds of switch. Some are **owner-only doors in the database**, which need the owner login and are audited. Some are **app settings in Lovable**, some are **Worker settings in Cloudflare**, and some are **build-time `VITE_*` flags** (how these reach the published build is unknown). The last kind is **code constants** (`LEGAL_APPROVED`, `CONTACT_EMAIL`). The full list is in [`FLAGS.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/phase-3/completion/FLAGS.md).

| Stage | What it opens | Main switches | SQL | Release |
|---|---|---|---|---|
| 2–3 Studio and engine | The conversation studio, renderer v2, the lab | `studio_settings.open`, `generation_settings.enabled` (owner); conversation budget; prompt-pack approval | Applied (to 0079) + 2 staged | R1, then studio spend (OD-03) |
| Gifts host | Cards served on uncard.gifts | `cards_on_gifts` (owner); a shared secret set on both sides | — | R1 |
| 4 Consent and measurement | Consent banner, recipient counts, ad sets, visibility levels | `LEGAL_APPROVED` (code), `APP_CONSENT_LIVE_READY`, `RECIPIENT_MEASUREMENT_READY`, `AD_SOURCE_LIVE_READY` | 12 files | R2 |
| 5 Checkout (test mode) | Checkout, sandbox billing, Apple sign-in, passkeys | `UNCARD_TEST_BILLING_*`, `UNCARD_AUTH_APPLE_READY`, `UNCARD_AUTH_PASSKEY_READY` | 9 files | R2 |
| 6 Recipients | "It's mine", saved and received uncards, share tiles | `UNCARD_RECIPIENT_ACCOUNTS_READY`, `UNCARD_SHARE_TILES_READY` + Worker `SHARE_TILES_READY` | 3 files | R2 |
| 7 Discovery | Gallery on uncard.gifts, search pages, sitemaps | `UNCARD_GALLERY_DRAFTS_READY`, `UNCARD_GALLERY_READY`, Worker `GALLERY_READY`, `UNCARD_SEARCH_PAGES_*` | 3 files | R3 |
| 8 Contributors | Invites, guest page, review tray, include | `UNCARD_CONTRIBUTOR_*` (all must be on) | 8 files | R3 |
| 9 Memory | Remember?, What I'm using, `/memory` | `UNCARD_SENDER_MEMORY_*` | 12 files | R3 |
| 10 Agents | OAuth, REST, MCP, `/agents`, `/account/agents` | `UNCARD_AGENT_GRANTS_READY`, `_OAUTH_READY`, `_OPS_READY` | 17 files | R3 |

While a switch is off, its pages answer "not found" or "not available", and no button should lead to a dead end. `FLAGS.md` section 13 lists the few places that still do (for example, the studio's photo upload always fails today because no storage bucket exists).

## The release path

Rules for every step (`ACTIVATION.md`): **publish first, then move `workers-live`**, forward only and checked with `git merge-base --is-ancestor`. Apply one SQL file per message. Turn on one switch at a time, with its check after it. Every step has a written rollback.

| Release | Carries | Done | Still open |
|---|---|---|---|
| **R1** studio | Stages 1–3 path, the gifts Worker, spend records | Published `72f02dd` (18 Oct). `workers-live` moved. M2 SQL files 1–3 applied (16 Oct) | Cloudflare steps (plan, R2 bucket, both Workers building from `workers-live`, AI-bot policy). Two secrets. Six smoke checks (never run, because the build agent cannot reach the live sites). One read-only live query (X-02). M2 files 4–5. The **Stage 3 contraction** (13 messages, which retire old names and columns; the yes for the drops is recorded on 17 Oct) |
| **R2** privacy, commerce, recipients | Stages 4, 5, 6 | Code and packets | 24 SQL files. Counsel's Terms and Privacy text, then `LEGAL_APPROVED`. Stripe test keys. A publish |
| **R3** discovery, collaboration | Stages 7–10 | Code and packets | 40 SQL files (Stage 9 needs the contraction first). Cloudflare rate-limit rules. Crawler setting and Search Console. Approval of each search page. Connecting ChatGPT and Claude (`OP-AGENTS.md`) |
| After R3 | — | — | Opening the studio and any paid model call (OD-03). Real-money Stripe (S5-X1). The photo bucket (OD-19) |

**What waits on whom.** The decisions belong to the partners. The packets assign the *actions* like this:

- **Jordan:** publishing in Lovable, the Cloudflare account steps, setting secrets and app switches in the Lovable project, the owner-only database switches, the phone checks, and sending the named yes lines. These are his because he holds the owner login and those accounts.
- **The build agent:** applying SQL through Lovable's agent, moving `workers-live`, and the web smoke checks.
- **Counsel:** the legal text.

If nobody does anything, the site stays as it is: studio closed, no payments, no new data collected and no model spend.

## The agent doors (Stage 10, M11)

- **What:** ChatGPT, Claude or a script connects to Uncard and works on an owner's uncards. The **same 15 operations** run over REST at `/api/v1` and over MCP at `/mcp`. A guide lives at `/agents` and `/agents.md`. These are routes on uncard.app itself, with no separate Worker in front.
- **Sign-in:** OAuth with public clients and PKCE. An app registers itself (rate-capped), then sends the owner to Uncard's own **Connect** page to approve read, create or edit rights for all uncards or for chosen ones. Access tokens last 1 hour. Refresh tokens last 30 days and are replaced each use. A grant lasts until the owner revokes it on `/account/agents`.
- **Never allowed:** paying, publishing, changing who can see a card, inviting people, reading another owner's uncards, or writing memory (imported notes wait until the owner accepts them). The two steps that spend money (`propose_ideas`, `generate_uncard`) are refused while studio spend is closed.
- **Records:** every write takes an idempotency key, and every call is logged for 90 days.
- **State:** 17 SQL files at L3, three switches off. A scripted client passes the 140-check journey. ChatGPT and Claude have **not** connected yet (OD-15).

## How the build is checked

- **Exact-source runs, not GitHub Actions** (stopped 9 Oct). `tools/ci/gates.sh` has four profiles: `static`, `db`, `browser:<suites>` and `full`. Each run writes a receipt for one exact commit into `docs/phase-3/completion/receipts/`.
- **`full` = 71 steps, about 5 hours.** It covers types, lint, builds, offline checks, the SQL tests in two time zones and **races** on a real PostgreSQL 16 (20 connections at once, plus "control" copies with one lock removed that the races must catch). It also covers **mutation kits** (deliberately broken copies of SQL that the tests must catch; for example, agent sign-in caught 101 of 101) and **browser journeys** at 390, 320 and 1280 px wide, with zero outside requests allowed.
- **Reviews:** at M12, six fresh reviewers went over the high-risk areas. There was no blocker. They found 36 issues: 9 were fixed with a check, 3 were partly fixed in the app, and 24 were recorded with an owner and a closing condition (summed up as K1 to K12).

## In progress: branch `codex/m13` (not on main)

Four commits by Jordan's Codex on 20 Oct, about 225 files changed. Its own report says **"In progress; source completion is not yet claimed."** It aims at:

- honest public pages (planned prices in CAD, and the studio shown as closed before anyone types a brief);
- six fully authored sample uncards;
- an invite-only studio test window with owner spend controls (window closed, paid allowance 0);
- new SQL packets (unapplied).

Nothing in it is merged, published or applied.

## Known open items

- **X-02:** no live database read since 16 Oct. One read-only query closes it (`packets/OD05-live-precheck.md`).
- **No live smoke check has ever run on the published `72f02dd`,** and the five deployment facts in `packets/M1-owner-readonly.md` are unanswered.
- **K4:** may a child's uncard be listed in the gallery? The spec says yes with a guardian's tick, and the report asks for a ruling before the gallery opens.
- **Placeholders:** `CONTACT_EMAIL` is still `[contact email]` (OD-20), so no "Report this uncard" link shows. `LEGAL_APPROVED` is false until counsel's text arrives (OD-08).
- **No storage bucket:** photo upload fails closed (OD-19).
- **Recorded limits K1 to K12** (completion report, section 6, in the private product repo): each has an owner and a closing condition, and none can be reached while the doors stay closed.
- **One test repair** (`lab-flow`) sits on branch `sonnet/m11-agents`, not on main, and rides with the next code change.

## Open questions

- Which commit is published now? It was `72f02dd` on 18 Oct. Jordan's 20 Oct report of live testing suggests a newer one; which one is unknown.
- Does `uncard-gifts` build from `workers-live`? Does the `uncard-lake` bucket exist?
- How do `VITE_*` build flags reach the published build?
- The sources disagree on the rate-limit rules: R3 and `ACTIVATION.md` list **three**, while the completion report's K8 lists **four** (adding `/api/v1` and `/mcp` before agents are offered beyond the owner).
- Brian is Domain Administrator on both Cloudflare zones (`live-product.md`). Whether that lets him set the rate-limit rules, so they don't all wait on Jordan's account, is unverified.

## Sources

All at `84977d9` unless noted. Links go to `main`, which may have moved since.

- [`docs/phase-3/completion/CHECKPOINT.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/phase-3/completion/CHECKPOINT.md), [`LIVE-STATE.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/phase-3/completion/LIVE-STATE.md), [`ACTIVATION.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/phase-3/completion/ACTIVATION.md), [`FLAGS.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/phase-3/completion/FLAGS.md)
- [`docs/phase-3/build-reports/phase-3-completion.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/phase-3/build-reports/phase-3-completion.md), [`stage-10.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/phase-3/build-reports/stage-10.md)
- [`docs/phase-3/build-spec.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/phase-3/build-spec.md) (sections 4 and 5), [`docs/phase-3/completion/COMPLETION-SPEC.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/phase-3/completion/COMPLETION-SPEC.md)
- [`db/README.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/db/README.md), [`gifts/README.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/gifts/README.md), [`cron/README.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/cron/README.md), [`tools/ci/README.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/tools/ci/README.md), [`src/uncard/README.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/src/uncard/README.md)
- Branch `codex/m13` at `21c7f56`: [`docs/phase-3/build-reports/m13.md`](https://github.com/JNabsRepo/uncard-starter/blob/codex/m13/docs/phase-3/build-reports/m13.md)
