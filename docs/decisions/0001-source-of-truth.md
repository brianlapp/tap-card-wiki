# 0001 — Authoritative project, repo and branch

**Status:** Accepted
**Date:** 2026-09-20 · **Decided:** 2026-09-30
**Deciders:** Jordan, Brian Lapp

## Context

The build catalogue contains 526 tasks but no link to the actual product. The only URL referenced is the adult demo `jordan-exe-birthday.netlify.app` (linked 197 times). No Lovable project URL, no GitHub repo, no staging URL. Task T-002 in the catalogue is literally "confirm the authoritative product project and branch."

Nothing can be built, and no agent can be pointed at code, until this is answered.

## Options

1. **Confirm the existing Lovable project** — preserves whatever backend, accounts and data already exist. Requires Jordan.
2. **Start a fresh repo** — clean, but risks abandoning working auth, database and deployed cards. Rejected unless option 1 proves there's nothing usable.

## Decision

Resolved 2026-09-30 after Brian's meeting with Jordan: **there is no product repo, Lovable project or backend.** The only working version of UNCARD is the mockup — the brand demo artifact, saved in this repo at `examples/uncard-demo/` and treated as the line of truth (`0005`).

Neither option above applied. The build starts from scratch, using the mockup as the reference.

## Required answers

- [x] Lovable project URL — **none exists**
- [x] GitHub repo and default branch — **none exists**; this wiki is the only repo
- [x] Staging environment — **none**
- [x] Backend — **none**; Supabase was only ever an assumption from Lovable defaults
- [x] Is anyone else editing outside this repo — the mockup is a claude.ai artifact; see `examples/README.md`

## Consequences

- ~~Until resolved: no code changes, no scaffolding, no schema work.~~ Resolved: there is nothing existing to protect, so there is nothing to rebuild over.
- Choosing a stack and creating the product repo is now its own decision, not yet made.
- Tasks written to find or verify the existing project are answered or moot — listed in `../tasks/README.md`.

## Note

A separate docs repo exists at https://github.com/brianlapp/tap-card-wiki for project context. It holds docs only, no code, so it can be merged into the product repo later or kept as the planning repo.
