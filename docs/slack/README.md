# Slack Archive

**Status:** Draft
**Updated:** 2026-10-07
**Owner:** Brian Lapp
**Method:** Every channel and DM in uncardapp.slack.com read through the claude.ai Slack connector on 2026-10-06 and 2026-10-07, including thread replies. Summarised by an agent, not reviewed by the team. Attachments were not opened, only listed.

## TL;DR

A running summary of the team Slack, so any partner's agent can catch up without reading the whole workspace. Start with `ledger.md` (decisions, open asks, who owes what). Read the month logs only for the story behind an item.

| File | What it holds |
|---|---|
| `ledger.md` | Current state: decisions made in Slack, open questions, action items, files waiting to be ingested, wiki follow-ups |
| `2026-09.md` | Day-by-day log, 21–30 Sep 2026 |
| `2026-10.md` | Day-by-day log, 1 Oct 2026 onward |

## This repo is public

Slack is private; this wiki is not. Summaries here keep to the work: what was decided, asked, shared or built. Leave out email addresses, account and folder IDs, credentials, personal and family details, and banter. Slack permalinks and file IDs are fine, since they only open for workspace members.

## Channels

| Channel | Used for | Last message read (ts) |
|---|---|---|
| #uncard-build | Build progress, infra asks, music research, team brain (0007) | `1791335969.732689` (2026-10-06 21:19) |
| #non-build-stuff | Research, brand and strategy files for filing | `1790988773.025529` (2026-10-02 20:52) |
| #all-tapcard | Announcements, ideas, tooling links | `1791226390.479279` (2026-10-05 14:53) |
| Group DM (Jordan, Brian, Tim) | Quick three-way chat | `1791335710.116989` (2026-10-06 21:15) |
| #social, #new-channel | Join messages only | — |
| 1:1 DMs | Nothing project-relevant beyond what's in the logs | — |

## Who's who

- **Jordan** ("Lord Jordan"), **Brian**, **Tim** ("Tim Biz") — equal partners.
- **Oy** — Jordan's ChatGPT agent. Posts appear as the ChatGPT bot, or as Jordan with "Sent using ChatGPT".
- **Claudius F'nMaximus** — Brian's Claude agent. Posts as Brian, signed off with that name.
- **Tim's Claude** — posts as Tim, starting with *[Claude, posting for Tim]*. Untagged posts are Tim himself.
- Jordan's build agents: Opus writes specs, Sonnet builds in Lovable, Codex handles account-level changes.

## How to update this archive

1. For each channel, read messages newer than its **Last message read** ts above (`slack_read_channel` with `oldest=<ts>`). Open any thread with new replies.
2. Add the new days to the current month's log (`YYYY-MM.md`, new file each month). One `##` heading per day, newest day at the bottom.
3. Update `ledger.md`: add decisions and asks, close the ones that got answered (strike through, with the date, don't delete).
4. Bump the ts values in the channel table and the `Updated` line on every file you touched, and the rows in `docs/index.md`.
5. If Slack contradicts a wiki doc, list it under **Wiki follow-ups** in the ledger, or fix the doc and mark the old line superseded (`conventions.md`).
