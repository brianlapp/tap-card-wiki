# 0001 — Authoritative project, repo and branch

**Status:** Open
**Date:** 2026-09-20
**Deciders:** Jordan, Brian Lapp

## Context

The build catalogue contains 526 tasks but no link to the actual product. The only URL referenced is the adult demo `jordan-exe-birthday.netlify.app` (linked 197 times). No Lovable project URL, no GitHub repo, no staging URL. Task T-002 in the catalogue is literally "confirm the authoritative product project and branch."

Nothing can be built, and no agent can be pointed at code, until this is answered.

## Options

1. **Confirm the existing Lovable project** — preserves whatever backend, accounts and data already exist. Requires Jordan.
2. **Start a fresh repo** — clean, but risks abandoning working auth, database and deployed cards. Rejected unless option 1 proves there's nothing usable.

## Decision

Pending. Blocked on Jordan.

## Required answers

- [ ] Lovable project URL
- [ ] GitHub repo and default branch
- [ ] Staging environment: exists or not
- [ ] Backend: Supabase or something else
- [ ] Is anyone else editing outside this repo

## Consequences

Until resolved: no code changes, no scaffolding, no schema work. Docs and research only.

## Note

A separate docs repo exists at https://github.com/brianlapp/tap-card-wiki for project context. It holds docs only, no code, so it can be merged into the product repo later or kept as the planning repo.
