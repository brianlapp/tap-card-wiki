# The Live Product (MVP)

**Status:** Draft — snapshot of a moving target
**Updated:** 2026-10-02
**Owner:** Brian Lapp
**Method:** Read from the product repo [`JNabsRepo/uncard-starter`](https://github.com/JNabsRepo/uncard-starter) at commit `ffd1adc` (2026-10-02): the five phase reports in `docs/review-2026-09-30/build-reports/`, `db/README.md`, `roadmap.md`, Oy's round-2 prompt and `src/uncard/catalogue/support.ts`. Not checked in a browser here — what's "live" is what the build agent's reports say it published. **Build status changes daily — for anything current, read the product repo, not this page.**

## TL;DR

UNCARD is live at **uncard.app**. Phases 0 to 5 of the six-phase build are built and published. The real studio (the interview, edit, approve) and giving (private links, PINs, withdraw) **exist but are shut**: nobody can make or give a real uncard until Jordan switches card-making and the studio on. No AI credits have been spent; the real AI gateway has never been called. Phase 6 (celebrations) is not built. Two worlds and fifteen scenes play, unchanged since 1 Oct.

## Changed since the 2026-10-01 snapshot

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
| Gift links | Served from uncard.app at `/c/:id` today. Serving them from **uncard.gifts** instead is Jordan's open decision D16 (no default; not built) |
| DNS | Both domains on **Cloudflare** (Jordan's account). uncard.app and www point at Lovable's hosting (DNS only, not proxied). **invest.uncard.app** is a proxied placeholder record, so something on Cloudflare serves it (a Worker or Pages site, unverified). uncard.gifts has **no DNS records** and serves nothing. No Worker routes on either zone (read via API, 2026-10-02) |
| Build docs (source of truth for status) | `docs/review-2026-09-30/` in the product repo — one report per phase in `build-reports/` |

## Stack (verified)

- **TanStack Start** (React, Vite, TypeScript), file-based routes in `src/routes/`
- **Tailwind + shadcn/Radix** UI
- **Supabase**: auth, Postgres with row-level security everywhere; **Drizzle** migrations, each with SQL tests
- **AI**: Lovable AI gateway. Default model `openai/gpt-6-astra`. Never called by the build yet — every AI answer in the build's checks was a stand-in
- **Bun** lockfile; `npm run dev` / `build` / `lint` / `format`

## What works today

| Area | State |
|---|---|
| Worlds ready | **2 of 20**: T02 Firmware, T03 Quest Log. The rest say "coming soon" |
| Scenes ready | **15 of 50**: S01, S04, S06, S08, S14, S15, S16, S18, S26, S33, S37, S41, S47, S48, S50 |
| Sample uncards | **Steph, 9** (Quest Log) and **Jamie, 40** (Firmware), fully playable |
| Sign in | Google (official button) or an email sign-in link. Adults only: 18+ confirmation |
| Studio | **Built, shut three ways**: a code switch, a database switch only Jordan can flip, and card-making being off. Plain `/make` still shows the Steph sample. Testers will enter at `/make?studio=1` |
| Giving | **Built and published**, but nothing can be given until the studio opens. Unknown, closed or withdrawn links all show the same "This uncard isn't here." page |
| Card lab | `/admin/lab` — make a test card and watch every model call, its tokens and cost. Unused: card-making is off |
| Admin | Tabs: People and cards, Testers, Metrics, Gifts. Panels for the card-making switch and the studio (owner only) |
| Card-making | **Off.** Limits unchanged: 60 calls a day, 30 per card |
| Payments | **Off.** None built |
| Celebrations (Phase 6) | **Not built.** The build agent ran out of room in its session; it's the next job |

Authoritative list of what's playable: `src/uncard/catalogue/support.ts` in the product repo.

## What making an uncard will feel like (built, shut)

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
- **Only the owner** makes admins, switches card-making or the studio on, or changes their limits. Brian and Tim are promoted by Jordan after they sign in (D4) — **not done yet** as of 2 Oct.
- **Golden Pass:** granted by email, even before sign-up, singly or as a list of up to 50. Covers everything, including hosting past three months (D8).
- **Suspend and restore** exist. A suspended person sees "contact [contact email]" — the address is still a placeholder (D20), so nobody should be suspended yet.
- **Cloudflare:** since 2026-10-02 Brian is **Domain Administrator** on uncard.app and uncard.gifts (plus Workers Routes), not a member of Jordan's account. So he can change DNS, settings, SSL, cache and Worker *routes*, but cannot deploy Worker *code* — that needs an account-level role from Jordan (e.g. Workers Admin). Brian's agents use a zone-only API token (1Password: "Cloudflare API Token (uncard)"). Relevant if D16 puts gifts on uncard.gifts. Changing DNS touches the live site, so it's still Jordan's call.
- **Everything is audited:** every access, settings or gift-withdrawal change writes an `admin_audit` row in the same transaction.
- **The browser never writes** account, job, allowance or card tables. Roles are checked server-side only.

## How a card gets made (as built)

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

## Waiting on Jordan

From the phase reports, newest first. None blocks the build; several block real testers or real gifts.

| Item | Blocks |
|---|---|
| Switch card-making + studio on, make the first real card (Steph first), enter model prices (D14, D22) | Everything real — first card, first cost number, testers |
| AI credit budget for the first lab runs (D22) — asked once, unanswered | Planning how many runs |
| Open two pages and check Lovable's visitor stats don't count gift pages (W-37) | Sending any real gift link |
| Where gifts live: uncard.app or uncard.gifts (D16, no default) | W-48 |
| Contact address for paused people (D20) | Suspending anyone |
| Schedule the nightly job in Lovable (D21) | Permanent daily totals, 13-month cleanup |
| Button colour: red (live) or green (W-50, side-by-side in the Phase 1 report) | — |
| Promote Brian and Tim to admin (D4) | Brian and Tim using admin |
| Publish the long-address fix (`b89cffe`) | Odd gift links answer 500 instead of 404 |
| Whether to split the sign-in library out of the gift page's download (Phase 5, E4) | — |
| Terms and Privacy wording; lawyer before launch (D10, D20) | Public launch |
| Phone checks listed in each report | — |

## Jordan's decisions

**Approved 30 Sep:** sample labels (D1) · invite testers once the studio works (D2) · 6–10 skippable interview questions, draft at 3 facts (D3) · Brian and Tim made admins after sign-in (D4) · green buttons trialled beside red (D5) · thin brief → shorter card (D6) · "private" = kept off share tiles, not hidden (D7) · Golden Pass covers everything (D8) · "coming soon" labels (D9) · Terms and Privacy drafted, lawyer before launch (D10) · pricing terms wait for payments (D11) · full measurement, recipients never tracked (D12).

**Still open** (the build is running on the bold defaults): currency, CAD or USD (D11a) · raw-data retention, **13 months** or 30 days (D12b) · copy approvals (D13) · model prices (D14) · Metrics access, **owner + admins** (D15) · gift hosting, uncard.app or uncard.gifts (D16, no default) · what happens to gifts if a pass is revoked or an account suspended, **they stay live** (D17) · milestone and birthday rules (D18–D19) · legal details (D20) · nightly job (D21) · AI budget (D22) · studio access before payments, **pass holders + staff** (D24) · email provider (D25) · scene rewrites per card, **5** (D26).

Live list: `improvement-spec.md` §8.3 in the product repo.

## Security note

`.env` is still committed to the product repo (checked 2026-10-02). It holds the Supabase project URL and **publishable** key only — designed to be public — and no service-role key. Low risk, but `.env` should be in `.gitignore` so a secret never follows it in.
