# 0003 — Task catalogue lives in the repo

**Status:** Accepted (repo side); Jordan's confirmation still required
**Date:** 2026-09-20
**Deciders:** Brian Lapp (decided), Jordan (owns the spreadsheet)

## Context

The 526-task build catalogue lived only in `Tapcard_Build_Catalogue.xlsx` in Jordan's Drive. As a source of truth for agents it failed on every axis, measured on 2026-09-20:

- **471,738 characters** — roughly 118,000 tokens to read once. It exceeded the read tool's limit and had to be spilled to disk and parsed offline.
- **Binary `.xlsx`** — cannot be grepped, cannot be diffed, no git history.
- **Auth-gated** — sits in Jordan's Drive, so a CI or headless agent cannot reach it at all.
- **No row structure** in the text rendering — 526 rows arrive as one continuous smear.
- **~11% literal repetition** — one rollback sentence appears 318 times, one provenance sentence 357 times.

Answering "what is T-002?" — a 40-token fact — cost about 118,000 tokens.

Project context is now the expensive, load-bearing asset. It has to be as well organised as code, and cheap to read.

## Options

1. **Repo is canonical.** Tasks live in git; the spreadsheet becomes a view. Agents get fast, cheap, diffable data. Cost: Jordan has to accept that status changes are recorded outside his spreadsheet.
2. **Spreadsheet is canonical, repo holds a dated export.** Jordan keeps working exactly as he does now. Cost: the repo copy is knowingly behind, and silent drift is possible between exports.
3. **Leave it as-is.** Rejected — every agent pays ~118,000 tokens, and headless agents simply cannot read it.

## Decision

**Option 1.** The repo is the real task list.

Exported to `docs/tasks/`, restructured for progressive disclosure:

- `tasks.csv` — the 10 columns used for filtering and planning
- `task-details.csv` — verbose per-task fields, keyed by `task_id`
- `legend.md` — column meanings, code tables, and the six near-constant columns lifted out of the rows

Result: one task now costs ~40 tokens to look up instead of ~118,000.

## Export fidelity

The parse was validated against the workbook's own summary tab before being trusted:

- 526 rows, 526 unique task IDs — matches
- Phase counts (14 / 116 / 214 / 68 / 100 / 14) — exact match
- Owner counts (Jordan 43, Brian Lapp 316, Tim Miller 167) — exact match

Column *meanings* in `legend.md` are inferred from their values and are (unverified) by Jordan.

## Drift protection

Not yet built. The intended shape:

1. A scheduled job exports the sheet to CSV on a fixed cadence
2. It diffs that export against `docs/tasks/`
3. On any difference it opens a PR or an issue — it does **not** silently overwrite

Direction of travel matters: this is a **drift alarm**, not a sync. If the repo is canonical, a change appearing only in the spreadsheet is a signal that someone edited the wrong copy, and a human should see it. Silent overwriting would quietly restore the spreadsheet as the boss and undo this decision.

Requires a Google service account with read access to the sheet — which requires Jordan.

## Consequences

- Agents read `docs/tasks/`. **Loading the spreadsheet is now a mistake**, and `docs/tasks/README.md` says so.
- Status changes are recorded in the repo. Until the alarm above runs, the two copies can diverge unnoticed.
- The export is a snapshot dated 2026-09-20. It has no live connection to the sheet.
- Not yet exported: Components (91), Evaluations (54), Telemetry events (60), Agent contracts, Data contracts, Decisions, Release gates, Benchmark, Readiness, Inspection, Sources. So `eval_ids`, `event_ids` and `lever_ids` currently point at nothing in this repo.

## Required from Jordan

- [ ] Agree the repo is where task status is recorded
- [ ] Confirm the inferred column meanings in `legend.md`
- [ ] Service account (or equivalent read access) for the drift alarm
- [ ] Decide whether the remaining tabs are worth exporting
