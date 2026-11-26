# How Uncard Fits Together (Architecture)

**Status:** Draft. This is a snapshot, and the product repo is the source of truth.
**Updated:** 2026-11-23
**Owner:** Brian Lapp
**Method:** 2026-11-23 refresh: read from the product repo [`JNabsRepo/uncard-starter`](https://github.com/JNabsRepo/uncard-starter) at `origin/main` = **`327d4a47`** (22 Nov), 577 commits after `e4867c71` (11 Nov). Read: `docs/README.md`, `db/applied.txt`, `db/pending/`, the top of `db/README.md`, the specs and hand-backs of the Studio fix (`docs/studio-fix/`), the new look (`docs/look/`), Build 6 (`docs/build-6/`) and Build 7 (`docs/build-7/`), `cron/`, `gifts/` and `photo-convert/` READMEs, `tools/ci/README.md`, the first-parent log and its merge messages, and `gh pr list` and `git merge-base` on 23 Nov. Live facts marked "the Roadmap, 22 Nov" come from the team's Roadmap. Nothing was checked in a browser or against the live database for this refresh. Older refreshes (15 Nov at `e4867c71`, 6 Nov at `6e0997d6`) are kept below as history, marked with their dates.

## TL;DR

- **Since 11 Nov about fifty pull requests and four builds reached `main`.** On 18 Nov Brian's Claude merged every open pull request into one "integration base"; it became `main` on 19 Nov (#57). The new look (UR-34) landed on top on 19–20 Nov, then Build 6 (UR-38, 21 Nov) and Build 7 (UR-39, 21–22 Nov). Six more pull requests merged on 22 Nov (#68 to #73). `main` = `327d4a47`.
- **What a giver gets on `main`:** a choice of Quick & Easy or The Full Experience; a progress bar that fills at six details; a card as long as what the giver gave (3 to 8 moments); Colour and Energy sliders with no AI call; one look on every screen; the first reply and a finished card arrive with no press.
- **One age rule (Build 6):** anyone 13 or older can do everything an adult can. Under 13 is the only refusal. A child's uncard stays a child's uncard, and the review reads every word a child will see.
- **What is live** (the Roadmap, 22 Nov): Build 7 is published, and Jordan publishes `327d4a47` next. Every SQL file up to **0175** is live (`db/applied.txt`). The site is team-only: nobody else can sign up. No uncard has been made on the live site since 18 Nov.
- **The Workers** (the Roadmap, 22 Nov): the cron Worker deploys from `main` and was last deployed 22 Nov. The nightly job has run 22 times; the last 7 nights ended "partial" (cause not read yet). The gifts Worker runs 2 Oct code, so cards open on uncard.app. There is no photo converter Worker.
- **What is open:** 17 pull requests, all from Brian's side (#74 to #89 since 22 Nov, mostly checks brought up to today's screens, and #1). Build 7's questions for Jordan and Tim. Jordan's phone checks. Four groups of older database checks are still red.

## What changed since 11 Nov

| When | What landed on `main` | Builder |
|---|---|---|
| 14–17 Nov | Pull requests #5 to #39, opened for review, landed through the integration base: "Great cards from little input" parts 1 to 6c; the database and integration checks green on today's schema; Promotions Manager fixes (Toronto dates, delete rules, 44 px tabs); UX-review fixes; a guest can take their words back; a card made before "under 13" is not given as an adult's; show builder Phase 3b on today's code | Brian's Claude Code (Opus 5.5) |
| 17–18 Nov | **Studio fix** (UR-33), slices S0 to S9 (#45 to #54): each uncard has its own lane; the same problem twice ends a step with a receipt; direct answers and "Make it now"; "Update the uncard"; the Worker carries the writer's step; one paragraph, several meanings; writer pack `studio-5.1`. Then Brian's rulings and review fixes (#55) and pack `studio-5.2` (six details, tap answers, #56) | Jordan's builder (Claude Opus 5.5); Brian's Claude |
| 18–19 Nov | **The integration base** (#57): every open pull request except #1 and #11, merged into one branch. It became `main` on 19 Nov | Brian's Claude |
| 19–20 Nov | **The new look** (UR-34, slices U0 to U9, addenda 1 to 4): one set of colours, type, buttons and spacing on every screen a visitor or giver sees. The recipient's uncard is not restyled ("Yellow outside. Their world inside."). SQL 0150 to 0169 applied live on 20 Nov (UR-35). Jordan published `503dec06` on 20 Nov | Claude Code cloud sessions for Jordan (Opus 5.5), spec by Claude Fable 5.2 |
| 20 Nov | A whole-system review of `503dec06` (UR-37, #67). Build 6 was written from it; the findings are in the product repo | Jordan's Codex |
| 21 Nov | **Build 6** (UR-38), slices 0 to 8 and Part C: one age rule; under 13 the one refusal; a child's uncard stays a child's; nothing typed at the start is lost; the first reply arrives by itself; a line that lost its source is left out; the loop rule holds; a guest finds their words again on the same device; the pricing page says a free-launch link stays open. SQL 0170 to 0174, live 21 Nov | Claude Code cloud sessions for Jordan (Opus 5.5), spec by Claude Fable 5.2 |
| 21–22 Nov | **Build 7** (UR-39), slices 0 to 3 and Part C: the record of live SQL is true; a second message waits as queued words and both changes land; Move up and Move down work; a build that stopped says so; a finished card shows by itself; Home, About and Pricing say what a free-launch link does today. SQL 0175, live 22 Nov | The same |
| 22 Nov | On Jordan's instruction: #71 (the build guards), #68 (the Promotions Manager's review faults), #69 (a failed night now fails visibly; deletion replay gets "Go on"; it changes `cron/`, so the Worker redeployed), #72 and #73 (checks), #70 (the recipient's first screen is lighter) | Merged by Jordan's Claude (Fable 5.2); #68 and #69 taken to ready by Brian's Claude |

## What changed from 19 Oct to 11 Nov (history, 15 Nov refresh)

| When | What landed on `main` | Builder |
|---|---|---|
| 20–24 Oct | **M13**: honest public pages, sample uncards, an invite-only test window (pull request #3). Security pins and in-browser photo clean-up | Codex |
| 25–27 Oct | **Studio practice**: a two-pane studio, photos, the age line at 13, practice windows. The **agent door's database part** was applied on 27 Oct | Claude (Sonnet 5.5) |
| 28 Oct | **Delight**: a new card pack, a theme engine, sound, 21 new kinds of moment, sandboxed "hero" moments | Claude (Sonnet 5.5) |
| 29–30 Oct | **Big Bold Beautiful**: the shared Uncard Viewer, 20 themes, picture, music and narration paths, free-launch giving. It removed most switches, budgets and time limits | Codex |
| 30 Oct–1 Nov | Its SQL applied in parts (0112 to 0154). Then 0155 to 0160, for the cron Worker owning each model call | Claude and Lovable |
| 1–2 Nov | The Worker's minute timer switched off after an unattended build made 13 unreadable calls in a row. Then **one call per card**; the old 27-role pipeline frozen | Claude (Sonnet 5.5, Opus 5.5) |
| 3 Nov | **Show builder** Phases 1 to 3, and the show kit | Devin, Claude (Sonnet 5.5) |
| 7–10 Nov | Library security updates. **Kit 1.1**: five toys, the finale recap, opt-in weather | Devin; Claude |
| 11 Nov | **Promotions Manager** (P1 to P6), pushed to `main` without pull requests; its SQL applied live the same day | Jordan's Codex (GPT 6.1 Sol) |

## The moving parts

| Part | What it is | State (as of the sources) |
|---|---|---|
| **uncard.app** | The website, the studio, the account and admin pages, and every server route. TanStack Start (React, Vite, TypeScript), built and hosted by **Lovable**. Commits sync both ways with GitHub `main`. | **Build 7 is published**; Jordan publishes `327d4a47` next (the Roadmap, 22 Nov). Before that, `503dec06` was published on 20 Nov (Build 6 spec). Team-only: four accounts, all on the team (Build 7 spec, 21 Nov). |
| **Database** | **Lovable Cloud = Supabase Postgres.** Lovable's migration files are in `drizzle/migrations/`. Files applied with the database tool are in `db/pending/`, and `db/applied.txt` names each one that is live. | 161 migration files (0000 to 0160, none added since 1 Nov) plus 47 `db/pending/` files, **all live through 0175**. New SQL starts at 0176. From 0170 on, a file cannot be applied twice. |
| **Card-call Worker and nightly job** | Cloudflare Worker **`uncard-cron`** (`cron/`). (1) It **owns each model call**: the app wakes it, a Durable Object (one per call) streams the answer from the AI gateway, keeps it, and hands it back until the app says "saved". Since the Studio fix it also carries the Studio writer's step. (2) Every night at 07:17 UTC it copies data to a private R2 bucket, **`uncard-lake`**, and rolls up the metrics. Since #69 a failed night fails visibly. | Cloudflare's own Builds deploys it whenever `main` moves, whatever a merge touches (`cron/README.md`: the `workers-live` setting was never switched on for it). Last deployed 22 Nov. The night has run 22 times; the last 7 ended "partial", cause not read yet (the Roadmap, 22 Nov). |
| **uncard.gifts** | Cloudflare Worker **`uncard-gifts`** (`gifts/`). The card page and the PIN form; it also serves the show frame and the hero frame. It has **no database key**. It asks uncard.app through a private API with a shared secret. | **Runs 2 Oct code** (the Roadmap, 22 Nov). It deploys only when the branch `workers-live` moves (`gifts/README.md`). That branch is at `ada61906` (1 Nov): 613 commits behind Build 7 (`fa3ae351`), 653 behind `main`. Cards open on `uncard.app/c/<id>` until the owner's "Cards open on uncard.gifts" switch moves them. |
| **Photo converter** | Cloudflare Worker **`uncard-photo-convert`** (`photo-convert/`). Turns iPhone HEIC photos into JPEG for browsers that can't open them. It stores nothing. | **Not deployed:** there is no such Worker in the Cloudflare account (the Roadmap, 22 Nov). |
| **AI** | The **Lovable AI gateway**, through three "doors". No provider keys. The **route table** (`src/uncard/generator/routes.ts`, unchanged since 11 Nov) puts studio chat and review on Gemini 3.8 Flash, and show plan, build and fix on Claude Opus 5.5. The one-call card uses `openai/gpt-6-astra`. Writer packs `studio-5.1` and `studio-5.2` are registered as candidates; the app uses one only after Jordan approves it and switches it on. | One-call cards were made on the live site from 2 Nov; none since 18 Nov (the Roadmap, 22 Nov). The stop button's state today and which writer pack is on: **unknown**. |
| **Payments** | Stripe, test mode only (Stage 5 code). | **Free while we launch**: hosting is not charged, and a link stays open until the giver closes it (0118, 0135). No real money. |
| **DNS** | Both domains are on Cloudflare. | See `live-product.md`. |

## The diagram

```
 WHO               LANDS ON                                    TALKS TO
 ───────────────   ─────────────────────────────────────────   ───────────────────────────────────
 Sender         ─► uncard.app (Lovable hosting, team-only)    ─► Lovable Cloud Postgres (Supabase)
                   pages, /make studio, /account, /admin         row-level security on every table;
                   (server code holds the keys)                  writes only through server code
                   studio chat, Make, a show press ─► wakes   ─► Lovable AI gateway (one call per
                                     Worker "uncard-cron"          step; the Worker keeps the answer
                                     (one object per call)         and hands it back to uncard.app)
                   HEIC photo ─► "uncard-photo-convert" (no such Worker deployed)

 Recipient      ─► uncard.app/c/<id> today                    ─► the same server code and database
                   later: uncard.gifts, Worker "uncard-gifts" ─► uncard.app private gifts API
                   (shows and hero moments play in               (shared secret; the Worker has
                   sandboxed frames)                              no database key)

 Outside AI app ─► uncard.app /oauth, /api/v1, /mcp           ─► the same server code and database
                   owner approves it on /account/agents

 Nightly job    ─► Worker "uncard-cron", 07:17 UTC            ─► uncard.app cron doors  ─►  R2 "uncard-lake"
```

## How a card gets made and given (on `main` today)

1. **A sender opens uncard.app.** The site is team-only today (the Roadmap, 22 Nov). Start offers **Quick & Easy** (a short form: name, occasion, age, tone, a detail, closing words, Colour and Energy) or **The Full Experience** (the chat). Switching between them keeps what was typed (Build 6).
2. **The gate.** The stop button refuses chat and builds while it is closed. **One age rule** (Build 6, live 21 Nov): anyone 13 or older can do everything an adult can. A birthday under 13 is refused and not stored; the person is told to ask a parent and is signed out, and an empty account is removed. Suspended accounts can't make. Quick & Easy has no age chosen, and Make waits until the recipient's age is tapped. When a birthday and a tapped age disagree, the uncard is made for the younger.
3. **Chat.** Two panes in the new look (on a phone, two tabs). A progress bar fills at six details and says what is still to add. The first reply arrives with no press (Build 6). A second message sent while the first is being answered waits as queued words, then both changes are made (Build 7). Long answers save.
4. **One call writes the card** (since 2 Nov). Make sends one request through the cron Worker. The card is as long as what the giver gave: 3 to 8 moments (0163). A line that claims to be the giver's or a guest's own words but cannot be traced to what they told us is left out, and the giver is told which (Build 6). With the page open, a finished card shows by itself; after a while the page says "This is taking longer than usual. Check now." A build that stopped says so, with Details and Try again (Build 7, 0175).
5. **Shape it.** One cover on the Uncard pane, then the moments as rows. Edit words, lock, Move up and Move down, remove; undo, redo and history; Colour and Energy sliders (no AI call); "Update the uncard" when the details changed after a build. Full-screen play in the shared Uncard Viewer.
6. **Ready and give.** Review & give plays the uncard on top of the panel. For a child's uncard the review reads every word, playable pages included, and a flagged playable page is not kept. A card made for the wrong age is refused until it is made again. Giving uses the free-launch path: a private link, an optional PIN, open until the giver closes it.
7. **The recipient opens the link** (today `uncard.app/c/<id>`). The v2 player plays it. Since #70 (on `main`, not yet published) the first screen loads much less, and the player is fetched once the cover has drawn.

## The show builder (3 Nov, updated 23 Nov)

- **What it is.** A card made as a **show**: the recipient plays one section at a time, each built from a real story. Plan, then one build, then a free test drive, then fix only what you press. A show is a version of an uncard; sections run in a sandboxed frame on both uncard.app and uncard.gifts, from one kit (`src/uncard/show/kit/`). Paid steps go through the cron Worker.
- **Where it stands:** Phases 1 to 3, Kit 1.1 and **Phase 3b** (sound after the first tap, an always-there close button, shows read-only in the classic studio and the agent door; #34, on `main` since 19 Nov) are all staff-only Lab tools. Their SQL is live: 0137 and 0139 to 0145 (0142 to 0145 by Jordan's sweep of 7 Nov) and the show account cover (staged as 0166, live since 6 Nov).
- **Not on `main`:** Phase 4 (the sender's board) and Phase 5 (the model bake-off). No record on `main` says either was authorized or started. Phone checks for Phases 2 to 3b are Jordan's; none is recorded.

## Where things live in the code

| Path | What it holds |
|---|---|
| `src/routes/` | One file per page or API route. Includes `/make`, `/account`, `/admin*`, `/c/$cardId`, `/add/$token`, `/discover/$slug`, `/agents`, `/mcp`, `/oauth.*`, `/api/v1/*`, and the sandboxed frames `/show-frame` and `/hero-frame`. No route was added since 11 Nov |
| `src/uncard/site/` | The pages and the new look's parts, the start screen, the Studio (`site/studio/`, `site/make/`), the Back layer |
| `src/uncard/show/` | The show builder: the frozen contract, the kit, the player and test drive, the press engine |
| `src/uncard/generator/`, `src/uncard/creative/`, `src/uncard/conversation/` | The route table and gateway doors; the one-call author and its mend; the Studio's writer turn and its packs |
| `src/uncard/player/`, `player-v2/`, `themes/`, `hero/`, `audio/` | The card players, the 20 themes (and Colour and Energy), hero moments and sound |
| `cron/`, `gifts/`, `photo-convert/` | The three Cloudflare Workers, each with its own packages and deploy |
| `drizzle/migrations/`, `db/pending/`, `db/applied.txt` | Lovable's 161 migration files; the 47 files applied with the database tool; the list of which are live |
| `db/proposals/`, `db/tests/` | About 140 proposal files (never apply one as written; `db/proposals/README.md` sorts them), 130 SQL test files |
| `tools/ci/`, `tools/db/`, `tools/qa/` | The check runner, the database checks, the browser suites (now with `look/`, `build-6/`, `build-7/`) |
| `docs/README.md` | **What is current**: where plans live, what is live in the database, which documents are records |
| `docs/build-7/`, `docs/build-6/`, `docs/look/`, `docs/studio-fix/`, `docs/better-cards/`, `docs/review-2026-11-20/` | The builds since 11 Nov: spec, hand-back, how to apply the SQL, receipts |
| `docs/show-builder/`, `docs/offers/`, `docs/big-bold-beautiful/`, `docs/studio/`, `docs/phase-3/` | Earlier builds. Records, not instructions (`docs/README.md`, section 5) |

## The data layer

- **Main table groups:** as before. Accounts and roles; the studio and cards (`card_roots`, `card_versions`, `conversations`, `facts`, `people`); generation and spend (`generation_*`, `creative_*`, `model_prices`, `prompt_packs`); measurement and the lake; evaluation; settings, including `creative_settings` (the stop button); and the Promotions Manager's sixteen private tables. Build 6 added one small server-only table, the record of applied SQL files. Packs: card pack `uncard-4.1`; studio pack `studio-5.0`, with `studio-5.1` and `studio-5.2` registered as candidates.
- **The security pattern** (`db/README.md`) still holds. Row-level security is on every table. The browser never writes account, job or card tables, and can call only a short allow-list of database functions, checked on every migration. Roles live in one table, with exactly one owner. Since Build 6 one database rule decides whether a person is old enough to act, and a check fails if a second age test appears.
- **What sits in `db/pending/`** (47 files at `327d4a47`): every one is live, and `db/applied.txt` names each. Never apply one again and never edit one: a change to a live function goes in a new file. The test tools build the database two ways: **as live** (what `db/applied.txt` names) and **as next** (every file).
- **How SQL reaches the live database** (`db/README.md`, `docs/build-7/APPLY.md`): the SQL and its checks are written in `db/pending/` and `db/tests/`. On Jordan's yes, **Jordan's Claude applies each file through Lovable's database API**: a dry run that is rolled back, then the file and its checks in one guarded transaction that commits only if every check passes. Its name goes into `db/applied.txt` in the same commit as the record. From 0170 on, a second apply changes nothing. SQL is never pasted into Lovable chat.
- **Applied since 11 Nov:** 0150 to 0169 on 20 Nov (the Studio fix, better cards, the Promotions Manager follow-ons, the trust floor; UR-35); 0170 to 0174 on 21 Nov (Build 6); 0175 on 22 Nov (Build 7).

## The Promotions Manager (11 Nov, updated 23 Nov)

- **What it is.** Admin → Offers: the one place that decides what Uncard sells, at what price and on what terms. Every change is a reviewed, versioned decision. Assistants can read and draft offers through a private connection the owner grants; they never activate anything.
- **How it fits.** Sixteen private tables, closed to browser roles. Quotes are fixed when made and re-checked at payment. Real checkout (UR-15) is not built, and the order tables are not applied live.
- **State:** the four SQL files of 11 Nov are live, and so are the follow-ons for Toronto dates and delete rules (20 Nov). #68 (merged 22 Nov; it reaches the live site with the publish of `327d4a47`) fixes the review's five faults, adds "End it now" with a scheduled version and fixes the done screen on a phone. The manager and Growth offers were **off** on 12 Nov; their state today is unknown. #75 (Jordan's two rulings, docs) is open.
- **The TY Growth Engine** (UR-26) is in its own repo with nothing deployed (hand-off card, 12 Nov). Connecting it is UR-17, UR-19 and UR-29.

## Switches

The Big Bold Beautiful build (29–30 Oct) **removed most switches, budgets, call caps and time limits**. The Studio fix and Builds 6 and 7 add none back, on purpose (Jordan's rule: "no brakes at the starting line"). The safety rules stay: sign-in, ownership, suspension, age, the sandbox and content safety. What is left at `327d4a47`:

| Switch | Kind | What it holds back |
|---|---|---|
| The stop button (`creative_mode`) | Database switch, set in a guarded transaction when Jordan says | Every card build, show press and studio chat. State today: unknown |
| Cards open on uncard.gifts (`cards_on_gifts`) | Owner-only database switch | Moving card links to uncard.gifts. Cards open on uncard.app today (the Roadmap, 22 Nov) |
| Offers manager on/off, Growth offers on/off | Owner-only database settings | Offer-driven prices on the public pages; Growth's offer tests. Off on 12 Nov |
| Which writer pack the Studio uses | App setting, after Jordan approves a pack | `studio-5.1` or `studio-5.2` instead of `studio-5.0` |
| Final terms approved; the contact address | Code constants | Final Terms and Privacy; the "Report this uncard" link. At `327d4a47` the terms are not approved and the address is still `[contact email]` |
| Consent and recipient measurement; the gallery and share pictures; test-mode checkout; asking for a birthday on the account page | App and Worker settings from the Phase 3 stages | Those parts of the site |
| Two build flags committed in `.env` | Build settings | Photo intake and the agent access screen |

Which settings are set live is **unknown**. Their names are in the product repo (`docs/phase-3/completion/FLAGS.md`, last changed 20 Oct, before the removals).

## How a change reaches the live site

From `docs/README.md`, `cron/README.md`, `gifts/README.md` and the Build 6 and 7 specs (20–22 Nov):

1. **Code:** a builder works on a branch. It lands on `main` by pull request, or a build lands slice by slice with merge commits, each one publishable. A build guard fails if a build touches a protected path (the Workers, the packs, the player, the dependencies). Never rewrite pushed history.
2. **SQL:** staged in `db/pending/` with its checks; Jordan's Claude applies it on Jordan's yes (see "The data layer").
3. **Publish:** Jordan presses Publish in Lovable.
4. **Workers:** `uncard-cron` redeploys whenever `main` moves, so a Worker change is live the moment it is on `main`, and it must work with the app already published (the Worker calls the published site for every step). A redeploy can cut a reply or a build in the air. Prove a Worker change first with the `worker-pairing` check (Build 6). `uncard-gifts` deploys only when `workers-live` moves. There is no photo converter Worker.
5. **Paid tests:** nothing starts or retries a build on a timer (`cron/README.md`). The page's own check for a finished card only reads.

**What waits on whom** (as recorded on 21–22 Nov). The decisions belong to the partners:

- **Jordan:** publish `327d4a47`; the look's phone pass (`docs/look/PHONES.md`) and the Studio fix's two-phone live run; approve a writer pack; Build 7's open questions; the legal terms' hosting line.
- **Tim:** the words and rulings in his area (Build 7's K2, K4, K6, W11, W12); the look's sheet beside the reference boards.
- **Brian:** the red labels Build 7's hand-back names as his. His open pull requests #74 to #89 wait for review and merging.
- **Partners and counsel:** the contact address, the legal entity and the open legal terms.

## The agent doors (Stage 10)

- **What:** ChatGPT, Claude or a script connects to Uncard and works on its owner's uncards. REST at `/api/v1`, MCP at `/mcp`, a guide at `/agents`. Sign-in is OAuth. The owner approves on Uncard's own Connect page and revokes on `/account/agents`. Never allowed (27 Oct plan): paying, publishing, or changing who can see a card.
- **State:** the database part has been live since 27 Oct (0092 to 0104). Since 19 Nov the Connect page says plainly which app wants to connect and what each app may do (#31), sign-in requests nobody approved are tidied away (0169, live), and signing in from `/account/agents` returns there (Build 6). The door's tools that start a build use the same one-call build as Make, so the stop button covers them. Shows are read-only through the door (Phase 3b). Whether an outside app has connected yet: **unknown**.

## How the build is checked

- **Exact-source runs, not GitHub Actions** (stopped 9 Oct). `tools/ci/gates.sh` runs the checks on one exact commit. The `static` profile is now **24 steps** (Builds 6 and 7 each added a guard). It passed 24 of 24 on `main` with #68 to #71 before the 22 Nov merges.
- **The database checks are green again where they test today's schema.** The SQL tests and integration checks pass on `main` since #20 and #21 (19 Nov). At Build 7's end, on both the as-live and as-next databases: `integration`, `sql-tests`, `live-line`, `age-rule`, `recipient` and `recipient-races` pass. Still red: `proposed-creative` 1 to 4 (checks of a proposal written before 0113; draft #88 works on them) and one race label.
- **Browser suites:** at Build 7's end, 47 of 67 suites passed whole and 20 were red or stopped, each red named with its cause and whose it is (`docs/build-7/HANDBACK.md`, "Red labels"). No label went from green to red. A recipient's uncard and `/play` were the same pictures, byte for byte, before and after Builds 6 and 7.
- **Engines and phones:** the look's checks are written for Chromium, WebKit and Firefox, but the build's sandbox could install only Chromium (`docs/look/HANDBACK.md`). Real-phone checks are Jordan's; none is recorded on `main`.

## In progress now (not on `main`)

Checked on 23 Nov with `gh pr list` and `git merge-base --is-ancestor`. 45 remote branches are not on `main`. Merged since the last snapshot: pull requests #5 to #39 except #11, #45, #57, #61, #62 and #64 to #73, and `devin/1793889643-show-phase3b` (through #34). The work of #46 to #56, #58 to #60 and #63 came in through the integration base and the look's merges; those pull requests were closed.

| What | Last commit | State | What it is |
|---|---|---|---|
| Pull requests #74, #77, #79 to #84 | 22 Nov | Open | Brian's Claude: checks brought up to today's screens (delivery, the recipient's keep page, the privacy panel, Google, the agent journey, the conversation race, the journal project, the Worker-page suites) |
| #75, #78, #85, #86 | 22–23 Nov | Open | Brian's Claude: Jordan's two Promotions Manager rulings (docs); a sign-in fix; the privacy notice on both hosts; the site player starts a returning visitor at moment 1 |
| #76, #87, #89 | 22–23 Nov | Open | Brian's Claude: three more changes, described in the product repo. #89 adds SQL 0176, which waits for an apply |
| #88 (`proposed-green`) | 23 Nov | Draft | The `proposed-creative` database checks on today's database |
| #1 | Oct | Open | Brian's: AGENTS.md points agents to this wiki |
| `codex/quality-engine` | 28 Oct | 16 ahead | A judge for finished cards and a staff dashboard. Whether it will be merged: unknown |
| `sf/x-probe`, five `studio-*` branches, `better-cards-tap-questions` | 14–18 Nov | Not merged | A Studio fix probe, the earlier fixes #40 to #44 and the first part 4b (#11), all closed or replaced |
| `integration-base`, `lovable-sync` | 19 Nov, 31 Oct | 3 ahead each | Leftovers: the work in their last commits reached `main` another way (#62 and #64; `docs/README.md` for `lovable-sync`) |
| `codex/*`, `devin/*`, `sonnet/*` and other older branches (19) | 1–24 Oct | 1–6 ahead each | Older leftovers. Deleting them waits on the partners |

## Where builders work

From commit authors, co-author lines and branch names. Since 11 Nov: 548 of 577 commits are authored "Claude".

| Branch prefix | Builder | How you can tell |
|---|---|---|
| `look/*`, `build-6`, `build-7`, `sf/*` | **Claude Code cloud sessions for Jordan** (Opus 5.5), from specs by Claude Fable 5.2 | Author "Claude", a "Claude Opus 5.5" co-author line and a session link (344 commits since 11 Nov carry one) |
| Pull request branches with no prefix | **Brian's Claude Code** (Opus 5.5) | Author "Claude" with a "Claude Opus 5.5" line and no session link; opens pull requests. On 18 Nov it built and merged the integration base |
| Merges of 22 Nov | **Jordan's Claude** (Fable 5.2) | Author `JNabsRepo`, "Merged on Jordan's instruction" |
| `codex/*`, the UR-37 review, `pm/*` | **Jordan's Codex** | Author "JordanLMC" or "Jordan Nabigon", no tool line (12 review commits on 20 Nov) |
| `devin/*` | **Devin** | "Devin AI" co-author line; no new commits since 7 Nov (Phase 3b came in through #34) |
| `sonnet/*`, `studio/*`, `claude/*` | Jordan's Claude Code cloud sessions (Sonnet 5.5) and Claude Code (Opus 5.5) | October and early November work |
| `lovable-sync`, direct commits | **Lovable's agent** | Author `gpt-engineer-app[bot]`; none since 11 Nov |

**How it lands:** Brian's Claude opens pull requests; the integration base took them all in on 18–19 Nov. Builds 6 and 7 land slice by slice on `main` with merge commits. Since 22 Nov Jordan's Claude merges reviewed pull requests on his instruction.

## Known open items

- **The publish:** `327d4a47` (the 22 Nov merges) waits for Jordan's Publish (the Roadmap, 22 Nov). The cron Worker redeployed from `main` on 22 Nov, so for now it runs newer code than the published app.
- **The nightly job:** the last 7 nights ended "partial"; the cause has not been read (the Roadmap, 22 Nov).
- **uncard.gifts:** its Worker runs 2 Oct code and its deploy branch is far behind `main`. Cards open on uncard.app.
- **Photos:** no photo converter Worker exists, so HEIC conversion for browsers that can't open HEIC is not live.
- **One stopped job:** after 0175, a card job of 9 Nov still reads "running" by the file's own rule, and an operation of 28 Oct too. Whether opening that uncard settles it has not been seen live (`docs/build-7/APPLY.md`).
- **Placeholders:** the contact address is still `[contact email]` at `327d4a47`, so no "Report this uncard" link shows. The legal terms still open with "three months of hosting", which is not what a free-launch link does (Build 7 left them for Jordan). The legal entity is still open.
- **Phones:** the look's phone pass, the Studio fix's two-phone live run and Build 7's "one thing to try first on a phone" are Jordan's. None is recorded on `main`.
- **Writer packs:** `studio-5.1` and `studio-5.2` wait for Jordan's approval and a format check through the real gateway.
- **The Stage 3 contraction:** no record says it ran. Its checks now run on their own (`proposed-creative`).
- **Missing server values:** a 30 Oct check found two values unset in Lovable (names in the private repo). Not re-checked.

## Open questions

- Is the stop button open or closed today, and which writer pack is on?
- Is the Promotions Manager on, and are Growth offers?
- Why did the last 7 nights end "partial"?
- Should `uncard-cron` deploy only after a publish? `cron/README.md` has the Cloudflare steps; nothing records a decision. When does `workers-live` move for the gifts Worker, and when does the "Cards open on uncard.gifts" switch go on?
- Which app settings in the Switches table are set in Lovable today?
- Has an outside app connected through the agent door?
- Build 7's questions for Jordan and Tim: may a giver tap an age range after a birthday gave one; should an age said in the chat follow the younger-wins rule; should there be a ceiling on moments when people contribute; should Home and Pricing still say a recipient's own subscription can keep a link open?
- Will `codex/quality-engine` be merged, parked or dropped? Which proposals and old branches get deleted?

## Sources

All at `327d4a47` unless noted. Links go to `main`, which may have moved since.

- [`docs/README.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/README.md), [`db/applied.txt`](https://github.com/JNabsRepo/uncard-starter/blob/main/db/applied.txt), [`db/README.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/db/README.md) (top paragraphs)
- [`docs/build-7/`](https://github.com/JNabsRepo/uncard-starter/tree/main/docs/build-7) (`SPEC.md`, `HANDBACK.md`, `APPLY.md`), [`docs/build-6/`](https://github.com/JNabsRepo/uncard-starter/tree/main/docs/build-6) (`SPEC.md`, `HANDBACK.md`, `APPLY.md`), [`docs/studio/AGE-RULE.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/studio/AGE-RULE.md)
- [`docs/look/`](https://github.com/JNabsRepo/uncard-starter/tree/main/docs/look) (`SPEC.md`, `HANDBACK.md`, `PHONES.md`), [`docs/studio-fix/`](https://github.com/JNabsRepo/uncard-starter/tree/main/docs/studio-fix) (`HANDBACK.md`, `PACK.md`, `LIVE-RUN.md`), [`docs/review-2026-11-20/`](https://github.com/JNabsRepo/uncard-starter/tree/main/docs/review-2026-11-20)
- [`cron/README.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/cron/README.md), [`gifts/README.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/gifts/README.md), [`photo-convert/README.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/photo-convert/README.md), [`tools/ci/README.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/tools/ci/README.md)
- Merge messages of `9617c974` to `327d4a47` (18–22 Nov); pull requests #5 to #89 (`gh pr list`, 23 Nov)
- History: [`docs/show-builder/`](https://github.com/JNabsRepo/uncard-starter/tree/main/docs/show-builder), [`docs/offers/`](https://github.com/JNabsRepo/uncard-starter/tree/main/docs/offers), [`docs/big-bold-beautiful/REPORT.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/big-bold-beautiful/REPORT.md), [`docs/phase-3/completion/`](https://github.com/JNabsRepo/uncard-starter/tree/main/docs/phase-3/completion)
