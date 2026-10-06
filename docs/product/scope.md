# Scope

**Status:** Draft
**Updated:** 2026-10-06
**Owner:** Brian Lapp
**Method:** Distilled from the 526-task build catalogue Google Sheet. Stack below is partly inferred from Lovable defaults and is (unverified) until the repo is confirmed.

## TL;DR

Personalized interactive birthday cards adults create for someone they love — the whole family, kids through 60+ (`0005`; previously "for kids"). First milestone is one synthetic card working end to end. Everything else waits.

## What it is

A slideshow player renders themed scenes from a versioned card JSON: opening boot, greeting, mini-games, mixtape/music, certificate, candles finale, closing note. Kids open a link — no child accounts.

> **Update 2026-09-30.** The scene list above was the Jordan.EXE starting point. It is now superseded by a catalogue of **50 sections and 20 themes** (`../catalogue/`), a **nine-beat arc** of 8–10 scenes (`experience.md`), and the working name **UNCARD** (`../brand/directions.md`).
>
> **Audience (resolved by `0005`):** not kids-first. UNCARD is for anyone someone loves — the whole family, kids through 60+. Every "kids-first" statement below is superseded. Child-safety rules (no child accounts, Link + PIN for kids) still stand.

Reference implementation: `jordan-exe-birthday.netlify.app`, an adult one-off demo. This project turns its modules into a reusable product. ~~kids-first~~ *(superseded by `0005`)*

Build catalogue: https://docs.google.com/spreadsheets/u/1/d/1d7c4FesVy08oaTlquBT3FbXUPGZa0_70/htmlview

## Tech stack

**Product app**
- Lovable, synced to GitHub: [`JNabsRepo/uncard-starter`](https://github.com/JNabsRepo/uncard-starter) — **verified 2026-10-01** (`../decisions/0001`). *(The 2026-09-30 note that none existed was wrong.)*
- Verified from the repo: **TanStack Start** (React + Vite + TypeScript), **Tailwind + shadcn/Radix**, **Supabase** (auth, Postgres) with **Drizzle** migrations. The (assumption) markers on the lines below are resolved by this.
- React + Vite + TypeScript (assumption: Lovable default)
- Tailwind CSS + shadcn/ui (assumption)
- Supabase: auth, Postgres, storage, edge functions (assumption)

**Player and scenes**
- React components driven by the card JSON schema
- SVG illustration + CSS animation
- Three.js, pinned version, with SVG fallback when WebGL is unavailable
- Canvas for confetti/particles (seeded, capped)
- Web Audio API for procedural sound
- Fonts: Rubik Glitch, Big Shoulders Display, Permanent Marker, Chivo, Red Hat Mono

**AI and media**
- OpenAI text generation, server-side via a provider adapter, pinned versions
- OpenAI image generation, offline and human-reviewed
- ~~Suno for songs — manual pilot; commercial rights (unverified)~~ superseded 2026-10-05: Suno is out (no public API, terms ban automation and redistribution). Songs must come from a cloud API; candidates are Google Lyria, ElevenLabs Music and ACE-Step, with rights still to be confirmed (`slack/ledger.md`)

**Sharing**
- PNG first, then deterministic MP4
- Web Share API with download and copy-link fallbacks
- 9:16 (1080x1920), 1:1 (1080x1080), 4:5 (1080x1350)

**Analytics:** first-party event pipeline, schema-validated, no PII
**Payments:** Stripe deferred — do not connect

## Constraints

- Adult accounts only; no child logins or child contact data
- No PII in telemetry
- Unlimited free creation for approved founders/family, separate from admin
- Pricing: **$5.99 per uncard, $9.99/month for two**, 3 months hosting then free keepsake or $3/year (`0005`). ~~$4.99/card, $9.99/month~~ superseded. Not built. (see `decisions/0002`)
- Music needs verified commercial rights before any use
- No promise of one-click social posting
- Reduced motion, mute, keyboard and touch support required

## Architecture principles

- One shared Player + versioned card JSON; no bespoke site per card
- Scenes are reusable modules driven by schema data
- 10 reusable skins via design tokens (Quest first) — *superseded 2026-09-30: the Themes catalogue defines 20 themes, each a fixed DNA plus a six-axis kit (`../catalogue/`). Quest survives as T03 Quest Log.*
- Drafts separate from immutable published versions
- Every change has a rollback path

## Phases

| Phase | Tasks |
|---|---|
| P0 Define and verify | 14 |
| P1 Shared foundation | 116 |
| P2 Card experience | 214 |
| P3 Sharing and pilot | 68 |
| P4 Learning and efficiency | 100 |
| Deferred (incl. all payments) | 14 |

## Team

Jordan, Brian and Tim are **equal partners** (Brian, 2026-10-02). Areas of focus (task counts from the build catalogue):

- Jordan — direction and commercial (43 tasks). Holds the app's owner login
- Tim Miller — experience and quality (167)
- Brian Lapp — engineering, infrastructure and reliability (316)

## Open questions

1. ~~Which Lovable project, repo and branch are authoritative?~~ `JNabsRepo/uncard-starter`, `main` (`0001`).
2. ~~Does a staging environment exist?~~ No; each phase is published to the live site after its checks (`0001`).
3. ~~Is the backend actually Supabase?~~ Yes, verified (`0001`).
