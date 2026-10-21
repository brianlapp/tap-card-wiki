# The Live Product (MVP)

**Status:** Draft — snapshot of a moving target
**Updated:** 2026-10-21
**Owner:** Brian Lapp
**Method:** 2026-10-21 refresh: TL;DR, "Changed since 2026-10-02" and the superseded notes read from `origin/main` at `84977d9` (2026-10-19): the Phase 3 completion folder (`CHECKPOINT.md`, `LIVE-STATE.md`, `ACTIVATION.md`, `FLAGS.md`) and the completion report. The how is in `product/architecture.md`. The rest of the page is the original snapshot, read at commit `ffd1adc` (2026-10-02): the five phase reports in `docs/review-2026-09-30/build-reports/`, `db/README.md`, `roadmap.md`, Oy's round-2 prompt and `src/uncard/catalogue/support.ts`. Not checked in a browser here — what's "live" is what the build agent's reports say it published. **Build status changes daily — for anything current, read the product repo, not this page.**

## TL;DR

UNCARD is live at **uncard.app**. The last confirmed publish is commit **`72f02dd`** (18 Oct). Since 2 Oct the team built a new plan, **Phase 3**: a conversation studio, a new card engine, and the foundations for consent, checkout, recipients, a gallery, contributors, memory and AI-agent access. It is all on `main` as code (milestones M0 to M12, finished 19 Oct), and **almost all of it is switched off**:

- The studio is closed. No model is called and no payment is possible.
- 64 SQL files for Stages 4 to 10 are written and rehearsed, but none is applied.
- uncard.gifts does not serve cards yet, and the nightly job's Worker does not exist.

Turning things on happens in three releases (R1, R2, R3). Each needs publishes, Cloudflare steps and switches that use the owner login or Jordan's accounts, plus a named yes for each wave of SQL. R1 is published but not smoke-checked. On 20 Oct Jordan reported in Slack that Phase 3 is finished and Manus and Devin are live-testing uncard.app; which commit they are testing is not recorded. How it all fits together: `product/architecture.md`.

## Changed since 2026-10-02

The 2 Oct snapshot below described build Phases 0 to 5. Since then:

- **Phase 3 plan (approved 5 Oct).** The goal: talking is the interface, every uncard is made fresh, and the infrastructure is built properly now. New words: *sender* (was giver), *moment* (was scene), *edition* (a published version). The 20 worlds and 50 scenes became internal creative knowledge, not a menu.
- **Phase 2 (to 5 Oct) and Phase 3 Stages 0 to 3 (5 to 14 Oct).** Phase 2 wrote build spec v2 and the uncard.gifts Worker code. In Phase 3, several build agents added the rename, the command layer, measurement and the nightly lake, the v2 card engine (UncardSpec v2, 25 building blocks, renderer v2), and the conversation studio, which replaced the old interview studio. Early, switched-off pieces of Stages 4 to 10 were started too. By 15 Oct the live database had 77 migration files (0000 to 0076), up from 19 on 2 Oct.
- **M0 (15 Oct):** the completion run took over: it integrated earlier fixes, added the check runner (`tools/ci/gates.sh`) and a list of every switch (`FLAGS.md`).
- **M1:** a read-only live check found the live database matched the repo exactly, every switch that costs money closed, and no storage bucket. The older published site still worked with the newer database.
- **M2:** the studio spine, from the home box to "Ready to give", with spend records. 3 of its 5 SQL files were applied live on 16 Oct (0077 to 0079).
- **M3:** the Stage 3 clean-up (the "contraction", retiring old names and columns) rehearsed and packeted, plus the R1 release packet. Published as `72f02dd` on 18 Oct. The clean-up itself has not run.
- **M4:** evaluation accounting and the owner's evaluation page. Nothing has been run, because no evaluation package is approved.
- **M5 (Stage 4):** consent banner, recipient measurement, ad sets and visibility levels. 12 SQL files. Waits on counsel.
- **M6 (Stage 5):** checkout and billing in Stripe **test mode only**, plus Apple sign-in and passkeys, all off. 9 SQL files.
- **M7 (Stage 6):** "It's mine" claims, saved and received uncards, share controls. 3 SQL files.
- **M8 (Stage 7):** the gallery on uncard.gifts, search pages at `/discover/<slug>`, and the crawler rules. 3 SQL files.
- **M9 (Stage 8):** contributors: invites, a guest page at `/add/<token>`, a review tray, and "Include". 8 SQL files.
- **M10 (Stage 9):** sender memory: "Remember?", "What I'm using", and `/memory`. 12 SQL files.
- **M11 (Stage 10):** AI-agent access: OAuth sign-in, REST at `/api/v1`, MCP at `/mcp`, a guide at `/agents`, and revoke on `/account/agents`. 17 SQL files.
- **M12 (19 Oct):** release candidate. Six independent reviewers found no blocker (36 findings, each fixed or recorded). The full 71-step check passed on `441c701`. The run also produced a completion report and an activation runbook.
- **In progress, not on main:** branch `codex/m13` (20 Oct), with honest public pages, finished samples and an invite-only test window. Its own report says it is not finished.

Every new door above is **built and switched off**, and its SQL is **not applied**.

## Changed since the 2026-10-01 snapshot (history)

That snapshot (commit `5649437`) said the studio and giving were labelled samples and the build was at Phase 0. Superseded: Phases 1–5 shipped between 30 Sep and 2 Oct. What's new, in a sentence each:

- **Phase 1** — the site says only what's true: sample labels, "coming soon" on unfinished worlds/scenes, "usually 8 to 10 scenes", draft Terms and Privacy, Google's own sign-in button, owner-only AI switch.
- **Phase 2** — admin gets Testers and Metrics tabs; first-party measurement and per-call AI cost recording.
- **Phase 3** — the card lab at `/admin/lab`, the three test people loaded, and an avoid list that no longer bans the person's own name.
- **Phase 4** — the studio, built and published shut.
- **Phase 5** — giving, built and published; unknown gift links now answer a real 404.

## Where it lives

| What | Where |
|---|---|
| Code | [`JNabsRepo/uncard-starter`](https://github.com/JNabsRepo/uncard-starter), branch `main` |
| Editor | Lovable project `3a7b58dd-a027-4ee9-9df4-96c469e3f8ac` — commits sync both ways |
| Marketing + account site | **uncard.app** |
| Gift links | *Superseded 2026-10-07 (`decisions/0006`): uncard.gifts is the product repo's own Cloudflare Worker `uncard-gifts` (`gifts/`), not a second Lovable project. Links stay on `uncard.app/c/<id>` until it is live and the owner switch `cards_on_gifts` is on; see `product/architecture.md`.* Original 2 Oct text: served from uncard.app at `/c/:id` today. Moving to **uncard.gifts** on a second Lovable project (W-48): D16 settled by Jordan's plan (`strategy/domain-tracking-seo.md`), confirmed 2026-10-06; `decisions/0006` (a Cloudflare Worker) is superseded. Earlier note: a Cloudflare Worker, `uncard-gifts`, created 2026-10-02, no route yet) |
| DNS | Both domains on **Cloudflare** (Jordan's account). uncard.app and www point at Lovable's hosting (DNS only, not proxied). **invest.uncard.app** is a proxied placeholder record, so something on Cloudflare serves it (a Worker or Pages site, unverified). uncard.gifts has one proxied placeholder record and the route `uncard.gifts/*` → Worker `uncard-gifts`, which answers every address with a 404 "This uncard isn't here." (slice 1 of `decisions/0006`, 2026-10-02). No Worker routes on uncard.app |
| Build docs (source of truth for status) | Since Phase 3: `docs/phase-3/` in the product repo, and `docs/phase-3/completion/CHECKPOINT.md` for where things stand. Phases 0–5: `docs/review-2026-09-30/` |

## Stack (verified)

- **TanStack Start** (React, Vite, TypeScript), file-based routes in `src/routes/`
- **Tailwind + shadcn/Radix** UI
- **Supabase**: auth, Postgres with row-level security everywhere; **Drizzle** migrations, each with SQL tests
- **AI**: Lovable AI gateway. Default model `openai/gpt-6-astra`. Never called by the build yet — every AI answer in the build's checks was a stand-in
- **Bun** lockfile; `npm run dev` / `build` / `lint` / `format`

## What works today

*Partly superseded 2026-10-21. `/worlds` and `/scenes` now redirect to the home page, and worlds and scenes are internal knowledge, not a menu. `/make` is always the conversation studio, closed, and `?studio=1` is ignored. Card-making caps are now 1,000 calls a day, 30 a job and 200 a person a day (still off). Read the rest as the 2 Oct picture.*

| Area | State |
|---|---|
| Worlds ready | **2 of 20**: T02 Firmware, T03 Quest Log. The rest say "coming soon" |
| Scenes ready | **15 of 50**: S01, S04, S06, S08, S14, S15, S16, S18, S26, S33, S37, S41, S47, S48, S50 |
| Sample uncards | **Steph, 9** (Quest Log) and **Jamie, 40** (Firmware), fully playable |
| Sign in | Google (official button) or an email sign-in link. Adults only: 18+ confirmation |
| Studio | **Built, shut three ways**: a code switch, a database switch only the owner login can flip, and card-making being off. Plain `/make` still shows the Steph sample. Testers will enter at `/make?studio=1` |
| Giving | **Built and published**, but nothing can be given until the studio opens. Unknown, closed or withdrawn links all show the same "This uncard isn't here." page |
| Card lab | `/admin/lab` — make a test card and watch every model call, its tokens and cost. Unused: card-making is off |
| Admin | Tabs: People and cards, Testers, Metrics, Gifts. Panels for the card-making switch and the studio (owner only) |
| Card-making | **Off.** Limits unchanged: 60 calls a day, 30 per card |
| Payments | **Off.** None built |
| Celebrations (Phase 6) | **Not built.** The build agent ran out of room in its session; it's the next job |

Authoritative list of what's playable: `src/uncard/catalogue/support.ts` in the product repo.

## What making an uncard will feel like (built, shut)

*Superseded 2026-10-21: Phase 3 replaced this interview studio with a conversation studio (the old one is removed). See "How a card gets made and given" in `product/architecture.md`. Kept as history.*

1. **Six quick basics**: name, pronouns, what they are to you, age, tone, what to avoid.
2. **Up to ten more questions**, picked from a bank of 13 by which scenes they'd unlock — favourite foods, funny and fond stories, strengths, pets, hobbies, what they won't stop talking about. Every question can be skipped.
3. **"Make my draft"** appears at three usable facts. Under four, it asks one more first.
4. **"Here's what I've got"** — the giver confirms or fixes the details, picks a direction ("Make it", "Try another direction", tone nudges).
5. **The draft**, editable scene by scene: change the words, rewrite a scene (5 rewrites per uncard), lock, undo, approve.
6. **One optional question** after approval: "How did making this uncard go?"

Who may use it while it's shut to the public (D24 default): a live Golden Pass holder or staff, 18+ confirmed, not paused.

## What giving will feel like (built, waiting on the studio)

- An approved uncard gets a **private link**, with an optional **4–8 digit PIN**. Five wrong PIN tries lock it for 15 minutes.
- The giver can copy the link or close it again. **Staff** can withdraw a gift (with a reason), restore it, or look at it read-only — every look is audited.
- **Hosting:** three calendar months from first publish; Golden Pass gifts stay up past that.
- **Still "coming soon":** share tiles, captions and keepsake downloads. The rule that keeps the private letter off them is built and tested.

## People and access

- **Roles:** creator (everyone), admin, owner. Exactly one owner: **Jordan**.
- **Only the owner** makes admins, switches card-making or the studio on, or changes their limits. Brian and Tim are promoted by the owner login after they sign in (D4). **Contradiction:** in Slack on 30 Sep Jordan told Brian "You are now admin" (Oy granted it), but every phase report through 2 Oct still lists D4 as open. Unverified which is current.
- **Golden Pass:** granted by email, even before sign-up, singly or as a list of up to 50. Covers everything, including hosting past three months (D8).
- **Suspend and restore** exist. A suspended person sees "contact [contact email]" — the address is still a placeholder (D20), so nobody should be suspended yet.
- **Cloudflare:** since 2026-10-02 Brian is **Domain Administrator** on uncard.app and uncard.gifts (plus Workers Routes), not a member of Jordan's account (Jordan confirmed full admin on both domains in Slack, 2 Oct). So he can change DNS, settings, SSL, cache and Worker *routes*. Deploying Worker *code* is account-level: hand Jordan a ready-to-run prompt for his Codex, or ask him to do it (his preference, 2 Oct). Brian's agents use a zone-only API token (1Password: "Cloudflare API Token (uncard)"). Changing DNS touches the live site, so tell the team before you do.
- **Everything is audited:** every access, settings or gift-withdrawal change writes an `admin_audit` row in the same transaction.
- **The browser never writes** account, job, allowance or card tables. Roles are checked server-side only.

## How a card gets made (as built)

*Superseded 2026-10-21: this is the first build's generator (Phases 0–5 on this page). Phase 3 builds with the v2 engine (UncardSpec v2, renderer v2). See `product/architecture.md`.*

1. **Interview** → a brief: name, pronouns, age, relationship, signed-by, tone, things to avoid, and facts.
2. **Choose a world** filtered by age fit and what the player can draw today.
3. **One art-director call** → the look. Colours and fonts are forced from the kit, never from the model.
4. **Choose scenes** following the arc. A thin brief makes a **shorter card**, never padding (D6) — Ada, with three facts, gets six scenes, not nine.
5. **One writer call per scene.** Missing facts → skip. Avoid items can rule out whole scenes ("no timed games" drops the catch game).
6. **Avoid-list check**: short items ban their words; long ones become a topic one extra model call checks the finished card for. The person's name and facts are never banned. A scene that breaks the list is rewritten up to twice, then the card stops rather than show it.
7. **Assemble** into the player's card spec and save a draft.

**Rough cost shape (unverified until the first real run):** about 10–12 model calls a card; a typical studio session about 15, a talkative one up to 30. The daily cap of 60 holds two to four sessions.

**Guard rails, enforced in the database:** card-making switch (off by default); call caps; failed or timed-out jobs refund their attempt; a card's look must differ on 4 of 6 axes from the last 20 in its world. Every model call's cost is recorded — model prices are still empty, so costs read "Unknown" until Jordan enters them (D14).

Prompts stay server-side: the build fails if a page tries to import them.

## Measurement

First-party only. **Recipients are never tracked.** The Metrics tab adds up **22 of 27** metrics; a group of one to four people shows "Too few to show", never a number.

**Five weekly questions:**
1. Are invited testers reaching a first usable card?
2. Where is card-making failing?
3. Did the last change keep cards factual, respectful and personal?
4. Can we afford the cards people approve?
5. Are the limits holding?

**Never measured:** anything about who opens a card; third-party analytics, pixels or scripts; card or brief text, names, birthdays, emails or private messages; keystrokes, session replay or emotion scores.

**Nightly job** (daily totals, clears raw records after 13 months): built and tested, **not scheduled**. Lovable's agent can't create it; Jordan has to add it in the Lovable editor under Cloud → Jobs (D21).

## Database (13 migrations)

*Superseded 2026-10-21: the live database has **80** applied migrations (0000 to 0079, last read 16 Oct), with 2 more staged and 64 Stage 4–10 files waiting. See "The data layer" in `product/architecture.md`.*

| # | Adds |
|---|---|
| 0001 | Accounts: profiles, roles, adult confirmation |
| 0002 | Card generation: settings, allowances, jobs, calls, looks, drafts |
| 0003–0004 | Owner role, Golden Passes, admin audit |
| 0005 | The owner-only switch and caps |
| 0006 | Measurement store |
| 0007 | What each model call costs |
| 0008 | Admin tools: pass notes, admin plans, suspend/restore, exports |
| 0009 | Metrics, the nightly count, deleting one person's measurement data |
| 0010 | Generator roles and the evaluation record (card lab scoring) |
| 0011 | The studio: interview, brief, versions, scene rewrites, approvals, feedback |
| 0012 | Studio metrics |
| 0013 | Giving: publications, withdrawals, PINs, gift state |

Applied as 19 files (0011 and 0012 were split into parts Lovable's agent could apply). Every migration ships with SQL tests, most also run against the live database.

## How it's being built

*Superseded 2026-10-21: this six-phase plan was overtaken by Phase 2 (build spec v2, to 5 Oct), then Phase 3 (Stages 0 to 11) and its completion run (M0 to M12). See "Changed since 2026-10-02" above.*

A Claude build agent (Sonnet 5.5) works through **six phases** from a 52-item work list Jordan approved on 30 Sep, publishing each phase itself once its checks pass:

0. Sign-in link ✓ · 1. Honest site ✓ · 2. Measurement + admin tools ✓ · 3. Card lab ✓ · 4. Studio ✓ (shut) · 5. Giving ✓ · 6. Celebrations — **not built**

It stops for Jordan only for: AI spending, legal text, anyone's access, or anything irreversible. **Never:** payments, emails, tracking on gift pages, force-pushes.

**Next:** Oy's second test round. The prompt is written (`docs/review-2026-09-30/oy-round-2/oy-prompt.md`): Oy checks the live site against what the phase reports claim, then writes a prompt for an Opus 5.5 follow-up review. Results land in the same folder.

## Test people

Three fictional recipients, hash-locked so tests stay comparable. Loaded in the card lab as the regression set:

| | Who | Why they're there |
|---|---|---|
| **Niko**, 9 | From Aunt Vera. Paper rockets, a cardboard moon | Must work without fast reading or winning a game |
| **Mira**, 27 | From her brother Ari. Playlists, a yellow mug | Sibling in-jokes; the giver wants control of wording |
| **Ada**, 80 | From her nephew Noel. Only three details | The hard one: must not invent a life story |

A lab run is scored on seven 0–2 marks plus ten ticks. A change may go live only if it has no hard failure, meets every must-include, drops no mark by 1+ against the baseline, and stays under the cost ceiling.

## Open items from the build

*Partly superseded 2026-10-21: the current list, in priority order, is section 9 of the Phase 3 completion report (`docs/phase-3/build-reports/phase-3-completion.md` in the product repo), summarised in `product/architecture.md` under "The release path" and "Known open items".*

From the phase reports, newest first. None blocks the build; several block real testers or real gifts. Items that flip a switch in the app need the owner login (Jordan's); the decisions themselves belong to the partners.

| Item | Blocks |
|---|---|
| Switch card-making + studio on, make the first real card (Steph first), enter model prices (D14, D22) | Everything real — first card, first cost number, testers |
| AI credit budget for the first lab runs (D22) — asked once, unanswered | Planning how many runs |
| Open two pages and check Lovable's visitor stats don't count gift pages (W-37) | Sending any real gift link |
| ~~Where gifts live: uncard.app or uncard.gifts (D16, no default)~~ Settled 2026-10-06: uncard.gifts on a second Lovable project, per Jordan's plan | W-48 |
| Contact address for paused people (D20) | Suspending anyone |
| Schedule the nightly job in Lovable (D21) | Permanent daily totals, 13-month cleanup |
| Button colour: red (live) or green (W-50, side-by-side in the Phase 1 report) | — |
| Promote Brian and Tim to admin (D4) | Brian and Tim using admin |
| Publish the long-address fix (`b89cffe`) | Odd gift links answer 500 instead of 404 |
| Whether to split the sign-in library out of the gift page's download (Phase 5, E4) | — |
| Terms and Privacy wording; lawyer before launch (D10, D20) | Public launch |
| Phone checks listed in each report | — |

## Decisions

**Approved 30 Sep** (Jordan, on the build agent's recommendations): sample labels (D1) · invite testers once the studio works (D2) · 6–10 skippable interview questions, draft at 3 facts (D3) · Brian and Tim made admins after sign-in (D4) · green buttons trialled beside red (D5) · thin brief → shorter card (D6) · "private" = kept off share tiles, not hidden (D7) · Golden Pass covers everything (D8) · "coming soon" labels (D9) · Terms and Privacy drafted, lawyer before launch (D10) · pricing terms wait for payments (D11) · full measurement, recipients never tracked (D12).

**Still open, for the partners** (the build is running on the bold defaults): currency, CAD or USD (D11a) · raw-data retention, **13 months** or 30 days (D12b) · copy approvals (D13) · model prices (D14) · Metrics access, **owner + admins** (D15) · what happens to gifts if a pass is revoked or an account suspended, **they stay live** (D17) · milestone and birthday rules (D18–D19) · legal details (D20) · nightly job (D21) · AI budget (D22) · studio access before payments, **pass holders + staff** (D24) · email provider (D25) · scene rewrites per card, **5** (D26).

Live list: `improvement-spec.md` §8.3 in the product repo.

## Security note

`.env` is still committed to the product repo (checked 2026-10-02). It holds the Supabase project URL and **publishable** key only — designed to be public — and no service-role key. Low risk, but `.env` should be in `.gitignore` so a secret never follows it in.
