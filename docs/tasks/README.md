# Task Catalogue

**Status:** Draft
**Updated:** 2026-09-20
**Owner:** Brian Lapp
**Method:** Exported from `Tapcard_Build_Catalogue.xlsx` (Jordan's Drive) on 2026-09-20 and restructured for agent use. Parse validated against the workbook's own summary tab: 526 unique task IDs, phase counts and owner counts all matched exactly. Column meanings in `legend.md` are inferred and (unverified) by Jordan.

## TL;DR

526 tasks, queryable without loading them all. **Start here, not in the spreadsheet.**

```bash
grep '^T-002,' docs/tasks/tasks.csv          # one task
grep ',P0 Define and verify,' docs/tasks/tasks.csv   # one phase
grep ',Brian Lapp,' docs/tasks/tasks.csv     # one owner
```

## Read this much, and no more

| You need | Read | Cost |
|---|---|---|
| Counts, how to query | this file | ~800 tokens |
| One task's basics | `grep` one line from `tasks.csv` | **~40 tokens** |
| One task's detail | `grep` one line from `task-details.csv` | ~70 tokens |
| What a column means | `legend.md` | ~1,300 tokens |
| Everything (rarely needed) | both CSVs | ~48,000 tokens |

For comparison, answering "what is T-002?" from the original spreadsheet costs **~118,000 tokens**. From here it costs about **40**.

## Files

| File | Size | What |
|---|---|---|
| `tasks.csv` | 86076 bytes | 526 rows. The 10 columns you filter and plan on. |
| `task-details.csv` | 106792 bytes | 526 rows keyed by `task_id`. Output, acceptance, tooling. |
| `legend.md` | — | Column meanings, code tables, and the near-constant columns. |

Split deliberately: most questions are answered by `tasks.csv` alone, so the verbose fields stay out of the way until asked for.

## The numbers

| Phase | Tasks |
|---|---|
| P0 Define and verify | 14 |
| P1 Shared foundation | 116 |
| P2 Card experience | 214 |
| P3 Sharing and pilot | 68 |
| P4 Learning and efficiency | 100 |
| Deferred | 14 |

| Proposed owner | Tasks |
|---|---|
| Brian Lapp | 316 |
| Tim Miller | 167 |
| Jordan | 43 |

Status: 498 Backlog, 14 To verify, 14 Deferred. **Nothing is Done.**

## Where to start

P0 has six kickoff tasks. T-002 is the blocker — it is the "find the authoritative project" task, and it is yours:

```bash
grep -E '^T-00[1-6],' docs/tasks/tasks.csv
```

See `../decisions/0001-source-of-truth.md`.

## Rules for agents

- **This repo is the task list.** See `../decisions/0003-task-catalogue-source.md`.
- **Do not load the spreadsheet.** It costs ~118,000 tokens and needs Jordan's Drive. Everything useful from it is here.
- **Grep, don't read.** These are CSVs so you can pull one row. Loading a whole file should be a deliberate choice.
- **Owners are proposed, not accepted.** T-003 is the task that makes them real.
- **Statuses are stale by design** until the sync in ADR 0003 is running.
