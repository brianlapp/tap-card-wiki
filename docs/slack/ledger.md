# Slack Ledger

**Status:** Draft
**Updated:** 2026-10-06
**Owner:** Brian Lapp
**Method:** Pulled from the Slack logs in this folder (read 2026-10-06). Agent summary, not reviewed by the team. Each line links back to the day in the month log. Closed items are struck through with the date, never deleted.

## TL;DR

Music is the live topic: Suno is out, Lyria/ElevenLabs/ACE-Step are on the table, and rights emails are ready to go. uncard.gifts slice 1 is done, and the plan (0006) is waiting on partner input. Eight research and brand files (nine with the SEO plan) are still waiting to be filed and ingested.

## Decided in Slack

| Date | Decision | Who | Log |
|---|---|---|---|
| 2026-09-30 | Don't share uncard.app with anyone outside the team yet; a few more rounds of fixes first | Jordan | `2026-09.md` |
| 2026-09-30 | Golden Pass: unlimited, free for friends and family, separate from admin access | Jordan / Oy | `2026-09.md` |
| 2026-10-02 | uncard.gifts runs on a Worker **route**, not a Custom Domain | Brian's agent, Oy | `2026-10.md` |
| 2026-10-02 | Account-level Cloudflare changes go to Jordan as a ready-to-run Codex prompt | Jordan | `2026-10.md` |
| 2026-10-05 | Music must come from a cloud **API** the backend calls, not manual or home-PC generation; plan for 10 → 100,000+ users | Jordan | `2026-10.md` |
| 2026-10-05 | **Suno is out** (no public API; terms ban automation and redistribution). Udio out too (downloads disabled) | Tim, agreed by Jordan | `2026-10.md` |
| 2026-10-06 | Confirm commercial rights in writing before building on any music API | Tim | `2026-10.md` |

## Open questions

| Since | Question | Waiting on | Log |
|---|---|---|---|
| 2026-10-02 | uncard.gifts plan, `decisions/0006` (D16): any objections before slices 2–4? No replies in Slack yet | Jordan, Tim | `2026-10.md` |
| 2026-10-05 | Free procedural sounds plus paid sung songs (S37) as an upsell — adopt? | All three | `2026-10.md` |
| 2026-10-05 | AI budget (D22), needed before any paid music pilot | All three | `2026-10.md` |
| 2026-10-05 | Legal review of delivering generated songs to givers and recipients | All three | `2026-10.md` |
| 2026-10-06 | **Cost per song** (Jordan). Tim's per-card figures are for one accepted song at 3 attempts, so per *attempt* that's about $0.04–0.13 ACE-Step, $0.08 Lyria, $0.19 ElevenLabs (derived here, unverified) | Tim's report | `2026-10.md` |
| 2026-10-06 | Song lengths: which lengths, for which uses? Jordan wants variety, including short ones | All three | `2026-10.md` |
| 2026-09-29 | Free-uncard-for-signup plus birthday-card loop (Jordan's idea; Oy's plan item 4). Rules are D18–D19 in the product repo | All three | `2026-09.md` |
| 2026-10-02 | customer.io: Jordan's suggestion for the email provider (D25)? Only a bare link so far | Jordan | `2026-10.md` |

## Action items

| Since | Item | Owner | Log |
|---|---|---|---|
| 2026-10-05 | One-day music spike: the same 5 prompts through Lyria, ElevenLabs and ACE-Step | Brian | `2026-10.md` |
| 2026-10-06 | Send the rights-confirmation emails to Google (Lyria) and ElevenLabs | Tim | `2026-10.md` |
| 2026-10-05 | Share the music research artifact with Jordan and Brian (it's private) | Tim | `2026-10.md` |
| 2026-10-05 | Opus review of the music research | Jordan | `2026-10.md` |
| 2026-10-02 | File the 2026-10-02 research, brand and strategy files in the shared Drive (Oy never did) | Jordan | `2026-10.md` |
| 2026-09-30 | Post the full testing and learning plan document once storage is agreed | Jordan / Oy | `2026-09.md` |
| ~~2026-10-02~~ | ~~Create the `uncard-gifts` Worker and give Brian Editor on it~~ — done 2026-10-02 | Jordan (Codex) | `2026-10.md` |
| ~~2026-10-02~~ | ~~uncard.gifts slice 1: route to the placeholder 404~~ — done 2026-10-02 | Brian | `2026-10.md` |

## Waiting to be ingested

Posted in Slack, not yet in the Drive or this wiki. The Drive folder is where originals belong. Slack still holds copies (#non-build-stuff); file IDs below, readable with `slack_read_file`.

| File | Posted | Slack file ID |
|---|---|---|
| Making an Uncard Feel Like a Joy: Research-Backed Creation Flow, Landing to Paid (.md) | 2026-10-02 | `F0C6CGA9W1F` |
| Uncard Checkout Research: How to Get Givers to Pay on a Phone, on the Day (.md) | 2026-10-02 | `F0C6594SY5T` |
| Sharing and Referral Loop Design, Incentives and Measurement, October 2026 (.md) | 2026-10-02 | `F0C751G8NNL` |
| Holding the Recipient's Attention: Research Findings, Generator Rules and Metrics (.md) | 2026-10-02 | `F0C751HS9GQ` |
| Uncard growth strategy (.pdf) | 2026-10-02 | `F0C74UW6GFJ` |
| UNCARD investor deck (.pdf) | 2026-10-02 | `F0C6CGAKC2V` |
| UNCARD brand guide (.pdf) | 2026-10-02 | `F0C6594QXEH` |
| UNCARD brand system (.zip) | 2026-10-02 | `F0C68KBKKQW` |
| uncard Domain, Tracking and SEO Plan (.pdf) — **new, not in `index.md` before today** | 2026-10-02 | `F0C69E3DNKX` |
| Testing and learning plan (Oy) | 2026-09-30 | not posted yet |
| Music-generation research (Tim's Claude) | 2026-10-05 | private Claude artifact, not in Slack |

## Wiki follow-ups

Places where Slack is newer than the wiki.

- `product/scope.md` said "Suno for songs — manual pilot". Superseded 2026-10-05 (marked in that doc).
- `index.md`'s "Waiting to be ingested" table was missing the Domain, Tracking and SEO Plan PDF. Added 2026-10-06.
- `decisions/0006`: slice 1 is recorded there. Partner feedback still needed before it can move from Open to Accepted.
