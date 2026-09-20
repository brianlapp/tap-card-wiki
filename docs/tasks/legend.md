# Task Catalogue Legend

**Status:** Draft
**Updated:** 2026-09-20
**Owner:** Brian Lapp
**Method:** Generated from `Tapcard_Build_Catalogue.xlsx` (Jordan's Drive) on 2026-09-20. Row parse validated against the workbook's own summary tab — phase counts, owner counts and 526 unique task IDs all matched exactly. Column *meanings* below are inferred from their values and are (unverified) by Jordan.

## Why this file exists

Six of the workbook's 24 columns are effectively constant — the same sentence repeated hundreds of times. Storing them per-row cost ~90,000 characters and told an agent nothing. They live here instead, read once.

## Columns in `tasks.csv`

| Column | Meaning |
|---|---|
| `task_id` | Stable ID, e.g. `T-002`. Primary key across all files. |
| `phase` | Delivery stage, P0 through P4 or Deferred. |
| `area` | Workstream grouping, e.g. "Scope and governance". |
| `component_id` | Component this belongs to, e.g. `C-SCOPE`. |
| `task` | What to actually do. |
| `proposed_owner` | Jordan, Brian Lapp or Tim Miller. **Proposed, not accepted** (that is T-003). |
| `status` | Backlog / To verify / Deferred. |
| `size` | S = 1–2h, M = 2–4h. Proposed estimates. |
| `depends_on` | Task ID that must land first. Blank = no stated prerequisite. |
| `priority` | P0 / P1 / P3 as recorded in the workbook. |

## Columns in `task-details.csv`

Keyed by `task_id`. Load only when you need the detail of a specific task.

| Column | Meaning |
|---|---|
| `output` | The artefact the task produces. |
| `acceptance` | The bar for calling it Done. |
| `task_kind` | Creation / Judgment / Coordination / Pattern. |
| `build_tool` | Which agent or human is proposed to build it (see codes below). |
| `runtime_approach` | What runs in production for this task. |
| `eval_ids` / `event_ids` / `lever_ids` | Cross-references into the workbook's Evaluations, Telemetry and Levers tabs (**not yet exported**). |

## Build tool codes

| Code | Tasks |
|---|---|
| M-SOL | 257 |
| M-LUNA | 72 |
| M-HUMAN | 68 |
| M-JEV | 48 |
| M-ASTRA | 43 |
| M-IMAGE | 12 |
| M-SUNO | 12 |
| M-LOVABLE | 10 |
| M-GROK | 4 |

`M-HUMAN` means no model — a person does it.

## Distributions

| Status | Tasks |
|---|---|
| Backlog | 498 |
| To verify | 14 |
| Deferred | 14 |

| Priority | Tasks |
|---|---|
| P1 | 442 |
| P0 | 72 |
| P3 | 12 |

| Size | Tasks |
|---|---|
| S: 1–2h proposed | 472 |
| M: 2–4h proposed | 54 |

| Task kind | Tasks |
|---|---|
| Creation | 248 |
| Pattern | 189 |
| Judgment | 72 |
| Coordination | 17 |

## Near-constant columns (dropped from the CSVs)

These were identical on almost every row. Recorded here once.

### Rollback — 13 distinct values across 526 tasks
| Value | Tasks |
|---|---|
| Revert reviewed commit/config version; retain audit record | 318 |
| Pin previous approved asset version; quarantine disputed candidate | 64 |
| Disable this emitter or restore schema adapter; preserve transaction correctness | 60 |
| Disable question route; restore rules/human workflow | 48 |
| Restore previous export recipe; invalidate faulty derived assets | 12 |
| Disable routine and revoke scoped write access | 3 |
| Stop runner; restore previous suite version | 3 |
| Disable route; retain prior accepted draft | 3 |
| Disable route; rules or human fallback | 3 |
| Pause queue; revoke provider token; invalidate faulty candidate | 3 |
| Pause; route all cases to human queue | 3 |
| Disable alert job; restore queue state with approval | 3 |
| Archive proposal; stop routine; no live state affected | 3 |

### Source/evidence — 60 distinct
Top values only; 340 of 526 rows say the same thing.

| Value | Tasks |
|---|---|
| v1.1 playbook + current request; implementation unverified | 340 |
| Inline CSS or arcade.js | 18 |
| Inline Web Audio functions | 14 |
| https://jordan-exe-birthday.netlify.app/\#mixtape; inline audio handlers | 8 |
| Google Fonts CSS | 5 |
| https://jordan-exe-birthday.netlify.app/\#boot; HTML/CSS/inline handlers | 5 |
| https://jordan-exe-birthday.netlify.app/\#boot | 5 |
| https://jordan-exe-birthday.netlify.app/\#order | 5 |

### Disposition candidate
| Value | Tasks |
|---|---|
| pilot_step_5 candidate | 377 |
| stay_human | 89 |
| agent_now candidate | 60 |

### Readiness (1–5, proposed)
| Value | Tasks |
|---|---|
| 3 | 377 |
| 2 | 89 |
| 4 | 60 |

### Evidence/notes
| Value | Tasks |
|---|---|
| (blank) | 446 |
| Map asset to affected scene tasks; do not commission a new asset when  | 64 |
| Recurring template, not a scheduled automation. Record each occurrence | 16 |

### Dependency/evidence check
| Value | Tasks |
|---|---|
| Wait: prerequisites | 524 |
| Ready for owner | 1 |
| Wait: prerequisites Dependencies Task ID | 1 |

Essentially constant. Carries no information; ignore it.

## Not yet exported

The workbook has further tabs this export does not cover: Components (91), Evaluations (54), Telemetry events (60), Agent contracts, Data contracts, Decisions, Release gates, Benchmark, Readiness, Inspection, Sources.

`eval_ids`, `event_ids` and `lever_ids` therefore point at things not yet in this repo.
