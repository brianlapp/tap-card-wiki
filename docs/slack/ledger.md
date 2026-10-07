# Slack Ledger

**Status:** Draft
**Updated:** 2026-10-07
**Owner:** Brian Lapp
**Method:** Pulled from the Slack logs in this folder (read through 2026-10-07). Agent summary, not reviewed by the team. Each line links back to the day in the month log. Closed items are struck through with the date, never deleted.

## TL;DR

Music is the live topic: Suno is out, Lyria/ElevenLabs/ACE-Step are on the table, and rights emails are ready to go. D16 is settled: uncard.gifts goes on a second Lovable project per Jordan's plan (0006 superseded, 2026-10-06). The seven research, brand and strategy files from the 2026-10-02 Slack drop are now ingested (2026-10-06; see `docs/index.md`); the growth-strategy PDF and investor deck stay held, private and out of this public wiki. New as of 2026-10-06: a shared "team brain" (private Supabase project + bulletin board) for all agents, decision `0007` — Tim's agent agreed to a trial, Jordan's agreement still pending, and Tim raised four open points on access, keys and private files.

## Decided in Slack

| Date | Decision | Who | Log |
|---|---|---|---|
| 2026-09-30 | Don't share uncard.app with anyone outside the team yet; a few more rounds of fixes first | Jordan | `2026-09.md` |
| 2026-09-30 | Golden Pass: unlimited, free for friends and family, separate from admin access | Jordan / Oy | `2026-09.md` |
| 2026-10-02 | uncard.gifts runs on a Worker **route**, not a Custom Domain | Brian's agent, Oy | `2026-10.md` |
| 2026-10-02 | Account-level Cloudflare changes go to Jordan as a ready-to-run Codex prompt | Jordan | `2026-10.md` |
| 2026-10-06 | **D16 settled:** gifts live on uncard.gifts as a second Lovable project (W-48), per Jordan's Domain, Tracking and SEO Plan; `decisions/0006` (Worker) superseded | Brian, choosing Jordan's plan | `strategy/domain-tracking-seo.md` |
| 2026-10-05 | Music must come from a cloud **API** the backend calls, not manual or home-PC generation; plan for 10 → 100,000+ users | Jordan | `2026-10.md` |
| 2026-10-05 | **Suno is out** (no public API; terms ban automation and redistribution). Udio out too (downloads disabled) | Tim, agreed by Jordan | `2026-10.md` |
| 2026-10-06 | Confirm commercial rights in writing before building on any music API | Tim | `2026-10.md` |
| 2026-10-06 | **Team brain** (decision `0007`): a private Supabase project plus a bulletin board every partner's agent connects to, holding the wiki, shared files, Slack history and decisions. Trial, check-in in ~1 month. Tim's agent agreed; Jordan's agreement still needed | Brian proposed, Tim agreed | `2026-10.md` |

## Open questions

| Since | Question | Waiting on | Log |
|---|---|---|---|
| ~~2026-10-02~~ | ~~uncard.gifts plan, `decisions/0006` (D16): any objections before slices 2–4?~~ — closed 2026-10-06: Brian chose Jordan's newer plan (uncard.gifts on a second Lovable project); 0006 superseded | Brian | `2026-10.md` |
| 2026-10-05 | Free procedural sounds plus paid sung songs (S37) as an upsell — adopt? | All three | `2026-10.md` |
| 2026-10-05 | AI budget (D22), needed before any paid music pilot | All three | `2026-10.md` |
| 2026-10-05 | Legal review of delivering generated songs to givers and recipients | All three | `2026-10.md` |
| 2026-10-06 | **Cost per song** (Jordan). Tim's per-card figures are for one accepted song at 3 attempts, so per *attempt* that's about $0.04–0.13 ACE-Step, $0.08 Lyria, $0.19 ElevenLabs (derived here, unverified) | Tim's report | `2026-10.md` |
| 2026-10-06 | Song lengths: which lengths, for which uses? Jordan wants variety, including short ones. Spike finding: Lyria 3.5 ignores requested length (15 s asked, 145 s back); Lyria 3 Clip is always about 30 s | All three | `2026-10.md` |
| 2026-10-06 | **Google's Gemini API terms bar apps "directed towards or likely to be accessed by individuals under the age of 18".** Kids receive uncards. Does Lyria through Vertex AI (Google Cloud terms) avoid this? Needs a legal read before building on Lyria | All three | music spike |
| 2026-09-29 | Free-uncard-for-signup plus birthday-card loop (Jordan's idea; Oy's plan item 4). Rules are D18–D19 in the product repo | All three | `2026-09.md` |
| 2026-10-02 | customer.io: Jordan's suggestion for the email provider (D25)? Only a bare link so far | Jordan | `2026-10.md` |
| 2026-10-06 | Team brain: should all three partners get admin access to the Supabase project and a data-export path, not just Brian's account? What happens if the free plan pauses or hits its limits? Jordan is pushing back on full admin access for everyone until there's a clear dev/production system | Jordan, Brian | `2026-10.md` |
| 2026-10-06 | Team brain: when are agent keys rotated, and does a key pasted into a connector stay valid after its 1Password link expires? | Brian | `2026-10.md` |
| 2026-10-06 | Team brain: a list of which private files (investor deck, growth strategy) are now ingested and searchable by all four agents, including ChatGPT and Codex (so via OpenAI too) | Brian | `2026-10.md` |
| 2026-10-06 | Team brain: keep automated Slack syncing via a Slack app as its own separate decision | All three | `2026-10.md` |

## Action items

| Since | Item | Owner | Log |
|---|---|---|---|
| 2026-10-05 | One-day music spike: the same 5 prompts through Lyria, ElevenLabs, ACE-Step and Mureka. **Day 1 done 2026-10-06:** Lyria 3.5 ran (94–97% of our words sung, $0.08 a song, but no line timing, no length control, filter blocked two kids' songs until reworded). Brian posted a cost breakdown and song samples 2026-10-06. Mureka, ACE-Step and ElevenLabs wait on accounts (Mureka $10 top-up, free Hugging Face token, ElevenLabs $6/mo) | Brian | `2026-10.md` |
| 2026-10-06 | Send the rights-confirmation emails to Google (Lyria) and ElevenLabs | Tim | `2026-10.md` |
| 2026-10-05 | Share the music research artifact with Jordan and Brian (it's private) | Tim | `2026-10.md` |
| 2026-10-05 | Opus review of the music research | Jordan | `2026-10.md` |
| 2026-10-02 | File the 2026-10-02 research, brand and strategy files in the shared Drive (Oy never did) | Jordan | `2026-10.md` |
| 2026-09-30 | Post the full testing and learning plan document once storage is agreed | Jordan / Oy | `2026-09.md` |
| ~~2026-10-02~~ | ~~Create the `uncard-gifts` Worker and give Brian Editor on it~~ — done 2026-10-02 | Jordan (Codex) | `2026-10.md` |
| ~~2026-10-02~~ | ~~uncard.gifts slice 1: route to the placeholder 404~~ — done 2026-10-02 | Brian | `2026-10.md` |
| 2026-10-06 | Delete the `uncard.gifts/*` Worker route once the second Lovable project connects uncard.gifts | Brian | `decisions/0006` |

## Waiting to be ingested

Posted in Slack, not yet in the Drive or this wiki. The Drive folder is where originals belong. Slack still holds copies (#non-build-stuff); file IDs below, readable with `slack_read_file`.

| File | Posted | Slack file ID | Status |
|---|---|---|---|
| ~~Making an Uncard Feel Like a Joy: Research-Backed Creation Flow, Landing to Paid (.md)~~ | 2026-10-02 | `F0C6CGA9W1F` | Ingested 2026-10-06 → `research/creation-flow.md` |
| ~~Uncard Checkout Research: How to Get Givers to Pay on a Phone, on the Day (.md)~~ | 2026-10-02 | `F0C6594SY5T` | Ingested 2026-10-06 → `research/checkout.md` |
| ~~Sharing and Referral Loop Design, Incentives and Measurement, October 2026 (.md)~~ | 2026-10-02 | `F0C751G8NNL` | Ingested 2026-10-06 → `research/sharing-referral-loop.md` |
| ~~Holding the Recipient's Attention: Research Findings, Generator Rules and Metrics (.md)~~ | 2026-10-02 | `F0C751HS9GQ` | Ingested 2026-10-06 → `research/recipient-attention.md` |
| Uncard growth strategy (.pdf) | 2026-10-02 | `F0C74UW6GFJ` | **Held: private, not for the public wiki** |
| UNCARD investor deck (.pdf) | 2026-10-02 | `F0C6CGAKC2V` | **Held: private, not for the public wiki** |
| ~~UNCARD brand guide (.pdf)~~ | 2026-10-02 | `F0C6594QXEH` | Ingested 2026-10-06 → `brand/brand-guide.md` |
| ~~UNCARD brand system (.zip)~~ | 2026-10-02 | `F0C68KBKKQW` | Ingested 2026-10-06 → `brand/brand-guide.md` + `brand/system/` |
| ~~uncard Domain, Tracking and SEO Plan (.pdf)~~ | 2026-10-02 | `F0C69E3DNKX` | Ingested 2026-10-06 → `strategy/domain-tracking-seo.md` |
| Testing and learning plan (Oy) | 2026-09-30 | not posted yet | Not ingested |
| Music-generation research (Tim's Claude) | 2026-10-05 | private Claude artifact, not in Slack | Not ingested |

## Wiki follow-ups

Places where Slack is newer than the wiki.

- `product/scope.md` said "Suno for songs — manual pilot". Superseded 2026-10-05 (marked in that doc).
- `index.md`'s "Waiting to be ingested" table was missing the Domain, Tracking and SEO Plan PDF. Added 2026-10-06.
- `decisions/0006`: slice 1 is recorded there. Partner feedback still needed before it can move from Open to Accepted.
- **2026-10-06:** the seven 2026-10-02 research/brand/strategy files ingested into `docs/research/`, `docs/brand/brand-guide.md` and `docs/strategy/domain-tracking-seo.md` (see `index.md`). The SEO plan PDF itself claims "Jordan adopted this plan on 2 October 2026" and that it settles D16 (a separate uncard.gifts host) — but `decisions/0006` is still `Status: Open` and this ledger's own open-questions table above shows no partner replies. It also assumes uncard.gifts runs as a second Lovable project (W-48), where `decisions/0006` chose a Cloudflare Worker instead. Neither conflict is resolved here — see `strategy/domain-tracking-seo.md`'s Open questions.
