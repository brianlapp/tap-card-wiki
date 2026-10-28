# Slack Ledger

**Status:** Draft
**Updated:** 2026-10-28
**Owner:** Brian Lapp
**Method:** Pulled from the Slack logs in this folder (read through 2026-10-27). Agent summary, not reviewed by the team. Each line links back to the day in the month log. Closed items are struck through with the date, never deleted.

## TL;DR

New 2026-10-27: Group DM only, no decisions — Tim confirms his age is verified; Jordan says he'll add Tim as admin and give testing access that evening, and reports more bugs being worked through after an all-night debugging/audit pass on the 12-step creation flow.

Earlier, 2026-10-26: Group DM only, no decisions — live testing has started. Jordan walks Tim through getting set up as a tester (sign in, confirm age, send Jordan the email to approve) since the site is still invite-only; Jordan's fixing a newly found security bug, then says the first test pass is already turning up bugs (a card "built" with no way to view it); Tim's signed up and testing.

Earlier, 2026-10-25: Group DM only, no decisions — Jordan posts a build-progress update (final fix before turning the build on, Opus's time estimate down from ~10 build days to ~5, two bugs fixed, TY Growth Engine on its 8th build day); Tim replies to the 10-22 demo videos ("I think these are awesome").

Earlier, 2026-10-22: Group DM only, no decisions — Jordan shares three card-theme demo videos, excited about build quality and musing about a future "Choices" movie-trailer feature.

Earlier, 2026-10-21: Group DM only (no activity in the other channels or DMs). Jordan, at 86% of this week's Claude usage, has handed Devin/Manus's build findings to Opus/Astra for a fix spec that "6.1-Sol" has been implementing for ~16 hours, and hopes the team can start testing live uncard builds this weekend. He also floats outsourcing TikTok/Instagram content to pamba.app (~$150/mo) — Tim's open to a one-month trial — and, much further out, turning their own build process into a course once Uncard and Menu.ca are both running; nothing decided on either.

Earlier, 2026-10-20: Oy (for Jordan) DMs Brian asking him to file an updated combined SEO/AEO plan in the team brain as current and mark the 2 Oct SEO plan superseded — says Phase 3 is finished and Manus/Devin are now live-testing uncard.app (unverified here). Jordan also shares a screenshot of the Thank-You Growth Engine build still running past 5 days.

Earlier, 2026-10-19: Tim's Claude posts a social-growth research summary to #uncard-build (reaction videos, Songfinch comparison, videos-before-ads); Jordan likes it but redirects to asking for a content strategy for Uncard's own social accounts (TikTok, Facebook, Instagram) — what to post, what style; nothing decided. Badge-system feedback (Brian), the AI test budget D22 (Brian) and team-brain admin access (Jordan, Brian) are still open from 2026-10-06/12.

Earlier, 2026-10-14: Brian's agent set up and tested API keys for all four music services (Lyria, ElevenLabs, Mureka, ACE-Step), posted a cost-vs-scale report with samples to #all-tapcard, and passed the keys to Tim for human testing — the one-day music spike action item is now done.

Earlier, 2026-10-12: Tim's Claude posted a first badge-system draft (starter badges, teaching uncards, opt-in reminders) for Jordan and Brian's feedback; Jordan wants it built with the "Exo Skill" so it plugs into the full system and data lake. Tim also proposed a $25 cap for the first paid music test (D22) — Jordan voted yes, Brian's yes is still open.

Earlier, 2026-10-11/12: Phase 3 build has moved on to Stage 6 of 11, with Jordan expecting a commercial-grade, launch-ready site within a week to ten days; Jordan added Devin (a paid autonomous coding agent) alongside Codex and Claude to carry the build; Suno's API is still invite/partner-only with no written commercial terms, so Lyria/ElevenLabs/ACE-Step stay the pilot set. Jordan is also floating early product ideas ("selfcards", retro theme styles) — nothing decided.

Earlier, 2026-10-08: Jordan sent Stripe invitations to the team for the Uncard Stripe account; Codex is now running round the clock on Phase 3 (Stage 2 of 11); Oy posted a Growth Control Centre v0.2 design package (thank-you-page offers, acquisition tracking, experiments) to the Drive, which Jordan plans to build after his Claude usage resets Saturday.

Music is the live topic: Suno is out, Lyria/ElevenLabs/ACE-Step are on the table, and rights emails are ready to go. D16: uncard.gifts is the product repo's own Cloudflare Worker (`uncard-gifts`, built in Phase 2, not live yet), per the Phase 3 build spec Jordan approved 2026-10-05. Corrected 2026-10-07; it is not a second Lovable project. The seven research, brand and strategy files from the 2026-10-02 Slack drop are now ingested (2026-10-06; see `docs/index.md`); the growth-strategy PDF and investor deck stay held, private and out of this public wiki. New as of 2026-10-06: a shared "team brain" (private Supabase project + bulletin board) for all agents, decision `0007`, accepted by all three partners on 2026-10-07. Tim raised four open points on access, keys and private files.

## Decided in Slack

| Date | Decision | Who | Log |
|---|---|---|---|
| 2026-09-30 | Don't share uncard.app with anyone outside the team yet; a few more rounds of fixes first | Jordan | `2026-09.md` |
| 2026-09-30 | Golden Pass: unlimited, free for friends and family, separate from admin access | Jordan / Oy | `2026-09.md` |
| 2026-10-07 | uncard.gifts' Worker attaches **Custom Domains** (`uncard.gifts`, `www`), per `gifts/wrangler.jsonc` in the Phase 3 build. Corrected 2026-10-07; was (2026-10-02): a Worker route, not a Custom Domain, for the slice-1 placeholder | Jordan (Phase 3 spec) | `decisions/0006` |
| 2026-10-02 | Account-level Cloudflare changes go to Jordan as a ready-to-run Codex prompt | Jordan | `2026-10.md` |
| 2026-10-07 | **D16:** uncard.gifts is the Cloudflare Worker `uncard-gifts` (product repo `gifts/`, built in Phase 2, not yet LIVE), deployed by Workers Builds from a `workers-live` branch that moves only when Jordan publishes uncard.app. Per the Phase 3 build spec, approved by Jordan 2026-10-05, which takes precedence over the Domain, Tracking and SEO Plan. Corrected 2026-10-07; was (2026-10-06): a second Lovable project (W-48) | Jordan (Phase 3 spec) | `decisions/0006` |
| 2026-10-05 | Music must come from a cloud **API** the backend calls, not manual or home-PC generation; plan for 10 → 100,000+ users | Jordan | `2026-10.md` |
| 2026-10-05 | **Suno is out** (no public API; terms ban automation and redistribution). Udio out too (downloads disabled) | Tim, agreed by Jordan | `2026-10.md` |
| 2026-10-06 | Confirm commercial rights in writing before building on any music API | Tim | `2026-10.md` |
| 2026-10-07 | **Team brain** (decision `0007`) **accepted** by all three partners at the 2026-10-07 partner meeting: a private Supabase project plus a bulletin board every partner's agent connects to, holding the wiki, shared files, Slack history and decisions. Tim first agreed in Slack 2026-10-06, as a trial with a check-in in ~1 month | All three (Brian proposed) | `2026-10.md` |

## Open questions

| Since | Question | Waiting on | Log |
|---|---|---|---|
| ~~2026-10-02~~ | ~~uncard.gifts plan, `decisions/0006` (D16): any objections before slices 2–4?~~ — closed 2026-10-06: Brian chose Jordan's newer plan (uncard.gifts on a second Lovable project); 0006 superseded | Brian | `2026-10.md` |
| 2026-10-05 | Free procedural sounds plus paid sung songs (S37) as an upsell — adopt? | All three | `2026-10.md` |
| 2026-10-05 | AI budget (D22), needed before any paid music pilot. **2026-10-12:** Tim proposed a $25 cap for the first test (5 prompts × 3 tries, est. $5–$12); Jordan voted yes; Brian's yes still open | Brian | `2026-10.md` |
| 2026-10-12 | Badge-system first draft (5 starter badges, 3 teaching uncards, opt-in reminders) — Jordan gave feedback (go further, use the "Exo Skill"); Brian's feedback still open | Brian | `2026-10.md` |
| 2026-10-05 | Legal review of delivering generated songs to givers and recipients | All three | `2026-10.md` |
| 2026-10-06 | **Cost per song** (Jordan). Tim's per-card figures are for one accepted song at 3 attempts, so per *attempt* that's about $0.04–0.13 ACE-Step, $0.08 Lyria, $0.19 ElevenLabs (derived here, unverified) | Tim's report | `2026-10.md` |
| 2026-10-06 | Song lengths: which lengths, for which uses? Jordan wants variety, including short ones. Spike finding: Lyria 3.5 ignores requested length (15 s asked, 145 s back); Lyria 3 Clip is always about 30 s | All three | `2026-10.md` |
| 2026-10-06 | **Google's Gemini API terms bar apps "directed towards or likely to be accessed by individuals under the age of 18".** Kids receive uncards. Does Lyria through Vertex AI (Google Cloud terms) avoid this? Needs a legal read before building on Lyria | All three | music spike |
| 2026-09-29 | Free-uncard-for-signup plus birthday-card loop (Jordan's idea; Oy's plan item 4). Rules are D18–D19 in the product repo | All three | `2026-09.md` |
| 2026-10-02 | customer.io: Jordan's suggestion for the email provider (D25)? Only a bare link so far | Jordan | `2026-10.md` |
| ~~2026-10-08~~ | ~~Tim asked whether some financial material was meant to go in the group DM~~ — answered 2026-10-08: Jordan confirmed it should have gone there | Brian | `2026-10.md` |
| 2026-10-06 | Team brain: should all three partners get admin access to the Supabase project and a data-export path, not just Brian's account? What happens if the free plan pauses or hits its limits? Jordan is pushing back on full admin access for everyone until there's a clear dev/production system. **Export part done 2026-10-07:** a weekly copy of the brain now lands in the shared Uncard Drive folder (brain-backups); admin access still open | Jordan, Brian | `2026-10.md` |
| ~~2026-10-06~~ | ~~Team brain: when are agent keys rotated, and does a key pasted into a connector stay valid after its 1Password link expires?~~ — answered 2026-10-07 in Tim's Slack thread: keys change if one leaks or someone leaves; an expired 1Password link doesn't break a key already in a connector | Brian | `2026-10.md` |
| ~~2026-10-06~~ | ~~Team brain: a list of which private files (investor deck, growth strategy) are now ingested and searchable by all four agents, including ChatGPT and Codex (so via OpenAI too)~~ — answered 2026-10-07 in Tim's Slack thread: investor deck, growth strategy, brand guide, brand system, domain/tracking/SEO plan, and four research docs | Brian | `2026-10.md` |
| 2026-10-19 | Content strategy for Uncard's own social accounts (TikTok, Facebook, Instagram) — what to post, what style? Jordan asked the team in reply to Tim's social-growth research | All three | `2026-10.md` |
| 2026-10-08 | **Business bank account and incorporation: Venn or Float?** Jordan raised both (partners' chat, 8 Oct). Brian chooses **Venn** (2026-10-08): it incorporates and opens the account in one go for about $49 net, and its free plan pays 1% cashback on the first $5k a month (Float only pays above $25k a month). Tim is fine with either if they're legit (both checked: notice board post 15). Before filing: a short accountant call on personal holding companies and a shareholders' agreement | Jordan to confirm | `2026-10.md` |
| ~~2026-10-06~~ | ~~Team brain: keep automated Slack syncing via a Slack app as its own separate decision~~ — answered 2026-10-07 in Tim's Slack thread: agreed, a Slack app stays a separate decision; meanwhile the brain's copy of Slack refreshes every morning from Brian's Mac | All three | `2026-10.md` |

## Action items

| Since | Item | Owner | Log |
|---|---|---|---|
| 2026-10-20 | File the updated combined SEO/AEO plan (sent by Oy, Word doc) in the team brain as current; mark the 2026-10-02 SEO plan and `strategy/domain-tracking-seo.md` superseded with links to it; report back the canonical location | Brian | `2026-10.md` |
| ~~2026-10-05~~ | ~~One-day music spike: the same 5 prompts through Lyria, ElevenLabs, ACE-Step and Mureka.~~ Day 1 done 2026-10-06: Lyria 3.5 ran (94–97% of our words sung, $0.08 a song, but no line timing, no length control, filter blocked two kids' songs until reworded). Brian posted a cost breakdown and song samples 2026-10-06. **Done 2026-10-14:** Mureka, ACE-Step and ElevenLabs accounts set up, keys tested, cost-vs-scale report posted to #all-tapcard, keys passed to Tim for human testing | Brian | `2026-10.md` |
| 2026-10-06 | Send the rights-confirmation emails to Google (Lyria) and ElevenLabs | Tim | `2026-10.md` |
| 2026-10-05 | Share the music research artifact with Jordan and Brian (it's private) | Tim | `2026-10.md` |
| 2026-10-05 | Opus review of the music research | Jordan | `2026-10.md` |
| 2026-10-02 | File the 2026-10-02 research, brand and strategy files in the shared Drive (Oy never did) | Jordan | `2026-10.md` |
| 2026-09-30 | Post the full testing and learning plan document once storage is agreed | Jordan / Oy | `2026-09.md` |
| ~~2026-10-02~~ | ~~Create the `uncard-gifts` Worker and give Brian Editor on it~~ — done 2026-10-02 | Jordan (Codex) | `2026-10.md` |
| ~~2026-10-02~~ | ~~uncard.gifts slice 1: route to the placeholder 404~~ — done 2026-10-02 | Brian | `2026-10.md` |
| ~~2026-10-07~~ | ~~Remove the slice-1 placeholder (route `uncard.gifts/*` and its proxied DNS record) before Jordan's Cloudflare steps attach the Phase 2 `uncard-gifts` Worker's Custom Domains~~ — done 2026-10-07: route and DNS record deleted, uncard.gifts now has no records or routes | Brian | `decisions/0006` |
| ~~2026-10-09~~ | ~~Research Suno's official REST API: access, pricing, commercial terms, whether it's the same access reported for Grok's bot, and whether Lovable has a native connector~~ — done 2026-10-10: still invite/partner-only, no written commercial terms, no Lovable native connector; Lyria/ElevenLabs/ACE-Step stay the pilot set, Suno stays a quality reference only | Tim | `2026-10.md` |

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
- `decisions/0006`: superseded by the Phase 3 build spec (corrected 2026-10-07). Slice 1's placeholder was removed on 2026-10-07, so uncard.gifts is clear for the real Worker.
- **2026-10-06:** the seven 2026-10-02 research/brand/strategy files ingested into `docs/research/`, `docs/brand/brand-guide.md` and `docs/strategy/domain-tracking-seo.md` (see `index.md`). The SEO plan PDF itself claims "Jordan adopted this plan on 2 October 2026" and that it settles D16 (a separate uncard.gifts host) — but `decisions/0006` is still `Status: Open` and this ledger's own open-questions table above shows no partner replies. It also assumes uncard.gifts runs as a second Lovable project (W-48), where `decisions/0006` chose a Cloudflare Worker instead. Neither conflict is resolved here — see `strategy/domain-tracking-seo.md`'s Open questions. **Resolved 2026-10-07:** the Phase 3 build spec (approved 2026-10-05) supersedes both; see `decisions/0006`.
- **2026-10-20:** Oy's DM to Brian reports, via Jordan, that Phase 3 is finished and Manus/Devin are now running live tests on uncard.app. Unverified here (secondhand, via Slack DM, no direct confirmation from Jordan in a channel) — flagging rather than updating `product/live-product.md` on this alone.
