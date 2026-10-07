# Domain, Tracking and SEO Plan

**Status:** Draft
**Updated:** 2026-10-06
**Owner:** Jordan
**Method:** Extracted with `pdftotext` from `uncard Domain, Tracking and SEO Plan.pdf` (dated Oct 2, 2026, "adopted" per its own text by Jordan that day), posted by Jordan in Slack #non-build-stuff on 2026-10-02, then reformatted as markdown. Converted as written; the plan's own claims (including that it was "adopted") were not re-verified against Slack or the partners here — see Open questions.

## TL;DR

- **Cards live on uncard.gifts** with no third-party tracking and no search indexing. **Everything public and commercial lives on uncard.app** with full tracking (GA4, ad pixels, Search Console).
- Three routes connect the two domains without tracking recipients: a GA4 event on the giver's Send step (uncard.app), preview-bot fetch logging by platform (uncard.gifts server), and a tagged end-card "Make one" link that carries the occasion and theme but never the card's address, a name or message words.
- Cards get their own **aggregate, cookieless open/finish/theme counter** — never shown to the giver, no third-party scripts.
- Search and AI-answer visibility is meant to come from pages on uncard.app built to rank (occasion/person/interest pages, comparison pages, free tools, an opt-in gallery) — "shared card links pass almost no search value."
- The plan states it **settles D16** (serve gifts from a separate uncard.gifts host) and keeps D12 (no recipient tracking). It lists eight new work items as a result.

## Implication for Uncard

- **Resolved 2026-10-06 (Brian):** Jordan's plan is the newer one, so it wins (`decisions/0005`, newest wins). D16 is settled as this plan describes: a separate uncard.gifts host on a second Lovable project (W-48). `decisions/0006` is marked superseded. The two conflict notes below are kept for the record.
- **This plan and `decisions/0006` don't agree on the gift host's infrastructure.** Both are dated 2026-10-02. This plan's "Trade-offs we accept" section says uncard.gifts "needs its own project (W-48)" because "Lovable redirects extra domains to the main one" — i.e. a second Lovable project. `decisions/0006-gifts-on-uncard-gifts.md` (also 2026-10-02, proposed by Brian) explicitly chose a Cloudflare Worker instead, and says that Worker "replaces W-48's second Lovable project." Same destination domain, two different builds. See Open questions — this needs a partner conversation, not a silent edit to either doc.
- **This plan says D16 is already settled; the wiki still shows it open.** The plan states "Jordan adopted this plan on 2 October 2026" and that it "Settled" D16 as "option D, a separate uncard.gifts host, before public launch or paid ads." But `decisions/0006` is still `Status: Open`, and `slack/ledger.md`'s open-questions table lists D16 as waiting on Jordan and Tim with "no replies in Slack yet" as of today. If D16 really is decided, the wiki is stale and should be updated by whoever confirms it with Jordan directly — not assumed here.
- **The "own counter" idea matches the privacy gate, and is less granular than what the research docs propose.** "Aggregate, cookieless, never shown to the giver" for card opens/finishes is consistent with `AGENTS.md`'s privacy gate and `decisions/0006`. The two research docs ingested alongside this one (`research/recipient-attention.md`, `research/sharing-referral-loop.md`) propose considerably more granular event schemas (per-scene dwell time, device class, time-to-open) for the same uncard.gifts surface — see those docs' Open questions for the same unresolved tension, which this plan doesn't settle either.
- **Full tracking on uncard.app narrows, rather than reverses, the "no PII in telemetry" rule — but needs the same legal pass the plan itself calls for.** `AGENTS.md`'s privacy gate and `product/scope.md`'s "Analytics: first-party event pipeline, schema-validated, no PII" describe the product generally. This plan scopes GA4/ad pixels to the commerce domain only, which is a reasonable narrowing, but a live GA4 implementation near checkout will see purchaser PII (email, name) in practice — exactly the kind of thing the plan's own open legal question (below) should cover.
- **Cites both just-ingested research docs as sources** ("uncard Sharing and Referral Loop research," "Uncard: Holding the Recipient's Attention research"), confirming Jordan was already drawing on them when this plan was written.

## The plan

### Background

The earlier plan sent cards from uncard.gifts, kept them out of Google, and ran GA4 on uncard.app only. Jordan asked whether that gives up backlinks, traffic and data on where people share. He proposed hosting every card on uncard.app, with GA4 on every page and stronger privacy added later as an option. That alternative was tested against three questions — does a shared card link help SEO, would GA4 on a card show where people share, and what would tracking or indexing cards cost — and rejected (see "Alternative considered" below). The plan keeps the two-domain split, but changes its purpose from a privacy-only measure to a growth-and-risk decision as well.

### Eight decisions

| # | Decision | Reason |
|---|---|---|
| 1 | Cards are served from uncard.gifts. Commerce, marketing and public pages are served from uncard.app. | If someone misuses a card for spam or scams, blocklists hit uncard.gifts, not the checkout and ad landing pages. |
| 2 | uncard.app carries full tracking: GA4, ad pixels, Search Console and testing tools. | Buyers are on uncard.app. With cards on another domain, no marketing script can leak onto a card. |
| 3 | Cards carry no third-party scripts and are kept out of search (`noindex`). | Cards hold names, photos and children's birthdays. Tracking them creates legal risk, and nobody searches for someone else's card. |
| 4 | Cards report opens, finishes and themes through an own counter: aggregate, cookieless, never shown to the giver. | Learn what delights people without sending anyone's data to Google. Ad blockers don't block the product's own counts. |
| 5 | Log the preview bots that fetch each card link. | WhatsApp, Facebook, Slack and others fetch a link to draw its preview. That shows where cards travel, without tracking a person. |
| 6 | Every card ends with a "Make one" link to uncard.app, tagged with occasion and theme. | Turns recipients into buyers, and shows which occasions and themes bring new customers. |
| 7 | Public sharing goes through a teaser page on uncard.app, never the card itself. | Facebook and Instagram clicks land on the store, fully tracked, while the private card stays private. |
| 8 | SEO comes from pages built to rank: example pages, comparisons and free tools. | Shared card links pass almost no search value. These pages earn links, and AI tools cite them. |

**How the two domains connect:** the giver's link opens on uncard.gifts. Every route out of a card lands on uncard.app, where tracking runs (three routes: the Send-step GA4 event, preview-bot logging, and the end-card "Make one" link).

### What we measure and how

| Question | Where | How |
|---|---|---|
| Which channel do givers send through: text, WhatsApp, email or copy? | uncard.app | GA4 event on the Send step |
| Which platforms does a card travel to, including forwards? | uncard.gifts server | Preview-bot fetches, counted by platform |
| Do recipients open and finish, and which scenes and themes land? | uncard.gifts | Own aggregate counter (W-30) |
| Where do recipients share publicly? | Teaser page on uncard.app | Per-channel share buttons, tags and referrer |
| Which occasions and themes bring new givers? | uncard.app | Tags on the end-card "Make one" link |
| What do new visitors do before they buy? | uncard.app | GA4 funnel and ad pixels |

The end-card link uses one tag scheme: `uncard.app/?utm_source=uncard&utm_medium=card_end&utm_campaign=<occasion>&utm_content=<theme>`. A tag never holds a card's address, a name or any message words, because the address alone opens the card.

Three build details follow from this: messaging apps send no referrer, so GA4 would file those visits as "Direct" and can't answer the "which platform" question on its own; the phone's share sheet doesn't say which app was picked, so explicit share buttons should come before a generic "More"; and iMessage's preview fetcher borrows Facebook's and Twitter's names, so it needs its own fingerprint to be counted separately.

### SEO and AI-answer plan

Search and AI visibility ("AI answers" = ChatGPT, Perplexity, Google AI Overviews) are meant to come from pages on uncard.app built to rank, never from private cards.

| Page type | Example | Why it works |
|---|---|---|
| Occasion, person and interest pages | "Interactive birthday card for a dad who golfs" | Matches what people search, and shows a real demo uncard. Each must be genuinely useful, not templated filler. |
| Comparison pages | uncard compared with Jacquie Lawson, Punchbowl, Kudoboard and Paperless Post | Reaches people already shopping for a digital card. |
| Free tools | "What to write in a birthday card" | Earns real backlinks, which social shares mostly don't. |
| Opt-in gallery | Featured uncards, with both giver and recipient agreeing | Real examples that can be indexed with consent. |

For AI answers specifically: marketing pages render server-side with clear pricing and an FAQ; AI crawlers are allowed on uncard.app and blocked on uncard.gifts; the plan calls for seeking mentions on Reddit and in "best digital card" roundups, which AI tools lean on; and the uncard.gifts home page permanently redirects (301) to uncard.app so stray links count for the main site.

### Alternative considered

Hosting every card on uncard.app, with GA4 on every page and cards open to search, was rejected for six reasons:

1. **Little SEO gain.** Links in texts, iMessage, WhatsApp and email are invisible to Google; Facebook, Instagram, X and TikTok links are mostly nofollow and behind logins.
2. **Little sharing data gained.** Messaging apps send no referrer, so GA4 would file most card visits as "Direct." Ad blockers and Safari's cookie limits drop a share of the rest.
3. **The address is the key.** By default GA4 sends each page's full address and title. Every card link, and titles like "Happy 7th, Emma," would reach Google and anyone with GA access — and Google's terms bar sending personal information.
4. **Children and consent.** COPPA treats cookies as personal information; plain analytics can fit its "internal operations" exception but retargeting can't. Quebec requires tracking off by default. EU and UK recipients would need to consent before GA cookies, which would put a consent banner on a card's first screen.
5. **Indexing harms people.** It would put pages about people who never signed up into Google. Indexing thousands of AI-generated pages to win traffic is close to what Google's scaled-content spam policy targets.
6. **The poster isn't the only person in the card.** The person posting on Facebook is often not the recipient, contributors never agreed, and most sharing happens in private texts. Adding privacy later leaves the first users exposed, and removing pages from Google is slow.

### Trade-offs accepted

- **No ad retargeting of recipients.** Retarget people who click "Make one" instead — they land on uncard.app and are the people most ready to buy.
- **A second deployment to run.** "Lovable redirects extra domains to the main one, so uncard.gifts needs its own project (W-48). The two must be kept in step." *(See Open questions below — this is the point where this plan and `decisions/0006` diverge.)*
- **No per-person detail on cards.** Counts by card, occasion and theme, not individual journeys. Givers see no "opened" or "finished" status, as D12 already requires.

One question the plan itself leaves open: counsel should confirm that aggregate, cookieless card counts need no consent in Canada, the US, the EU and the UK.

### Timing and rollout

Cards stay on uncard.app/c, with Lovable's visitor analytics off, until uncard.gifts is built and verified. The move happens before public launch or any paid ads. GA4 starts on uncard.app only after the cards have moved, unless a check first proves it never loads on a card page. Old uncard.app/c links redirect to uncard.gifts, so cards already sent keep working. (The plan describes this as "3 phases, 2 gates" but doesn't spell out the phase boundaries beyond this paragraph.)

### Changes to existing decisions and work items

This plan settles D16, keeps D12, and adds eight items of new work.

| Item | Change |
|---|---|
| D16 | Settled (per this plan): option D, a separate uncard.gifts host, before public launch or paid ads. Option A (Lovable visitor analytics off) stays in force until then. |
| D12 | Kept: no recipient tracking and no third-party scripts on cards. Aggregate, cookieless counts per card are allowed and are never shown to the giver. |
| W-37 | Kept as the gate on real gifts. The same check is repeated on uncard.gifts once it is live. |
| W-48 | Moves from conditional to approved (per this plan). The recorded reason is risk isolation and freedom to track uncard.app. |
| W-47 | Unchanged: cards stay `noindex`, with no analytics. |

**New work listed:**
- End-card "Make one" link with the tag scheme
- Preview-bot logging on card links, counted by platform
- Channel events on the giver's Send step in uncard.app
- Teaser share page on uncard.app with per-channel share buttons
- Occasion, person and interest landing pages with demo uncards
- Comparison pages and one free writing tool
- Crawler rules: AI crawlers allowed on uncard.app, blocked on uncard.gifts
- Permanent redirects: the uncard.gifts home page to uncard.app, and old uncard.app/c links to uncard.gifts

### Sources (as listed in the plan)

- FTC: Complying with COPPA, frequently asked questions — cookies as personal information, and the internal-operations exception
- Google Search Central: spam policies — scaled content abuse
- UNCARD Opus Review Round 2 Report (project doc): hosting analytics options A to F, and the D12 rule
- uncard Sharing and Referral Loop research (project doc): share versions, link previews, and what never appears on a tile — ingested here as `research/sharing-referral-loop.md`
- Uncard: Holding the Recipient's Attention research (project doc): the privacy-minimal event list and Quebec's off-by-default rule — ingested here as `research/recipient-attention.md`
- UNCARD Prioritized Work v1 (project file): D16, W-37, W-47 and W-48

## Open questions

- ~~Infrastructure and decision-status conflicts with `decisions/0006`~~ — **Resolved 2026-10-06 (Brian):** Jordan's plan is the newer one, so it wins (`decisions/0005`, newest wins). D16 is settled as this plan describes: a separate uncard.gifts host on a second Lovable project (W-48). `decisions/0006` is marked superseded.
- **Infrastructure conflict:** this plan assumes uncard.gifts runs as a second Lovable project (W-48 "approved"); `decisions/0006` (same date, 2026-10-02) instead chose a Cloudflare Worker and treats that as replacing W-48. Only one of these can be what's actually getting built — needs a partner conversation, not a wiki edit.
- **Decision-status conflict:** this plan says D16 is "Settled... Jordan adopted this plan on 2 October 2026"; `decisions/0006` is still `Status: Open` and `slack/ledger.md` shows no partner replies yet. Confirm directly with Jordan whether D16 is actually decided before treating it as settled anywhere else in the wiki.
- **Analytics granularity**, again: this plan's card-side counter is deliberately minimal ("aggregate... never shown to the giver"), but doesn't reconcile with the more granular event schemas proposed in `research/recipient-attention.md` and `research/sharing-referral-loop.md` for the same uncard.gifts surface.
- **Unresolved per the plan itself:** counsel hasn't confirmed that aggregate, cookieless card counts need no consent in Canada, the US, the EU or the UK.
- **Not yet in `docs/tasks/`:** the eight new work items listed above (tag scheme, preview-bot logging, teaser page, SEO landing pages, crawler rules, redirects) aren't reflected in the task catalogue — flagged for whoever next updates it.
