# How Uncard Fits Together (Architecture)

**Status:** Draft. This is a snapshot, and the product repo is the source of truth.
**Updated:** 2026-11-06
**Owner:** Brian Lapp
**Method:** Read from the product repo [`JNabsRepo/uncard-starter`](https://github.com/JNabsRepo/uncard-starter) at `origin/main` = **`6e0997d6`** (2026-11-03, the last show builder Phase 3 report), 543 commits after the last snapshot (`84977d9`, 19 Oct). Also read: the unmerged branch `devin/1793889643-show-phase3b` at `d7f78885` (5 Nov). Sources: `docs/show-builder/` (the spec, the Phase 1 to 3 reports, the kit report, `KIT.md`), the Phase 3b report on its branch, `docs/studio/` (to 27 Oct), `docs/big-bold-beautiful/` (to 1 Nov), the READMEs for `db/`, `cron/`, `gifts/`, `photo-convert/` and `tools/ci/`, `src/uncard/generator/routes.ts`, and commit messages. Counts come from `git ls-tree`. Branch state comes from `git merge-base --is-ancestor`. Who built what comes from commit authors and co-author lines. Nothing was checked in a browser or against the live database. "Live" facts are what the builders recorded. The newest is a read-only live database check on **3 Nov** (show builder spec). Anything newer is marked unknown.

## TL;DR

- **Since 19 Oct the work went from "built and switched off" to "trying it for real".** Making opened in a practice window on 25 Oct (by 27 Oct it held Jordan, Brian and Tim). Then the way a card is made was rebuilt three times. Most on/off switches, budgets and time limits were removed (29–30 Oct). In `main`'s code since 2 Nov, **one model call writes a whole card**.
- **New: the show builder (3 Nov).** A card made as a playable "show", one section at a time. Plan, then one build, then a free test drive, then fix only what you press. Phases 1 to 3 are on `main`, as **staff-only Lab buttons**. The sender's version (Phase 4) is not authorized yet.
- **What is live:** uncard.app on Lovable. The last publish named in the repo is commit **`4487dbce`** (1 Nov). The database has **161 migration files** (0000 to 0160, the last added 1 Nov), plus three show files Claude applied on 3 Nov. Card making has one stop button. It read **closed** on 3 Nov, and Claude opens it only around Jordan's tests.
- **What waits:** Claude applies four staged show files (0142 to 0145). Jordan publishes, runs the paid feasibility test and checks a real iPhone and Android. As recorded on 5 Nov, **`main` is frozen at `6e0997d6`** until Jordan says that test is finished. Phase 3b waits on its branch.

## What changed since 19 Oct

| When | What landed on `main` | Builder |
|---|---|---|
| 20–24 Oct | **M13**: honest public pages, sample uncards, an invite-only test window (pull request #3, merged 24 Oct). Security pins and in-browser photo clean-up | Codex |
| 25–27 Oct | **Studio practice**: a two-pane studio, photos, the age line at 13, practice windows (Tim joined on 27 Oct). The **agent door's database part** was applied on 27 Oct | Claude (Sonnet 5.5) |
| 28 Oct | **Delight**: a new card pack, a theme engine, sound, 21 new kinds of moment, sandboxed "hero" moments | Claude (Sonnet 5.5) |
| 29–30 Oct | **Big Bold Beautiful**: the shared Uncard Viewer, 20 themes, picture, music and narration paths, free-launch giving. It removed most switches, budgets and time limits | Codex |
| 30 Oct–1 Nov | Its SQL applied in parts (migrations 0112 to 0154). The practice-window tables were dropped. Then 0155 to 0160, for the cron Worker owning each model call | Claude (Fable 5.1, Sonnet 5.5) and Lovable |
| 1 Nov | The Worker's minute timer was switched off after an unattended build made 13 unreadable calls in a row | Claude (Sonnet 5.5) |
| 2 Nov | **One call per card.** The old 27-role pipeline is frozen. Code mends small slips instead of paying to ask again. The cron Worker now deploys from `main` | Claude (Sonnet 5.5, Opus 5.5) |
| 3 Nov | **Show builder** Phases 1 to 3, and the show kit | Devin, Claude (Sonnet 5.5) |

## The moving parts

| Part | What it is | State (as of the sources) |
|---|---|---|
| **uncard.app** | The website, the studio, the account and admin pages, and every server route. TanStack Start (React, Vite, TypeScript), built and hosted by **Lovable**. Commits sync both ways with GitHub `main`. | Last publish named in a commit: **`4487dbce`** (1 Nov). Whether `6e0997d6` is published: **unknown**. |
| **Database** | **Lovable Cloud = Supabase Postgres.** Applied migrations are files in `drizzle/migrations/`. | 161 files (0000 to 0160), the last added 1 Nov. Also live: 0137, 0139, 0140 (applied 3 Nov through Lovable's database API, so no migration file) and 0141 (records nine definitions that were already live). Staged: 0142 to 0145. |
| **Card-call Worker and nightly job** | Cloudflare Worker **`uncard-cron`** (`cron/`). Two jobs. (1) It **owns each card's model call**: the app wakes it once, a Durable Object (one per call) streams the answer from the AI gateway, keeps it, and hands it back until the app says "saved". (2) Every night at 07:17 UTC it copies data to a private R2 bucket, **`uncard-lake`**, and rolls up the metrics. | Deployed: a 1 Nov commit (`4487dbce`) names "the cron deploy". Since 2 Nov, Cloudflare's own Builds deploys it whenever `main` moves. No minute timer. Whether the bucket exists: unknown. |
| **uncard.gifts** | Cloudflare Worker **`uncard-gifts`** (`gifts/`). The card page and the PIN form. It also serves the show frame and the hero frame. It has **no database key**. It asks uncard.app through a private API (`/api/gifts/v1/*`) with a shared secret. | Live state **unknown**. How it deploys is disputed: `gifts/README.md` (14 Oct) says from the `workers-live` branch (last moved 1 Nov, to `ada61906`), while the 3 Nov spec says it deploys itself from `main`. Links stay on `uncard.app/c/<id>` until the owner switch `cards_on_gifts` is on. Whether it is on: unknown. |
| **Photo converter** | Cloudflare Worker **`uncard-photo-convert`** (`photo-convert/`, new 25 Oct). Turns iPhone HEIC photos into JPEG for browsers that can't open them. It stores nothing. | Not deployed on 27 Oct. Its address is not in the committed `.env` at `6e0997d6`, so the app does not use it yet. |
| **AI** | The **Lovable AI gateway**, through three "doors" (Responses, Chat Completions, Messages). No provider keys. A **route table** (`src/uncard/generator/routes.ts`) picks the model for each job: studio chat and review on Gemini 3.8 Flash, show plan, build and fix on Claude Opus 5.5. The one-call card uses `openai/gpt-6-astra`. | Real calls have been made since 26 Oct. The stop button (`creative_settings.creative_mode`) read closed on 3 Nov. The model bake-off (Phase 5) has not started. |
| **Payments** | Stripe, test mode only (Stage 5 code). | Giving uses a free-launch path: "Free while we launch." On 30 Oct the live database had no billing tables. Real money is a later gate. |
| **DNS** | Both domains are on Cloudflare. | See `live-product.md`. |

## The diagram

```
 WHO               LANDS ON                                    TALKS TO
 ───────────────   ─────────────────────────────────────────   ───────────────────────────────────
 Sender         ─► uncard.app (Lovable hosting)               ─► Lovable Cloud Postgres (Supabase)
                   pages, /make studio, /account, /admin,        row-level security on every table;
                   /api/*  (server code holds the keys)          writes only through server code
                   studio chat (short, in the request)        ─► Lovable AI gateway
                   Make, or a show press ─► wakes Worker      ─► Lovable AI gateway (one call per
                                          "uncard-cron"            step; the Worker keeps the answer
                                          (one object per call)    and hands it back to uncard.app)
                   HEIC photo ─► Worker "uncard-photo-convert" (not deployed yet)

 Recipient      ─► uncard.gifts (Worker "uncard-gifts")       ─► uncard.app /api/gifts/v1/*
                   card page, PIN form; shows and hero           (shared secret; the Worker has
                   moments play in sandboxed frames              no database key)
                   (until then: uncard.app/c/<id>)

 Outside AI app ─► uncard.app /oauth, /api/v1, /mcp           ─► the same server code and database
                   owner approves it on /account/agents

 Nightly job    ─► Worker "uncard-cron", 07:17 UTC            ─► uncard.app /api/cron/*  ─►  R2 "uncard-lake"
```

## How a card gets made and given (on `main` today)

1. **A sender opens uncard.app.** The home page box opens the studio at `/make`.
2. **The gate.** The stop button refuses chat and builds while it is closed (it was on 3 Nov). The age line is **13**: teenagers make for themselves, and under-13s need a parent's account (25 Oct). Suspended and unconfirmed accounts can't make.
3. **Chat.** Two panes: the chat beside the uncard (on a phone, two tabs). The partner asks about their person. Facts, exact lines and photos (with optional captions) are saved. In `main`'s code since 3 Nov, the chat runs on Gemini 3.8 Flash.
4. **One call writes the card** (since 2 Nov). Make sends one request through the cron Worker. The studio says "Being written… usually 10–25 minutes". Code fixes small slips and saves it. Nothing runs on a timer: opening the studio, coming back to it, or "Check now" settles the result.
5. **Shape it.** A strip of moments; edit words, lock, move, remove; undo, redo and history; full-screen play in the shared Uncard Viewer.
6. **Ready and give.** A review card, then approve. Giving uses the free-launch path: a private link, with an optional PIN.
7. **The recipient opens the link** (today `uncard.app/c/<id>`). The v2 player plays it: 48 kinds of moment (28 Oct count), 20 themes and sandboxed hero moments.

## The show builder (new, 3 Nov)

- **What it is.** A card made as a **show**: the recipient plays one section at a time, and each section is built from a real story. The quality bar is a hand-built card, Booter, rebuilt on the shared kit.
- **How it's made** (spec §0). **Plan** (one strong-model call writes the storyboard; a cheaper model reads it back for problems). The sender adjusts the plan for free. **Build** (one call writes every section's code on the kit). A **free test drive** plays every section in the sender's browser. **Fix this section** runs only when pressed. Every press saves a new version. Nothing runs on a timer, and a paid answer is never thrown away.
- **How it fits.** No new tables or columns. A show is a version of an uncard (`spec.show`). Sections run in a sandboxed frame (`/show-frame`) on both uncard.app and uncard.gifts, from one kit (`src/uncard/show/kit/`). Paid steps go through the cron Worker, like the one-call card. Old Make and the older card packs are unchanged.

| Phase | What | State (as recorded) |
|---|---|---|
| 1 | Model doors, the cheaper chat, prices, never losing an answer | On `main`. SQL 0137, 0139, 0140 applied by Claude on 3 Nov |
| 2 | The kit plugged in, Booter hosted, the free test drive, "Save a show to an uncard" (staff Lab) | On `main`. 0142 staged. The kit came from a Claude session (`sonnet/show-kit`, merged 3 Nov) |
| 3 | The engine: staff Lab buttons for Plan, Build, Continue, Fix, Change, Review and Apply; three test briefs; free line edits and Undo | On `main` (code `dff9921d`). 0143 to 0145 staged |
| 3b | Sound on phones, an always-visible close button, shows read-only in the classic studio and the agent door | **Branch only** (5 Nov). 0146 staged on it |
| 4 | The sender's board and pack `studio-5.1` | **Not authorized.** Needs Jordan's go and his approval of the board reference page |
| 5 | A one-time model bake-off, then rollout | Not started. The new Make becomes everyone's default only after three different cards pass Jordan's acceptance |

**Live vs staged:** nothing a sender sees is live. The staff Lab tools are in `main`'s code; whether they are in the published build is unknown. **Next steps, by the Phase 3 report:** Claude applies 0142 to 0145. Jordan publishes, runs the feasibility test in Admin → Lab → Show engine (Claude opens and closes the stop button around it, then writes the feasibility report), and checks playback on a real iPhone and Android. After that, Phase 3b can land and Claude applies 0146.

## Where things live in the code

| Path | What it holds |
|---|---|
| `src/routes/` | One file per page or API route. Includes `/make`, `/account`, `/admin*`, `/c/$cardId`, `/add/$token`, `/discover/$slug`, `/agents`, `/mcp`, `/oauth.*`, `/api/v1/*`, `/api/gifts/v1/*`, `/api/cron/*`, and the sandboxed frames `/show-frame` and `/hero-frame` |
| `src/uncard/show/` | The show builder: the frozen contract, the kit, the player and test drive, the press engine, plan and code checks, test briefs |
| `src/uncard/generator/routes.ts`, `generator/doors/` | The route table (which model does which job) and the three gateway doors |
| `src/uncard/creative/` | The v2 engine; the one-call author (`author*.ts`); the Worker-stream finish; the frozen 27-role pipeline |
| `src/uncard/site/studio/`, `site/make/` | The two-pane studio |
| `src/uncard/player/`, `player-v2/`, `themes/`, `hero/`, `audio/` | The card players, the 20 themes, hero moments and sound |
| `src/uncard/delivery/`, `measure/`, `billing/`, `contributors/`, `memory/`, `agents/` | Links and the gifts contract; measurement; checkout (test mode); Stages 8, 9 and 10 |
| `cron/`, `gifts/`, `photo-convert/` | The three Cloudflare Workers, each with its own packages and deploy |
| `drizzle/migrations/` | The 161 applied migration files (0000 to 0160) |
| `db/pending/`, `db/proposals/`, `db/tests/` | 12 staged files (see below), 152 proposal files, 104 SQL test files |
| `tools/ci/`, `tools/db/`, `tools/qa/` | The check runner, the database checks, the browser suites |
| `docs/show-builder/`, `docs/studio/`, `docs/big-bold-beautiful/`, `docs/viewer/`, `docs/delight/` | One folder per build since 21 Oct: spec, reports, owner steps |
| `docs/phase-3/` | The Phase 3 spec, stage reports and `completion/` (last changed 24 Oct) |

## The data layer

- **Main table groups:** as before. Accounts and roles; the studio and cards (`card_roots`, `card_versions`, `conversations`, `facts`, `people`); generation and spend (`generation_*`, `creative_*`, `model_prices`, `prompt_packs`); measurement and the lake; evaluation; and settings, now including `creative_settings` (the stop button). The show builder adds no tables or columns. Current packs: card pack `uncard-4.1` (31 Oct), studio pack `studio-5.0` (3 Nov spec).
- **The security pattern** (`db/README.md`) still holds. Row-level security is on every table. The browser never writes account, job or card tables. It can call only a short allow-list of database functions, checked on every migration. Roles live only in `user_roles`, with exactly one owner. A new table holding personal data joins the account-erase path.
- **What sits in `db/pending/`** (12 files, at `6e0997d6`): four data files already applied and kept by design; four show files already live and kept for local replay (**never apply again**); and four to apply (0142 to 0145).
- **How SQL reaches the live database** (since 3 Nov, `db/README.md`): the SQL and its checks are written locally. **Claude applies each file through Lovable's free database API, as one guarded transaction that commits only if its checks pass.** SQL is never pasted into Lovable chat, and Devin never writes to the live database. Until 1 Nov, Lovable's agent applied each file as a migration, one per message, after a rolled-back rehearsal.

## Switches

The Big Bold Beautiful build (29–30 Oct) **removed most switches, budgets, call caps and time limits**. Its report says the safety rules stay: sign-in, ownership, suspension, age, the sandbox and content safety. The contributor, memory and agent switches are gone from production code. What is left at `6e0997d6`:

| Switch | Kind | What it holds back |
|---|---|---|
| `creative_settings.creative_mode` | Database stop button. Claude sets it in a guarded transaction when Jordan says | Every card build, show press and studio chat. **Closed** on 3 Nov |
| `cards_on_gifts` | Owner-only database switch | Moving card links to uncard.gifts |
| `LEGAL_APPROVED`, `CONTACT_EMAIL` | Code constants | Final Terms and Privacy; the "Report this uncard" link. `CONTACT_EMAIL` is still `[contact email]` |
| `APP_CONSENT_LIVE_READY`, `RECIPIENT_MEASUREMENT_READY`, `AD_SOURCE_LIVE_READY` | App settings | Stage 4 consent and measurement |
| `UNCARD_GALLERY_READY`, `UNCARD_GALLERY_DRAFTS_READY`, Worker `GALLERY_READY`, `SHARE_TILES_READY` | App and Worker settings | The gallery and share tiles |
| `UNCARD_TEST_CHECKOUT_READY`, `UNCARD_TEST_BILLING_INBOX_READY` | App and Worker settings | Stripe test mode |
| `UNCARD_ACCOUNT_COMPLETION_READY` | App setting | Asking for a birthday on the account page instead of the adult tick |
| `VITE_*` build flags | Committed in `.env` | Two are set there: photo intake and the agent access screen |

Which app settings are set live is **unknown**. `FLAGS.md` was last changed on 20 Oct, before the removals.

## How a change reaches the live site

This replaces the R1/R2/R3 runbook (`ACTIVATION.md`, last changed 20 Oct). Rules from the show builder spec (rule 8) and the READMEs, as of 2 to 3 Nov:

1. **Code:** a builder pushes a branch. When a phase is green, `main` is fast-forwarded. Never rewrite pushed history.
2. **SQL:** staged in `db/pending/` with its checks. Claude applies it (see "The data layer").
3. **Publish:** Jordan presses Publish in Lovable.
4. **Workers:** `uncard-cron` deploys itself when `main` moves, so a Worker change must work with the app version already published. For `uncard-gifts` and `uncard-photo-convert`, see the open question below.
5. **Paid tests:** Claude opens the stop button for Jordan's test and closes it when every receipt says done. Nothing else spends: since 2 Nov no timer starts or retries a build (`cron/README.md`).

**What waits on whom** (as recorded on 3 to 5 Nov). The decisions belong to the partners. The reports assign the actions like this:

- **Claude:** apply 0142 to 0145, and later 0146. Open and close the stop button. Write the feasibility report.
- **Jordan:** publish; run the paid feasibility test; check sound and fit on a real iPhone and Android; say when the test is finished (`main` stays frozen until then); approve the board reference page before Phase 4. These are his because he holds the owner login and the Lovable and Cloudflare accounts.
- **Devin:** Phase 3b on its branch, and Phase 4 only once it is authorized.
- **Partners and counsel:** the contact address, the legal entity and the open legal terms (all still placeholders on 30 Oct).

## The agent doors (Stage 10)

- **What:** ChatGPT, Claude or a script connects to Uncard and works on its owner's uncards. REST at `/api/v1`, MCP at `/mcp`, a guide at `/agents`. Sign-in is OAuth. The owner approves on Uncard's own Connect page and revokes on `/account/agents`. Never allowed (27 Oct plan): paying, publishing, or changing who can see a card.
- **State:** the database part was applied on **27 Oct** after Jordan's named yes (migrations 0092 to 0104). 0104 lets an account (staff included) work on its own uncards, and lets an app on the owner's own computer sign in (for Claude Code in a terminal). The agent switches that kept the door off were removed from production code on 29 Oct (commit `abe90225`). The door's `propose_ideas` and `generate_uncard` start the same one-call build as Make, so the stop button covers them too.
- **Shows:** read-only through the door (Phase 3b, branch only). Whether ChatGPT or Claude has connected yet: **unknown**.

## How the build is checked

- **Exact-source runs, not GitHub Actions** (stopped 9 Oct). `tools/ci/gates.sh` runs the checks on one exact commit. The `static` profile is now **22 steps**: types, lint, formatting, the app and Worker builds, the offline checks, and the docs and inventory checks. Phase 3 passed 22 of 22 on `dff9921d` (3 Nov).
- **Each show phase** also ran its focused SQL checks (for example, 0137 at 50 of 50), the show kit suite (72 of 72, three phone sizes), and a fake gateway, so building spent nothing. Then one independent review and one targeted recheck. The Phase 2 and 3 reviews each found a blocker, fixed before the phase closed; Phase 1's found none.
- **The full database suite is not green.** On 3 Nov it reported 145 pass, 45 fail and 10 error result groups. The report puts all of these in older tests, unchanged by the show work. The studio's full database run passed on 26 Oct (on `15258d3`). By 30 Oct the local SQL check already failed in older test files (SQL apply log).

## In progress now (branches not on `main`)

Checked on 6 Nov with `git merge-base --is-ancestor <branch> origin/main`. "Ahead" means commits not on `main`. Merged since the last snapshot: `codex/m13`, `codex/big-bold-beautiful`, `studio/*`, `sonnet/runs-to-the-end`, `sonnet/one-call-cards`, `claude/no-refusals`, `sonnet/show-kit`, `devin/show-builder` and `devin/1793740200-show-phase3`.

| Branch | Last commit | Ahead | Merged? | What it is |
|---|---|---|---|---|
| `devin/1793889643-show-phase3b` | 5 Nov | 4 | **No** | Show builder Phase 3b. Waits for Jordan to finish the feasibility test |
| `codex/quality-engine` | 28 Oct | 16 | **No** | A "Quality Engine": a judge for finished cards, a staff dashboard, references. Whether it will be merged: unknown |
| `lovable-sync` | 31 Oct | 3 | **No** | Lovable's commits applying 0126 parts 1–2; `main` records 0126 another way |
| `codex/*` security, Windows harness and codec (6 branches) | 24 Oct | 1–4 each | **No** | Side branches. `main` took the reviewed security and photo work on 24 Oct |
| `sonnet/m11-agents` | 19 Oct | 1 | **No** | One test repair (`lab-flow`), still not on `main` |
| `devin/*` Stage 4–6 branches (7) | 10–11 Oct | 1–6 each | **No** | Early Phase 3 work, older than the completion run |
| `sonnet/m2-photos`, two `codex/*` handoff branches, `docs/oy-conversation-design`, `brian/wiki-context-note` | 1–16 Oct | 1 each | **No** | Older leftovers |

## Where builders work

From commit authors, co-author lines and branch names (19 Oct to 5 Nov). All of them land on `main`.

| Branch prefix | Builder | How you can tell |
|---|---|---|
| `devin/*` | **Devin** | Author "Jordan Nabigon" with a "Devin AI" co-author line (25 commits on `main`, 4 more on Phase 3b) |
| `sonnet/*`, `studio/*` | **Jordan's Claude Code cloud sessions** (Sonnet 5.5) | Author "Claude", a "Claude Sonnet 5.5" co-author line and a Claude Code session link (174 commits on `main`). Jordan, 27 Oct: "I build Uncard in Claude." |
| `claude/*` | **Claude Code** (Opus 5.5) | `claude/no-refusals` (2 Nov). Sessions on Fable 5.1 also committed the 30–31 Oct SQL records straight to `main` |
| `codex/*` | **Jordan's Codex** | Author "JordanLMC" or "Jordan Nabigon", with no tool line. The M13 and Big Bold Beautiful reports name Codex |
| `lovable-sync`, and direct commits | **Lovable's agent** | Author `gpt-engineer-app[bot]` (217 commits on `main`: applied SQL and editor changes) |

**How it lands:** Devin fast-forwards `main` when a phase is green. Codex's M13 came in by pull request #3. Claude's branches are merged in. Lovable writes straight to `main`. As of 5 Nov, `main` is frozen until Jordan says the feasibility test is finished.

## Known open items

- **The feasibility test and staged SQL:** the 5 Nov branch report says the test is running. Whether 0142 to 0145 were applied after 3 Nov, and the stop button's state today: unknown.
- **Phones:** the iPhone and Android checks for Phases 2 to 3b are Jordan's. None are recorded yet.
- **Placeholders:** `CONTACT_EMAIL` is still `[contact email]` at `6e0997d6`, so no "Report this uncard" link shows. The legal entity and terms were still open on 30 Oct.
- **Missing server values:** a 30 Oct check found the values for saved-moment picture tiles and for contributor invites unset in Lovable (names in the private repo, Big Bold Beautiful report).
- **The Stage 3 contraction:** on 27 Oct the live database did not have it. No later record says it ran.
- **Recorded limits K1 to K12** (completion report, section 6, in the private product repo). Not re-checked after 19 Oct.

## Open questions

- Which commit is published now? The last one named in the repo is `4487dbce` (1 Nov).
- Were 0142 to 0145 applied, and is the stop button open or closed today?
- Does `uncard-gifts` deploy from `main` (spec, 3 Nov) or from `workers-live` (its README, 14 Oct; the 2 Nov cron commit says gifts and photo-convert "still document workers-live")? Does it serve cards yet, and is `cards_on_gifts` on?
- Does the `uncard-lake` bucket exist, and has a nightly run been recorded?
- Which app settings in the Switches table are set in Lovable today?
- Has ChatGPT or Claude connected through the agent door?
- Will `codex/quality-engine` be merged, parked or dropped?
- Which of the Stage 4 to 10 SQL files that the 21 Oct page listed as waiting are still unapplied? Many were applied between 27 and 31 Oct; this page did not recount them.

## Sources

All at `6e0997d6` unless noted. Links go to `main`, which may have moved since.

- [`docs/show-builder/SPEC-DEVIN.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/show-builder/SPEC-DEVIN.md), [`REPORT-phase-1.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/show-builder/REPORT-phase-1.md), [`REPORT-phase-2.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/show-builder/REPORT-phase-2.md), [`REPORT-phase-3.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/show-builder/REPORT-phase-3.md), [`SONNET-REPORT.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/show-builder/SONNET-REPORT.md), [`KIT.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/show-builder/KIT.md)
- Branch `devin/1793889643-show-phase3b` at `d7f78885`: [`docs/show-builder/REPORT-phase-3b.md`](https://github.com/JNabsRepo/uncard-starter/blob/devin/1793889643-show-phase3b/docs/show-builder/REPORT-phase-3b.md)
- [`docs/studio/STUDIO-STATUS-AND-WHAT-JORDAN-DOES-NEXT.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/studio/STUDIO-STATUS-AND-WHAT-JORDAN-DOES-NEXT.md), [`docs/studio/AGENT-DOOR-PLAN-27-OCT-2026.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/studio/AGENT-DOOR-PLAN-27-OCT-2026.md), [`docs/big-bold-beautiful/REPORT.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/big-bold-beautiful/REPORT.md), [`SQL-APPLY.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/docs/big-bold-beautiful/SQL-APPLY.md)
- [`db/README.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/db/README.md), [`cron/README.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/cron/README.md), [`gifts/README.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/gifts/README.md), [`photo-convert/README.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/photo-convert/README.md), [`tools/ci/README.md`](https://github.com/JNabsRepo/uncard-starter/blob/main/tools/ci/README.md)
- [`src/uncard/generator/routes.ts`](https://github.com/JNabsRepo/uncard-starter/blob/main/src/uncard/generator/routes.ts); commit messages `ada61906` (1 Nov), `b9074b48` to `d00db516`, `197b3888` and `a8211f7a` (2 Nov)
- Earlier Phase 3 status, still useful for history: [`docs/phase-3/completion/`](https://github.com/JNabsRepo/uncard-starter/tree/main/docs/phase-3/completion) (to 24 Oct)
