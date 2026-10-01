# Task Catalogue

**Status:** Draft
**Updated:** 2026-09-30
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

P0 has six kickoff tasks. T-002 ("find the authoritative project") is answered: `JNabsRepo/uncard-starter` (`../decisions/0001-source-of-truth.md`).

> **Two work lists exist.** This 526-task plan, and the product repo's 52-item `docs/review-2026-09-30/prioritized-work.csv` (W-01…), which is what the build agent is actually executing in six phases. How the two relate is not yet decided.

```bash
grep -E '^T-00[1-6],' docs/tasks/tasks.csv
```

See `../decisions/0001-source-of-truth.md`.

## Known drift from the current product

The build plan predates the UNCARD brand demo, which is now the line of truth (`../decisions/0005-demo-is-source-of-truth.md`). The task text below has **not** been rewritten — changing the plan is its own decision — but these tasks rest on superseded assumptions. Check `0005` before starting any of them.

| Tasks | Assumes | Now |
|---|---|---|
| `T-THEME-01` … `T-THEME-10` (area "Ten reusable skins") | 10 skins, Quest first | 20 worlds with fixed DNA and six-axis kits (`../catalogue/`) |
| `T-DEFER-01`, `T-DEFER-02` | $4.99 single, $9.99/month | $5.99 per uncard, $9.99/month for two |
| `T-002`, `T-SCOPE-02`, `T-SCOPE-03`, `T-OPS-01` | An existing Lovable project, repo and backend to find or verify | T-002 answered: `JNabsRepo/uncard-starter` (`0001`). The other three are live — the repo now exists to verify |
| Tasks mentioning "child-friendly" / kids-first | Kids-first product | Whole family, kids through 60+; child-safety rules still apply |

## Rules for agents

- **This repo is the task list.** See `../decisions/0003-task-catalogue-source.md`.
- **Do not load the spreadsheet.** It costs ~118,000 tokens and needs Jordan's Drive. Everything useful from it is here.
- **Grep, don't read.** These are CSVs so you can pull one row. Loading a whole file should be a deliberate choice.
- **Owners are proposed, not accepted.** T-003 is the task that makes them real.
- **Statuses are stale by design** until the sync in ADR 0003 is running.
