# Scope

**Status:** Draft
**Updated:** 2026-09-20
**Owner:** Brian Lapp
**Method:** Distilled from the 526-task build catalogue Google Sheet. Stack below is partly inferred from Lovable defaults and is (unverified) until the repo is confirmed.

## TL;DR

Personalized interactive birthday cards adults create for kids. First milestone is one synthetic card working end to end. Everything else waits.

## What it is

A slideshow player renders themed scenes from a versioned card JSON: opening boot, greeting, mini-games, mixtape/music, certificate, candles finale, closing note. Kids open a link — no child accounts.

Reference implementation: `jordan-exe-birthday.netlify.app`, an adult one-off demo. This project turns its modules into a reusable kids-first product.

Build catalogue: https://docs.google.com/spreadsheets/u/1/d/1d7c4FesVy08oaTlquBT3FbXUPGZa0_70/htmlview

## Tech stack

**Product app**
- Lovable, synced to GitHub (repo URL unknown — see `decisions/0001`)
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
- Suno for songs — manual pilot; commercial rights (unverified)

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
- Planned pricing $4.99/card, $9.99/month — not built, and contested (see `decisions/0002`)
- Music needs verified commercial rights before any use
- No promise of one-click social posting
- Reduced motion, mute, keyboard and touch support required

## Architecture principles

- One shared Player + versioned card JSON; no bespoke site per card
- Scenes are reusable modules driven by schema data
- 10 reusable skins via design tokens (Quest first)
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

## Team (proposed, not yet accepted)

- Jordan — direction and commercial (43 tasks)
- Tim Miller — experience and quality (167)
- Brian Lapp — engineering and reliability (316)

## Open questions

1. Which Lovable project, repo and branch are authoritative?
2. Does a staging environment exist?
3. Is the backend actually Supabase?
