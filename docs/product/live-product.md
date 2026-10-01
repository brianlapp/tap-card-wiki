# The Live Product (MVP)

**Status:** Draft — snapshot of a moving target
**Updated:** 2026-10-01
**Owner:** Brian Lapp
**Method:** Read from the product repo [`JNabsRepo/uncard-starter`](https://github.com/JNabsRepo/uncard-starter) at commit `5649437` (2026-10-01): source code, `db/README.md`, and `docs/review-2026-09-30/` (build spec, work list, Oy's review). Not checked in a browser here. **Build status changes daily — for anything current, read the product repo, not this page.**

## TL;DR

UNCARD is live at **uncard.app** as a pitch-piece MVP. Two worlds and fifteen scenes play today. Sign-in, accounts, Golden Passes, an admin page and measurement are real. The AI card generator is built but **switched off** until Jordan turns it on. The studio and giving are still samples, being built in six phases by a Claude build agent.

## Where it lives

| What | Where |
|---|---|
| Code | [`JNabsRepo/uncard-starter`](https://github.com/JNabsRepo/uncard-starter), branch `main` |
| Editor | Lovable project `3a7b58dd-a027-4ee9-9df4-96c469e3f8ac` — commits sync both ways |
| Marketing + account site | **uncard.app** |
| Gift links | **uncard.gifts** in product copy (`uncard.gifts/r7Qm2xVb`); whether gifts are actually served from there is Jordan's open decision D16 |
| Build docs (source of truth for status) | `docs/review-2026-09-30/` in the product repo |

## Stack (verified)

- **TanStack Start** (React, Vite, TypeScript), file-based routes in `src/routes/`
- **Tailwind + shadcn/Radix** UI
- **Supabase**: auth, Postgres with row-level security everywhere; **Drizzle** migrations, each with SQL tests
- **AI**: Lovable AI gateway. Default model `openai/gpt-6-astra` — the only one confirmed to work; others are untested lab options
- **Bun** lockfile; `npm run dev` / `build` / `lint` / `format`

## What works today

| Area | State |
|---|---|
| Pages | Home, How it works, Examples, Scenes, Worlds, Pricing, Make, Give, Play, About, Brand, Sign in, Account, Admin, Terms, Privacy, gift page `/c/:cardId` |
| Worlds ready | **2 of 20**: T02 Firmware, T03 Quest Log. The rest say "coming soon" |
| Scenes ready | **15 of 50**: S01, S04, S06, S08, S14, S15, S16, S18, S26, S33, S37, S41, S47, S48, S50 |
| Sample uncards | **Steph, 9** (Quest Log) and **Jamie, 40** (Firmware) fully playable. Steph is the demo's Riley, renamed |
| Sign in | Google, or an email sign-in link. Adults only: 18+ confirmation |
| Studio (`/make`) | Labelled a sample. Typed text is not kept anywhere |
| Giving (`/give`) | Labelled a sample. PINs, keepsake download and reminders say "coming soon" |
| Card generator | Built, tested, **off**. Only the owner can switch it on |
| Payments | **Off.** None built |

Authoritative list of what's playable: `src/uncard/catalogue/support.ts` in the product repo.

## People and access

- **Roles:** creator (everyone), admin, owner. Exactly one owner: **Jordan**.
- **Only the owner** makes admins and switches card-making on or changes its limits. Brian and Tim are promoted by Jordan after they sign in (decision D4).
- **Golden Pass:** granted by email, even before sign-up. Covers everything, including hosting past three months (D8). Max 100 live passes. Owners, admins and pass holders skip the attempts allowance, but not the safety limits.
- **Everything is audited:** every access or settings change writes an `admin_audit` row in the same transaction.
- **The browser never writes** account, job, allowance or card tables. Roles are checked server-side only.

## How a card gets made (as built)

1. **Interview** → a brief: name, pronouns, age, relationship, signed-by, tone, things to avoid, and facts.
2. **Choose a world** filtered by age fit and what the player can draw today.
3. **One art-director call** → a ThemeSpec. Colours and fonts are forced from the kit, never from the model.
4. **Choose scenes**, preferring ones that shine in the world, following the arc. A thin brief makes a **shorter card**, never padding (D6).
5. **One writer call per scene.** Missing facts → skip without calling a model. The model can also skip.
6. **Assemble** into the player's card spec and save a draft.

**Guard rails, enforced in the database:** card-making switch (off by default); 60 calls a day and 30 per card; failed or timed-out jobs refund their attempt; a card's look must differ on 4 of 6 axes from the last 20 in its world, and an exact repeat is impossible. **Every model call's cost is recorded.**

Prompts stay server-side: the build fails if a page tries to import them.

## Measurement

First-party only, from day one. **Recipients are never tracked.**

**Five weekly questions:**
1. Are invited testers reaching a first usable card?
2. Where is card-making failing?
3. Did the last change keep cards factual, respectful and personal?
4. Can we afford the cards people approve?
5. Are the limits holding?

**Never measured:** anything about who opens a card; third-party analytics, pixels or scripts; card or brief text, names, birthdays, emails or private messages; keystrokes, session replay or emotion scores.

## Database (7 migrations)

| # | Adds |
|---|---|
| 0001 | Accounts: profiles, roles, adult confirmation |
| 0002 | Card generation: settings, allowances, jobs, calls, looks, drafts |
| 0003–0004 | Owner role, Golden Passes, admin audit |
| 0005 | The owner-only switch and caps |
| 0006 | Measurement store (six server-only tables) |
| 0007 | What each model call costs |

Every migration ships with SQL tests, most also run against the live database.

## How it's being built

A Claude build agent works through **six phases** from a 52-item work list Jordan approved on 30 Sep, publishing each phase to the live site once its checks pass:

0. Sign-in link ✓ · 1. Honest site + quick fixes · 2. Measurement + admin tools · 3. Card lab · 4. The real studio · 5. Giving · 6. Celebrations (built, switched off)

It stops for Jordan only for: AI spending, legal text, anyone's access, or anything irreversible. **Never:** payments, emails, tracking on gift pages, force-pushes.

Current progress: `docs/review-2026-09-30/build-reports/` in the product repo.

## Test people

Three fictional recipients, hash-locked so tests stay comparable:

| | Who | Why they're there |
|---|---|---|
| **Niko**, 9 | From Aunt Vera. Paper rockets, a cardboard moon | Must work without fast reading or winning a game |
| **Mira**, 27 | From her brother Ari. Playlists, a yellow mug | Sibling in-jokes; the giver wants control of wording |
| **Ada**, 80 | From her nephew Noel. Only three details | The hard one: must not invent a life story |

## Jordan's decisions

**Approved 30 Sep:** sample labels (D1) · invite testers once the studio works (D2) · 6–10 skippable interview questions, draft at 3 facts (D3) · Brian and Tim made admins after sign-in (D4) · green buttons trialled beside red (D5) · thin brief → shorter card (D6) · "private" = kept off share tiles, not hidden (D7) · Golden Pass covers everything (D8) · "coming soon" labels (D9) · Terms and Privacy drafted, lawyer before launch (D10) · pricing terms wait for payments (D11) · full measurement, recipients never tracked (D12).

**Still open** (defaults in bold where the spec has one): currency, CAD or USD (D11a) · raw-data retention, **13 months** or 30 days (D12b) · copy approvals (D13) · model prices after first lab runs (D14) · Metrics access, **owner + admins** (D15) · gift-page analytics vs serving gifts from uncard.gifts (D16, no default) · what happens to cards if a pass is revoked or an account suspended (D17) · milestone and birthday rules (D18–D19) · legal details (D20) · cron (D21) · AI budget and switching generation on (D22) · studio access before payments, **pass holders + staff** (D24) · email provider (D25) · scene regenerations per card, **5** (D26).

Live list: `improvement-spec.md` §8.3 in the product repo.

## Security note

`.env` is committed to the product repo. It holds the Supabase project URL and **publishable** key only — designed to be public — and no service-role key. Low risk, but `.env` should be in `.gitignore` so a secret never follows it in.
