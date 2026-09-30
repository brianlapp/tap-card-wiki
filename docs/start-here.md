# Start Here

**Status:** Draft
**Updated:** 2026-09-30
**Owner:** Brian Lapp
**Method:** Written by hand. Token figures are measured, not estimated — see below.

## What this is

The shared brain for **UNCARD** (formerly Tapcard) — personalized, interactive birthday cards that adults make for someone they love. Not a card. A whole little world.

Scope, competitor research, decisions and the full 526-task build list live here. One place, so people and AI agents read the same thing.

## Why it exists

The plan used to live in a 221KB spreadsheet. Asking it a single question — *"what is task T-002?"* — meant an agent loading the whole workbook:

| Asking "what is T-002?" | Cost |
|---|---|
| From the spreadsheet | **~118,000 tokens** |
| From this wiki | **~35 tokens** |

Same answer. Roughly **3,000× cheaper**.

That is the entire point of this repo. The answer was never the expensive part — *finding* it was. Agents burn their budget wading through a format built for humans, then have less left for the actual work.

So the content got restructured for machines: small files, one fact per line, greppable, with the repeated boilerplate lifted out. It stayed readable for people too — that is what this page you are reading is.

## How to use it

**Browse it** — the sidebar on the left has everything. On a phone, tap **☰** at the top.

**Start with what you need:**

- New here → `product/experience.md` — what it's like to make one and to open one
- What a card is made of → `catalogue/README.md` — 50 scenes, 20 worlds
- The look and voice → `brand/directions.md` — two directions, both shown
- The build plan → `product/scope.md`
- Wondering why something was chosen → `decisions/` — the numbered records, including the ones still open
- Need a task → `tasks/README.md` — how to query the 526 without loading them all
- Adding something → `conventions.md` first

**If you are an agent:** read `AGENTS.md` at the repo root, then load only what your task needs. Do not open the spreadsheet.

## A word on trust

Not everything here is confirmed. Anything marked `(unverified)` or `(assumption)` is a working guess, and three decisions are still open — the authoritative project repo, pricing, and the brand direction.

That is deliberate. A wiki that quietly states guesses as facts is worse than no wiki, because nobody knows which parts to check. If you know better than something written here, you are the source — correct it.

## Open questions

Waiting on Jordan:

1. Which Lovable project, repo and branch are authoritative? (`decisions/0001`)
2. One-off purchase or subscription — and at which of three prices? (`decisions/0002`)
3. Matinee or Midnight? (`decisions/0004`)
