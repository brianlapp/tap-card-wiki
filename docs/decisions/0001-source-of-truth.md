# 0001 — Authoritative project, repo and branch

> **In plain words:** The real product code lives in Jordan's uncard-starter project on GitHub. That's the one everyone builds from.

**Status:** Accepted
**Date:** 2026-09-20 · **Decided:** 2026-09-30 · **Corrected:** 2026-10-01
**Deciders:** Jordan, Brian Lapp

## Context

The build catalogue contains 526 tasks but no link to the actual product. The only URL referenced is the adult demo `jordan-exe-birthday.netlify.app` (linked 197 times). No Lovable project URL, no GitHub repo, no staging URL. Task T-002 in the catalogue is literally "confirm the authoritative product project and branch."

Nothing can be built, and no agent can be pointed at code, until this is answered.

## Options

1. **Confirm the existing Lovable project** — preserves whatever backend, accounts and data already exist. Requires Jordan.
2. **Start a fresh repo** — clean, but risks abandoning working auth, database and deployed cards. Rejected unless option 1 proves there's nothing usable.

## Decision

**The product repo is [`JNabsRepo/uncard-starter`](https://github.com/JNabsRepo/uncard-starter), branch `main`.** It is a Lovable project (TanStack Start template), live at **uncard.app**, with a Supabase backend and Drizzle migrations. Commits since 2026-09-22.

> **Correction 2026-10-01.** On 2026-09-30 this record said no repo, Lovable project or backend existed. That was wrong — the repo already existed. Brian supplied the link on 2026-10-01.

The brand demo (`examples/uncard-demo/`) remains the line of truth for **what the product should be** (`0005`). The product repo is the source of truth for **what is built and being built**, and for its own build docs (`docs/review-2026-09-30/` there).

## Required answers

- [x] Lovable project URL — `lovable.dev/projects/3a7b58dd-a027-4ee9-9df4-96c469e3f8ac` (from the repo README)
- [x] GitHub repo and default branch — `JNabsRepo/uncard-starter`, `main`
- [x] Staging environment — none separate; the build agent publishes each phase to the live site after its checks pass (product repo `docs/review-2026-09-30/OPERATING-MODE.md`)
- [x] Backend — **Supabase** (verified: `@supabase/supabase-js`, `.env`, 7 Drizzle migrations with SQL tests)
- [x] Is anyone else editing outside this repo — yes: Lovable and a Claude build agent both commit to the product repo. Lovable warns never to rewrite its history.

## Consequences

- Nothing in this wiki is code. Product work happens in the product repo; this wiki links to it and never copies its build docs, so the two can't drift.
- The 2026-09-30 "nothing to rebuild over" consequence is withdrawn: a working backend exists and must be preserved.
- `T-002` is answered. `T-SCOPE-02`, `T-SCOPE-03` and `T-OPS-01` are live again — see `../tasks/README.md`.

## Note

A separate docs repo exists at https://github.com/brianlapp/tap-card-wiki for project context. It holds docs only, no code, so it can be merged into the product repo later or kept as the planning repo.
