# Checkout Research

**Status:** Draft
**Updated:** 2026-10-06
**Owner:** Jordan
**Method:** Written by Jordan's research agent and posted by Jordan in Slack #non-build-stuff on 2026-10-02. Ingested as written; the findings were not re-verified here.

## TL;DR

- **Recommended paywall:** one free, email-gated, partial preview, then a one-screen paywall with Apple Pay, Google Pay and Link at the top. Payment unlocks the full uncard, unlimited edits and the shareable link.
- **Checkout should stay guest-only.** Collect email only (needed anyway to deliver the link), show the full price before payment starts, and never add anything that cheapens the gift: no third-party ads, no pre-ticked add-ons, no watermark the recipient could ever see.
- **Recommends testing price, not assuming it.** Launch at $5.99 with a 2-for-$9.99 plan shown beside it, but A/B test $4.99 against it rather than assuming charm pricing wins — a 2022 preregistered study found no reliable left-digit effect.
- **Biggest levers, roughly in order of evidence:** express wallets (+22.3% conversion for Apple Pay per Stripe), guest checkout (18% of shoppers abandon over forced accounts), no surprise costs (40% of abandoners cite extra costs), and visible reassurance (a remake guarantee plus sample uncards).
- **Tax and currency need professional review**: US digital-goods sales tax varies by state, Canada's simplified GST/HST registration kicks in past CA$30,000/12 months, and Quebec QST is separate — none of this is confirmed here.

## Implication for Uncard

- **Tests the decided price, doesn't override it.** `decisions/0002-pricing-model.md` (Accepted) already sets $5.99 per uncard / $9.99 per month for two. This research treats $5.99 as the launch price but recommends A/B testing $4.99 against it — useful as a future experiment design, not a reason to reopen 0002 on its own.
- **Payments work stays deferred.** The detailed Stripe stack (Payment Element, Express Checkout, Billing for the two-a-month plan, Stripe Tax, Radar) is a future spec. `AGENTS.md` is explicit: "Stripe is deferred. Do not scaffold, connect or mock payments." Nothing here authorizes starting that work.
- **Matches what's actually built.** `product/live-product.md` lists "Payments: Off. None built," and D11 ("pricing terms wait for payments") is still open — consistent with this doc being research, not a build ticket.
- **New input for an open decision.** D11a in `product/live-product.md` ("currency, CAD or USD") is still open; this research's CAD recommendation (manual charm prices like CA$7.99, not FX-converted) is a useful data point for whoever picks it up.
- **Tax/legal gaps aren't tracked anywhere yet.** The US state nexus, Canadian GST/HST and Quebec QST items, plus CASL/TCPA rules for recovery emails, don't correspond to any existing decision record — flagged below rather than invented into one.

## Source document

> The text below is the research file as posted in Slack on 2026-10-02 (`Uncard Checkout Research How to Get Givers to Pay on a Phone, on the Day.md`), reproduced verbatim except for heading levels, which are shifted down so this page has a single top-level heading. Treat its content as the research agent's findings, not as wiki fact — see the header above and the caveats and sources inside it.

### Uncard Checkout Research: How to Get Givers to Pay on a Phone, on the Day

**Recommendation: show one free, email-gated, partial preview, then a one-screen paywall with Apple Pay, Google Pay and Link at the top.** Payment unlocks the full uncard, unlimited edits and the shareable link. Keep checkout guest-only, show the full price before payment starts, and don't add anything that cheapens the gift: no third-party ads, no pre-ticked add-ons, no watermark the recipient could ever see.

#### TL;DR
- **Paywall placement.** Neither pure model works for uncard. Charging before any generation (as Lensa and HeadshotPro do) asks too much trust for a gift bought under time pressure. Unlimited free previews (as Suno and Gamma allow) cost too much in model spend. The best fit is one capped, low-cost preview behind an email capture, then pay. RevenueCat's 2026 data shows hard paywalls convert about 5x better than freemium (10.7% vs 2.1% at Day 35) while retaining users just as well,\[1\] which supports asking for payment early once value has been shown.
- **Biggest checkout levers**, roughly in order of evidence:
  - Express wallets: Stripe measured +22.3% conversion for Apple Pay among eligible checkouts.\[2\]
  - Guest checkout: 18% of shoppers have abandoned because they were forced to create an account (Baymard).\[3\]
  - No surprise costs: 40% of non-browsing abandoners cite extra costs (Baymard, Sep 2025).\[4\]
  - Visible reassurance: a remake guarantee and sample uncards answer the 19% who don't trust a site with their card.\[4\]
- **Price and the thank-you page.** Launch at $5.99, with a 2-for-$9.99 monthly plan shown beside it. Test $4.99 against it rather than assuming charm pricing will make up the margin: a preregistered 2022 PLOS ONE experiment (Fenneman et al., 266 participants making 4,788 purchasing decisions) found "no support for either of the two price-perception effects," including the left-digit effect. Show prices in CAD to Canadians. Keep the thank-you page free of Rokt-style ads (vendor-claimed $0.30–$0.80 per order)\[5\] and use it for "make another," reminders and scheduled sending.

#### Key Findings

##### 1. Funnel model with benchmark ranges

Nobody publishes step-by-step funnels for made-to-order generative gifts, so the model below joins the closest disclosed benchmarks. Ranges marked "assumption" are planning numbers to replace with uncard's own data within the first two weeks of launch.

| Step | Benchmark range (step conversion) | Source and grade | Notes for uncard |
|---|---|---|---|
| Landing → start chat | 20–40% (assumption) | No published benchmark; C | Depends on traffic. Measure from day one. |
| Start chat → first preview | 50–75% (assumption) | RevenueCat SOSA 2025: 80% of trial starts happen on day one,\[6\] so intent decays fast; B (directional) | A short chat (under 2 minutes) is the lever. Every extra question costs completions. |
| First preview → paywall view | 85–100% | Design-determined | Show the paywall on the preview screen, not one tap away. |
| Paywall view → payment start | 15–35% (assumption, bounded below) | Lower bound: RevenueCat hard-paywall download-to-paid is a median 10.7% (SOSA 2026) to 12.1% (SOSA 2025); A.\[1\]\[6\] The top 10% of hard-paywall apps reach 38.7% (SaaStr summary of SOSA 2026); B\[7\] | Uncard's paywall comes after value has been shown, so it should beat a cold app-download paywall. |
| Payment start → paid | 55–80% | Baymard's average cart abandonment is 70.22% across 50 studies (updated Sep 22, 2025),\[4\] but that counts cart-adds, not payment starts. Express wallets add +22.3% among eligible checkouts (Stripe, Apr 2025);\[2\] A for abandonment, B for wallets | Wallet-first payment on a single screen should put uncard at the top of this range. |
| End to end (visit → paid) | 2–6% | HeadshotPro says it converts about 5% of visitors (affiliate page, undated, self-reported; C).\[8\] Typical Shopify stores convert 1.4–2.4% (Shopify via Bogos, Jun 2026; C)\[9\] | Uncard's target should be the upper half, because the preview is persuasive. |

**Which abandonment reasons matter for a $5 digital item.** Baymard's ranked reasons, among shoppers who weren't just browsing (Baymard, updated Sep 22, 2025), apply as follows:
- **Apply strongly:**
  - Extra costs too high (40%).\[4\] Sales tax added late is the only "extra cost" uncard has, so show it early.
  - Didn't trust the site with card details (19%).\[4\]
  - Forced account creation (18%).\[4\]
  - Checkout too long or complicated (17%).\[4\]
  - Site errors (17%).\[4\]
  - Couldn't see the total cost up front (12%).\[4\]
  - Card declined (10%).\[4\]
  - Not enough payment methods (9%).\[4\]
- **Apply in an altered form:**
  - Delivery too slow (20%).\[4\] For uncard this becomes "will it be ready in time for today?" Show generation time and "send now / schedule" before payment.
  - Returns policy (13%).\[4\] This becomes the remake and refund policy.
- **Largely irrelevant:** shipping and address friction.
- **Benchmark caveat:** the widely quoted "~80% mobile vs ~66% desktop" abandonment split isn't on Baymard's own pages and appears to come from other vendors (Dynamic Yield, Contentsquare or Barilliance). Don't cite it as Baymard.

##### 2. Paywall placement: what comparable products do

| Product | When you pay | How free cost is capped | Disclosed results | Grade |
|---|---|---|---|---|
| Lensa Magic Avatars | Before generation: $7.99 for 50 avatars, or $3.99 with a subscription or trial (TechCrunch, Dec 5, 2022; CNBC, Dec 7, 2022)\[10\]\[11\] | No free avatars at all | About $8.2M revenue in the first 5 days (Prioridata, undated; third-party estimate)\[12\] | C |
| HeadshotPro | Before generation; one-time $29/$39/$59 packages (OpenTools, 2026)\[13\] | No free generation; a money-back guarantee replaces the preview | "3.3% ever refunded," based on 217,879 purchases from 2023–2026; about 5% visitor conversion (HeadshotPro site, live Oct 2026; self-reported)\[8\]\[14\] | B/C |
| Aragon, Try It On AI | Before generation (Slashdot review, Jul 26, 2023; OpenTools, 2026)\[13\]\[15\] | Refunds only if no images were downloaded, within 14 days (Aragon)\[13\] | No conversion figures disclosed | C |
| InstaHeadshots, Honest Headshots | Free preview, pay after ("You only have to pay if you love your headshots")\[16\]\[17\] | Preview-first | None disclosed | C |
| Suno | Freemium: 50 credits a day (about 10 songs), non-commercial use, watermarked output; Pro costs $10 a month (Layer3Labs, 2026; Undetectr, Sep 25, 2026)\[18\]\[19\] | Daily credit cap, a cheaper model for free users, and a shared queue\[20\]\[21\] | None disclosed | C |
| Gamma | Freemium: 400 one-time signup credits that never refresh, "Made with Gamma" branding on free exports (Gamma help center, live 2026)\[22\]\[23\] | One-time credit grant and a cap of 10 slides per prompt\[23\] | None disclosed | B |
| Canva Magic Studio | Freemium monthly AI-use pool; Canva's own pages conflict on the size (20 or 200 uses)\[24\] | Monthly reset\[25\] | None disclosed | C |
| Subscription apps in general | Hard paywall vs freemium | — | Median Day-35 conversion of 10.7% for hard paywalls vs 2.1% for freemium; 8x revenue per install at Day 60 ($3.09 vs $0.38); one-year retention of 27% vs 28% (RevenueCat SOSA 2026, Mar 2026)\[1\]\[26\] | A |

**What this means for uncard:**
1. **Pay-before-generation works when the output is low-stakes self-expression and the purchase is viral** (Lensa), or when a strong guarantee replaces the preview (HeadshotPro's 3.3% refund rate shows a guarantee can carry trust). A gift for someone else is higher-stakes: the giver needs to see that the uncard "gets" their person.
2. **Freemium with generous caps suits tools people use every day** (Suno, Gamma, Canva), not a once-per-occasion purchase. It would let model cost run away.
3. **RevenueCat's hard-paywall data says asking early doesn't hurt retention.** So the paywall should appear the moment value is shown, not after edits.
4. **Cost-capping methods the market already accepts:**
   - a one-time credit grant (Gamma)\[23\]
   - a cheaper model or lower fidelity for free users (Suno's free tier runs a lighter model)\[20\]\[21\]
   - an account or email requirement before generating
   - branding or a watermark on free output\[19\]\[22\]

##### 3. Payment methods

| Method | Disclosed lift | Grade | Fit for uncard |
|---|---|---|---|
| Apple Pay | +22.3% conversion and +22.5% revenue among eligible checkouts, from Stripe's holdback experiment across 50+ payment methods (Stripe blog, Apr 2025). Separate Stripe studies found an average 2x increase in conversion rate when Apple Pay is offered through the Express Checkout Element rather than displayed at the end of checkout. | B (method described) | Essential at launch, placed at the top of the paywall. |
| Google Pay | No equivalent independent study is published; the mechanism (no typing, biometric confirmation) is the same\[27\] | C | Essential at launch, alongside Apple Pay. |
| Stripe Link | +14% conversion for businesses with a large returning-customer base (Stripe newsroom, undated); up to +7% for logged-in Link users (Stripe support, undated). Free to enable on Stripe Checkout.\[28\]\[29\]\[30\] | B/C | Turn on at launch; it costs nothing and helps repeat givers. |
| Shop Pay | "Up to 50%" vs guest checkout and at least 10% above other accelerated checkouts, per an April 2023 external study by a "Big Three" consulting firm that Shopify cites (method not public). Shopify's Enterprise blog separately reports an average 9% lift across all checkouts and an 18% higher conversion rate for returning customers. | C | Not available outside Shopify checkout. Skip. |
| PayPal | No disclosed lift was found in this research. Baymard says 9% of abandoners leave over too few payment methods.\[4\] | C | Consider for 2027 if paywall analytics show card-entry abandonment. |

**Guest checkout vs sign-in.**
- Baymard's survey of 1,026 US adults found 18% have abandoned an order because they didn't want to create an account. Strict password rules can cause up to 19% checkout abandonment among existing account holders, and 62% of sites still don't make guest checkout the most prominent option (Baymard Checkout UX 2025).\[3\]
- **Conclusion for a first-time buyer:** collect email only, which uncard needs anyway to deliver the link and the keepsake. Use a magic link to return to saved uncards, and offer passkeys after the first purchase.
- **Costs of this approach:**
  - Magic links cost support time when emails are delayed or land in spam. Send them from a dedicated, authenticated domain.
  - Passkeys cut password-reset tickets, but few first-time buyers will set one up at checkout. Offer them on the thank-you page or the second visit.
- **Fraud:** low-price digital goods with instant delivery attract card testing. Keep Stripe Radar on, rate-limit payment attempts per session, and keep wallets prominent, since wallet payments are tokenized and biometrically confirmed. This research found no published uncard-comparable fraud-rate figure, so set a chargeback alarm at an internal threshold and monitor weekly.

**Fees at this price point.** Stripe charges 2.9% + 30¢ per domestic card payment, plus 1.5% for international cards and 1% if currency conversion is needed (Stripe pricing, live 2026).\[31\] On a $5.99 uncard that is about $0.47, or roughly 8% of the price. On $4.99 it is about $0.44, or roughly 9%. A Canadian card on a US Stripe account costs about 2.5 points more. Bundles and the monthly plan reduce the fixed-fee drag.

##### 4. Price presentation

- **Charm pricing evidence is mixed.**
  - Classic field work supports 9-endings: in Anderson (University of Chicago) and Simester (MIT)'s field experiment (Quantitative Marketing and Economics, 2003), a dress sold 21 units at $39 vs 16 at $34 and 17 at $44.
  - Thomas and Morwitz (2005) established the left-digit effect.\[32\]
  - A preregistered experiment by Fenneman, Sickmann, Füllbrunn, Goldbach and Pitz (PLOS ONE, Aug 18, 2022; 266 participants, 4,788 purchasing decisions) "found no support for either of the two price-perception effects," the left-digit and perceptual-fluency effects, and concluded that psychological price perception "may exert a weaker effect on purchasing decisions than previously suggested."
  - Both $4.99 and $5.99 are already charm prices. The real question is whether the extra dollar costs more than about 17% of buyers, and only a test can answer that.
- **Membership benchmarks.**
  - Moonpig Plus costs £9.99 a year (Moonpig FY25 investor presentation, Jun 2025).\[33\]
  - It grew to 920,000 members by April 2025, up from 540,000, and to 1.02 million by October 2025 (Moonpig FY26 interim results, Dec 9, 2025).\[33\]\[34\]\[35\]
  - Members' purchase frequency rises by more than 20% after joining, members set 2.5x more reminders, and Plus makes up about one-fifth of Moonpig UK orders (Moonpig Annual Report FY25, Jun 2025).\[36\]
  - The lesson: a membership pays off through frequency and reminders, so offer it after the first purchase rather than as a checkout decoy.
- **Credits as a framing.** Paperless Post sells coins: 25 for $12, 100 for $25, with Basic cards at 2 coins per recipient and a free tier for up to 50 recipients (Paperless Post help center, undated; App Store listing, live 2026).\[37\]\[38\] Reviewers call the coin system confusing ("Is Paperless Post Free? Coins, Pricing and Real Costs," InvitiApp, 2026). Prefer dollar bundles ("3 uncards for $14.99") to credits. Credits make a gift feel like a token spend, which is a cheapening risk.
- **Comparing against paper cards plus postage.** This is a defensible anchor, but only state prices that have been checked on the day of publication.

##### 5. Tax and currency

**United States**
- No federal rule applies, and taxability of digital products varies by state:
  - Tennessee, South Dakota and Washington tax a wide range of digital goods.\[39\]
  - Florida, Illinois and Virginia generally don't.\[39\]
  - Oregon, New Hampshire and Montana have no sales tax (Stripe, "Digital Product Tax," 2025/26).\[39\]
- Louisiana brought digital products into its sales tax base from January 1, 2025 (TaxJar, 2025).\[40\]
- Collection duty depends on each state's economic-nexus threshold. **An accountant should confirm** which thresholds uncard's transaction volume could cross, and whether an interactive web greeting card is a "specified digital product," a service, or software in each state.

**Canada**
- Non-resident vendors of digital products or services must register under the simplified GST/HST regime once taxable supplies to Canadian consumers exceed CA$30,000 over 12 months (Canada.ca e-commerce FAQ; CRA Interpretation 230511, Dec 19, 2023).\[41\]\[42\]
- Simplified registrants collect GST (5%) or HST at the province's rate, but can't claim input tax credits.\[43\]\[44\]
- Quebec administers QST separately and has its own registration system for out-of-province digital suppliers. **A Canadian tax advisor should confirm** both the QST obligation and whether uncard's US entity should register voluntarily before reaching the threshold.

**Display**
- Because 12% of abandoners couldn't see the total up front and 40% cite extra costs (Baymard),\[4\] show the estimated tax-inclusive total on the paywall. Use Stripe Tax to estimate it from IP address or postal code.
- Never add tax for the first time on the payment sheet.

**CAD pricing**
- Stripe's randomized experiment found Adaptive Pricing raised subscription payment completion by 3.3%. The lift was 0.5 percentage points higher for AI businesses where users create images, videos or other digital content (Stripe guide, 2026).\[45\]
- However, Adaptive Pricing adds a 2–4% conversion fee to the customer's price and produces uneven local prices.\[46\]\[47\]
- **Recommendation:** set manual CAD charm prices (for example CA$7.99), billed in CAD, rather than relying on automatic conversion.

##### 6. Trust

- **Card trust.** 19% of US shoppers abandoned a checkout in the past 3 months because they didn't trust the site with card details (Baymard, n=1,026, 2025). Concern spikes at the card fields, and small or niche sites trigger it easily.\[48\]
- **What reassures, per Baymard (perceived-security research, updated 2023):**
  - visually enclose the payment fields\[48\]
  - put security cues next to them\[49\]
  - use recognized seals (Norton led its 2023 seal study)\[48\]
- Uncard can largely sidestep card-field anxiety by leading with Apple Pay and Google Pay, which show the familiar system sheet.
- **Remake guarantee.** HeadshotPro, which sells personalized AI output paid upfront, reports only 3.3% of 217,879 purchases refunded under its money-back guarantee (self-reported, 2026).\[14\] That suggests a generous guarantee costs little and lets the guarantee stand in for preview depth. Its terms (no refund after download, one refund per customer) show how to limit abuse.\[50\]\[51\]
- **Sample uncards.** Put 2–3 real, playable samples on the paywall, matched to the occasion. No published lift figure exists, so A/B test them.
- **Clear refund policy.** 13% of abandoners cite unsatisfactory return policies (Baymard).\[4\] Use one line at the paywall: "Not right? We'll remake it free or refund you."

##### 7. Order bumps and add-ons

- **Gift card inside the card.** Moonpig is the strongest disclosed benchmark:
  - Gift attach rate was 17.9% in FY26, up from 17.7% in FY25 (Moonpig results, Jun 25, 2026).\[52\]\[53\]
  - Attached gifting revenue was £123.8m, against £203.5m of card revenue.\[53\]
  - Management says more than 60% of occasions involve both a card and a gift, but even Moonpig's attach rate has moved only about 0.2 points a year.\[54\]
  - The implication: offer a gift card as one optional, un-ticked line on the paywall with preset amounts. Make sure the recipient can redeem it without creating an account, or it adds recipient steps.
- **Extra year of hosting ($3).** Low value, and it adds a decision at the worst moment. Offer it at month two or three through the "keep this link live" email instead.
- **Printed keepsake.** Physical fulfillment clashes with same-day buying and adds shipping costs, which are the top abandonment reason. Keep it as a post-purchase upsell, not a checkout bump.
- **Second uncard.** Present this as the plan ("2 a month for $9.99") at the paywall, and as "make another" after purchase.

##### 8. Thank-you page

| Option | Disclosed economics | Brand risk | Verdict |
|---|---|---|---|
| Rokt Thanks (third-party offers) | Up to $500K incremental profit per 1M transactions and a 5.6% average positive engagement rate (Rokt, live 2026).\[55\] AfterSell, Rokt's Shopify-focused reseller, quotes $0.30–$0.80 per order and "zero negative impact on retention or brand perception" (AfterSell, live 2026).\[5\] | Vendor claims without published method (C). Ads for meal kits or streaming next to a love note cheapen the gift. Paperless Post's homepage promises "No ads, ever," and a co-founder (the company was founded by siblings James and Alexa Hirschfeld) compared ads to "getting a flyer inside a wedding invitation". | Never at launch. |
| Own upsells (membership, hosting, keepsake) | Moonpig Plus lifts frequency by more than 20% (Moonpig FY25)\[56\] | Low, if the offer is relevant | Yes, with one offer only. |
| "Make another" plus reminders | Moonpig's database grew to 101m reminders (FY25) and 107m (H1 FY26); about nine-tenths of Moonpig and Greetz revenue comes from existing customers\[34\]\[36\]\[57\] | None | Yes, as the main action. |

At $5.99, Rokt's claimed $0.30–$0.80 would be 5–13% of revenue. That is tempting, but it is unverified and works against a product whose whole value is that it feels made by hand for one person.

##### 9. Recovery

- **Benchmarks:** abandoned-cart emails average a 3.33% placed-order rate and $3.65 revenue per recipient across 143,000+ flows (Klaviyo benchmarks, 2026).\[58\] Omnisend's 2026 report gives 1.51%–1.72% conversion and $2.54–$3.59 per email.\[59\]\[60\]
- **Timing:** first send within an hour, then at 24 hours, then at 48–72 hours.\[58\] The first email typically earns 45–55% of a flow's revenue (Branvas summary, 2026; C).\[61\]
- **Canada (CASL):** the CRTC states that an abandoned cart is not a purchase and doesn't trigger implied consent. It recommends getting express consent when the email or phone number is collected (CRTC CASL FAQ, live).\[62\]
- **United States (TCPA):** marketing texts need prior express written consent.\[63\] The FCC's one-to-one consent rule was vacated by the Eleventh Circuit (Kelley Drye, Jan 2025),\[64\] and the earlier standard was reinstated on Aug 29, 2025 (ActiveProspect, 2025).\[65\] Carrier and CTIA practice limits abandoned-cart SMS to one message per cart, sent within 48 hours (Klaviyo help center, live).\[66\]\[67\]

##### 10. Gifting timing

Same-day buyers need certainty that the uncard will arrive on time. Moonpig's investor material notes that its paid "Guaranteed Delivery" option is now chosen on more than a third of orders (FY25 presentation, Jun 2025).\[33\] Uncard's equivalent is free and instant: "Ready now — send now or schedule."

---

#### Details: Deliverables

##### Deliverable 1 — Funnel model
See the table in Finding 1. **Instrument these events:** `chat_start`, `chat_complete`, `preview_generated`, `paywall_view`, `express_pay_tap`, `card_form_start`, `payment_success`, `edit_request`, `link_shared`, `recipient_open`. Track model cost per event so cost per paid uncard is visible daily.

##### Deliverable 2 — The 10 highest-impact recommendations (ranked)

| # | Recommendation | Evidence grade | Expected effect | Effort | How to test |
|---|---|---|---|---|---|
| 1 | **Wallet-first paywall.** Apple Pay, Google Pay and Link in Stripe's Express Checkout Element at the top of the paywall screen; card entry below a "Pay another way" divider. | B (Stripe holdback, Apr 2025) | +10–20% payment start → paid on mobile. Stripe's figures: +22.3% for Apple Pay among eligible checkouts, and an average 2x conversion-rate increase when Apple Pay is offered through the Express Checkout Element rather than at the end. | S | Holdback test: 10% of sessions get card-only, measured on paid per paywall view. |
| 2 | **One free partial preview, gated by email, then pay.** Pay before full generation and before edits. | A (RevenueCat hard-paywall data) and B (HeadshotPro guarantee) | Caps model cost at one cheap generation per email, and lifts paid per starter compared with both extremes (estimate). | M | Three-arm paywall experiment (Deliverable 3). |
| 3 | **Guest checkout only.** Email is the sole required field; magic link to return; passkey offer after purchase. | A (Baymard, n=1,026) | Removes the 18% forced-account abandonment reason and the up-to-19% password-failure abandonment.\[3\] | S | Not worth testing; just ship it. Monitor support tickets about magic links. |
| 4 | **All-in price on the paywall.** Tax estimated by Stripe Tax before tapping Pay; no new line items on the payment sheet. | A (Baymard: 40% extra costs, 12% couldn't see total)\[4\] | Removes the top abandonment reason. | S–M | Before/after on payment start → paid; check tax-estimate accuracy against actual charges. |
| 5 | **Remake-or-refund guarantee plus 2–3 playable samples, next to the Pay button.** | B (HeadshotPro 3.3% refund rate; Baymard 19% trust, 13% returns policy)\[4\]\[14\] | +3–8% paywall → payment start (estimate). Refund cost of about 3% of revenue if uncard matches HeadshotPro. | S | A/B test with the guarantee line shown vs hidden; guardrail on refund rate. |
| 6 | **Saved-uncard recovery sequence.** Email at 1 hour, 24 hours and on the morning of the occasion; express-consent checkbox at email capture. | B (Klaviyo 3.33% placed-order rate) | Recovers 3–10% of saved-but-unpaid uncards. | M | Holdback of 10% of saved uncards. |
| 7 | **CAD prices for Canadians**, with manual charm price points rather than FX-converted ones. | B (Stripe: +3.3% completion with local currency)\[45\] | +3–5% Canadian conversion. | S | Geo split: CAD vs USD for Canadian IPs. |
| 8 | **Price test:** $5.99 vs $4.99, with 2 for $9.99 a month shown as the "best value" anchor. | Mixed: A for price-level testing, with charm evidence contested (Fenneman et al., PLOS ONE 2022) | Find the revenue-per-visitor maximum. | M | Deliverable 5. |
| 9 | **Send-now or schedule choice on the confirmation screen**, with the recipient's time zone and the giver always receiving the link. | C | Reduces day-of anxiety and supports pre-occasion buying. | M | Track share of scheduled sends and the effect on repeat purchase. |
| 10 | **Thank-you page built around "make another" and reminders, with no third-party ads.** One own-offer at most (membership after the first purchase). | B (Moonpig reminders and Plus frequency); C for Rokt | Repeat rate and LTV, at no brand cost. | S | A/B test "make another" placement; measure 30- and 90-day repeat. |

##### Deliverable 3 — Paywall recommendation and experiment design

**Recommended default (Variant B):**
1. The giver finishes the chat and enters an email (magic-link verified, which caps one free preview per verified email and device).
2. Uncard generates a **partial preview**: the opening scene, title and one interaction, played at full quality but stopping at a tasteful "the rest is waiting" moment. Use a cheaper render path where possible.
3. The paywall sits on the same screen: price, wallets, guarantee and samples.
4. Payment unlocks the full uncard, unlimited edits by asking (with a fair-use cap) and the link.
5. Mark the giver's preview with a giver-only "Preview" label. The recipient link never carries a watermark.

**Variants**
- **A — Pay before generation.** Chat, then samples and guarantee, then pay, then generate. This is the lowest-cost arm (the HeadshotPro/Lensa model).
- **B — Partial preview, then pay** (recommended).
- **C — Full watermarked preview plus one free edit, then pay.** This is the highest-cost arm.

**Primary metric:** paid uncards per started chat. This combines conversion and drop-off before the paywall.

**Secondary metric:** contribution per started chat, meaning revenue minus model cost minus Stripe fees.

**Guardrail metrics:**
- model cost per paid uncard
- refund and remake rate
- chargeback rate
- time from chat start to payment, in minutes
- recipient open rate
- giver CSAT or thumbs-up on the delivered uncard
- support tickets per 100 orders

**Sample size to detect a 10% relative change** (two-sided α = 0.05, 80% power):

| Baseline (primary metric) | Detect | Needed per arm | 3-arm total |
|---|---|---|---|
| 20% | 20% → 22% | ≈6,500 | ≈19,500 |
| 10% | 10% → 11% | ≈14,700 | ≈44,000 |
| 5% | 5% → 5.5% | ≈31,300 | ≈94,000 |

- These use the standard two-proportion formula. Correcting for three comparisons (α = 0.025 each) adds about 20%.
- **If launch traffic is small, use stepping stones.** First run A vs B only, which halves the sample. Alternatively, use a sequential or Bayesian decision rule with a pre-registered minimum of 2 full weeks, so that both weekday and weekend occasion patterns are covered.

##### Deliverable 4 — Payment stack

**Launch (Q4 2026)**
- **Payments:** Stripe Payment Element plus the Express Checkout Element (Apple Pay, Google Pay, Link) on uncard's own paywall, or embedded Stripe Checkout if faster to ship. Register the domain for Apple Pay.
- **Cards:** Visa, Mastercard, Amex and Discover.
- **Identity:** guest checkout with email only; magic-link sign-in to return to saved uncards.
- **Tax:** Stripe Tax for US state and Canadian GST/HST calculation and threshold monitoring.
- **Currency:** USD for US buyers; manual CAD price points for Canadian buyers.
- **Fraud:** Radar defaults, a payment-attempt rate limit, and a weekly dispute review.
- **Subscriptions:** Stripe Billing for the 2-for-$9.99 plan, with one-tap cancel in the email footer and the account page.

**2027**
- Passkeys for returning givers, and a membership with reminders, modelled on Moonpig Plus.
- PayPal or Venmo if paywall data shows meaningful card-form abandonment.
- Gift cards inside the card through a gift-card partner. Recipient redemption must need no account.
- Group contributions: the organizer pays a base price and shares a Stripe-hosted contribution link; contributors pay by wallet with no account.
- Team plans invoiced through Stripe Billing.

##### Deliverable 5 — Price test plan

1. **Test 1 (launch, 4 weeks):** single price of $5.99 vs $4.99, with 2 for $9.99 a month shown in both arms.
   - Primary metric: revenue per started chat net of Stripe fees.
   - Guardrails: refund rate and plan take-up.
   - Expectation: $4.99 must lift conversion by more than about 22% to beat $5.99 on net revenue, because Stripe's fixed 30¢ fee makes the lower price lose about 22% of net per order. Treat this as a hypothesis, not a forecast.
2. **Test 2:** plan framing.
   - (a) Single price plus plan shown as "Best value: 2 a month."
   - (b) Single price plus a 3-pack ("3 for $14.99, use anytime").
   - (c) Single price alone.
   - Watch the share of buyers choosing multi-unit options and 60-day usage of the second and third uncards.
3. **Test 3:** anchors.
   - A "less than a card and a stamp" comparison line vs no comparison. Only use verified current prices, and refresh them quarterly.
   - Avoid "credits" language entirely.
4. **Membership (after first purchase, not at checkout):** a yearly membership with reminders, priced and tested once repeat-purchase data exists. Moonpig's data (a lift of more than 20% in frequency, 2.5x reminders)\[36\] indicates the value lies in occasion reminders.
5. **Canada:** CA$7.99 vs CA$8.99 once Canadian volume allows. Until then, keep CA$7.99.

##### Deliverable 6 — Thank-you page policy

**What we show, in this order:**
1. The uncard link with large "Copy link" and "Share" buttons, and **Send now / Schedule** (date, time and the recipient's time zone).
2. "Save their birthday for next year?", an optional, unticked reminder opt-in. This doubles as express consent under CASL.
3. "Make another uncard", pre-filled with the giver's tone and style.
4. At most one own-offer: the monthly plan, or a passkey or account save.
5. A receipt line and the remake guarantee.

**What we never show:**
- third-party ads or offer networks (Rokt or similar)
- discount codes for other brands
- countdown timers
- pre-ticked add-ons
- survey walls before the link
- anything the recipient sees that wasn't written for them

##### Deliverable 7 — Recovery sequence and consent rules

| Step | Timing | Channel | Content |
|---|---|---|---|
| 1 | 1 hour after the preview is left unpaid | Email | "Your uncard for [name] is saved," with a thumbnail of the preview and a one-tap resume link that opens directly on the wallet paywall. |
| 2 | 20–24 hours later | Email | Reassurance: the guarantee, a sample, "ready instantly." |
| 3 | The morning of the occasion, if a date was given (otherwise 72 hours) | Email | "It's [name]'s day: send it in one tap." No discount; discounts train people to wait and cheapen the gift. |
| Optional | Within 48 hours, once only | SMS | Only with prior express written consent (US) or express consent (Canada). One message per saved uncard. |

**US rules**
- CAN-SPAM applies to commercial email. Include a working unsubscribe link and a postal address, and honor opt-outs.
- TCPA requires prior express written consent for marketing texts, sought on its own and never bundled with payment.\[68\] Keep consent records.
- **A lawyer should confirm** whether a "your saved uncard" email counts as a transactional or relationship message rather than a commercial one.

**Canada rules**
- Under CASL, an abandoned or unpaid uncard does not create implied consent (CRTC FAQ).\[62\]
- Collect express consent with an unticked box at email capture ("Email me about this uncard and occasion reminders").
- Without it, send only messages the giver explicitly asked for, such as the magic link itself.
- Each message must identify the sender and include an unsubscribe.\[69\]
- **A Canadian lawyer should confirm** whether a resume-your-draft reminder needs consent.

---

#### Recommendations: Brand and Recipient Red Flags

**Would cheapen the brand:**
- a watermark on anything a recipient can open
- third-party post-purchase ads
- a discount in the first recovery email
- "credits" or coin language
- pre-ticked add-ons
- countdown timers
- more than one upsell on the thank-you page

**Would add recipient steps (avoid):**
- gift cards that need an account to redeem
- scheduled sends that need the recipient's phone number or email when the giver would rather share the link
- any login or app prompt on the recipient's link
- group-contribution flows that message the recipient before the uncard is ready

#### Caveats

- **Vendor figures:** Stripe, Shopify, Rokt and HeadshotPro numbers are vendor-disclosed. Only Stripe's payment-method experiment describes its method. Treat the Shop Pay, Rokt and HeadshotPro conversion claims as grade C.
- **Missing disclosures:** no generative-gift company publishes step-level funnels. The middle funnel ranges are reasoned assumptions to replace with uncard's own data.
- **Stale and conflicting sources:** Lensa data is from 2022. Canva's free AI allowance is contradictory across its own pages.\[24\]
- **Charm pricing:** the evidence is contested, so test the price rather than assume the effect.
- **Professional review:** tax taxability by state, Quebec QST, CASL treatment of draft reminders, and TCPA consent wording all need review by a qualified accountant or lawyer in each country before launch.

#### Sources

1. [The State of Subscription Apps in 10 minutes: lessons, trends, and benchmarks for 2026](https://www.revenuecat.com/blog/growth/subscription-app-trends-benchmarks-2026)
2. [Testing the conversion impact of 50+ global payment methods](https://stripe.com/blog/testing-the-conversion-impact-of-50-plus-global-payment-methods)
3. [Checkout UX Best Practices 2025](https://baymard.com/research-articles/current-state-of-checkout-ux)
4. [50 Cart Abandonment Rate Statistics 2026 – Cart & Checkout – Baymard](https://baymard.com/lists/cart-abandonment-rate)
5. [Rokt Thanks — Earn Incremental Income on Every Order](https://www.aftersell.com/rokt-thanks)
6. [RevenueCat's State of Subscription Apps 2025 Report: AI's Dominance, Retention Challenges, and the Shift Away from Pure Subscriptions - Subscription Insider](https://www.subscriptioninsider.com/article-type/news/revenuecats-state-of-subscription-apps-2025-report-ais-dominance-retention-challenges-and-the-shift-away-from-pure-subscriptions)
7. [the top 10 learnings from revenuecats state of subscription apps how 115000 mobile apps deliver 16b in revenue whats working whats quietly killing growth](https://saastr.com/the-top-10-learnings-from-revenuecats-state-of-subscription-apps-how-115000-mobile-apps-deliver-16b-in-revenue-whats-working-whats-quietly-killing-growth)
8. [HeadshotPro Affiliate Program](https://www.headshotpro.com/affiliate)
9. [Shopify Checkout Optimization: 9 Ways To Boost Your CR (2026)](https://bogos.io/shopify-checkout-optimization/)
10. [Lensa AI, the app making 'magic avatars,' raises red flags for artists](https://techcrunch.com/2022/12/05/lensa-ai-app-store-magic-avatars-artists/)
11. [Here's how to use Lensa, the chart-topping app that uses AI to transform your selfies into digital avatars](https://www.cnbc.com/2022/12/07/lensa-app-turns-selfies-into-avatars-with-artificial-intelligence.html)
12. [Lensa AI Revenue, Users & Statistics 2026](https://prioridata.com/data/lensa-ai-statistics/)
13. [Best AI Headshot Generators: Paid Plans Compared](https://opentools.ai/resources/best-ai-headshot-generators)
14. [AI Headshot Generator that Looks Like You](https://www.headshotpro.com/ai-headshot-generator)
15. [Try it on AI Reviews - 2026](https://slashdot.org/software/p/Try-it-on-AI/)
16. [AI Headshot Generator - Create Professional Headshots Online](https://honestheadshots.com/)
17. [InstaHeadshots (now Magic Studio) - #1 AI Headshot Generator](https://instaheadshots.com/)
18. [Suno AI Free: Exactly What You Get (and What You Don't) in 2026](https://suno.bi/en/blog/suno-ai-free-what-you-get)
19. [How Much Does Suno Cost? Pricing & Credits (2026)](https://www.layer3labs.io/guides/suno-pricing)
20. [Suno Pricing 2026: Free vs Pro vs Premier, Which to Buy — Undetectr](https://undetectr.com/blog/suno-free-vs-pro-vs-premier)
21. [Suno AI Free Tier Credits 2026: How to Use Free Generations Wisely](https://musicmake.ai/blog/suno-ai-free-tier-credits-2026)
22. [Is Gamma Free? The Truth About Gamma's Free Tier in 2026](https://www.instantdeckai.com/alternative/gamma/free-tier)
23. [How can I upgrade my Gamma subscription?](https://help.gamma.app/en/articles/8077107-upgrading-your-gamma-subscription)
24. [Canva Magic Studio in 2026: What Each AI Tool Does](https://moda.app/blog/canva-magic-studio)
25. [Canva AI Review: Free Plan Vs Pro — Is It Worth It?](https://dailytechedge.com/canva-ai-review/)
26. [RevenueCat State of Subscription Apps: Trial, Paywall & Churn Benchmarks - RocketShip HQ](https://www.rocketshiphq.com/revenuecat-state-of-subscription-apps-2025-summary/)
27. [Apple Pay vs Google Pay 2026: 800M vs 250M Users (Stats)](https://www.chargeflow.io/blog/apple-pay-vs-google-pay-statistics-adoption-rates-market-share)
28. [Link with Checkout](https://docs.stripe.com/payments/link/checkout-link)
29. [Adding Link to your site : Stripe: Help & Support](https://support.stripe.com/questions/adding-link-to-your-site)
30. [Businesses using Stripe's newest checkout optimizations saw 10.5% more revenue](https://stripe.com/newsroom/news/payments-revenue-uplift)
31. [Pricing & Fees](https://stripe.com/pricing)
32. [Charm Pricing in Banking: How To Use The Left Digit](https://southstatecorrespondent.com/banker-to-banker/price-strategy/charm-pricing-in-banking-how-to-use-the-left-digit/)
33. [Strictly Private and Confidential Full year results presentation Year ended](https://www.moonpig.group/media/c0emy1st/moonpig-group-plc-fy25-full-year-results-investor-presentationpdf.pdf)
34. [9 December 2025 Moonpig Group plc ("Moonpig Group" or the "Group")](https://www.moonpig.group/media/t2lbafil/moonpig-group-plc-fy26-half-year-results-announcement.pdf)
35. [26 June 2025 Moonpig Group plc ("Moonpig Group" or the "Group")](https://www.moonpig.group/media/ylcfmqgj/moonpig-group-plc-fy25-full-year-results-announcementpdf.pdf)
36. [Moonpig : Annual report and accounts for the financial year ended 30 April 2025](https://www.marketscreener.com/quote/stock/MOONPIG-GROUP-PLC-118501097/news/Moonpig-Annual-report-and-accounts-for-the-financial-year-ended-30-April-2025-50467187/)
37. [Paperless Post: Invitations - App Store - Apple](https://apps.apple.com/us/app/paperless-post-invitations/id489940389)
38. [How much does my Card or Flyer cost?](https://paperlesspost.zendesk.com/hc/en-us/articles/360046178571-How-much-does-my-Card-or-Flyer-cost)
39. [Digital Product Tax: A Guide](https://stripe.com/resources/more/digital-product-tax)
40. [Sales tax by state: should you charge sales tax on digital products? - TaxJar](https://www.taxjar.com/blog/sales-tax-digital-products)
41. [FAQ - Application of the GST/HST in relation to electronic commerce supplies - Canada.ca](https://www.canada.ca/en/revenue-agency/programs/about-canada-revenue-agency-cra/federal-government-budgets/faq-relation-electronic-commerce-supplies.html)
42. [19 December 2023 GST/HST Interpretation 230511 - Non-resident vendor selling digital products or services](https://taxinterpretations.com/content/827197)
43. [How to register for GST/HST in Canada in 2026 - Quaderno](https://quaderno.io/guides/canada/gst/registration/)
44. [GST/HST Registration Canada 2026](https://truenorthbenefits.ca/taxes/gst-hst-registration-small-businesses/)
45. [How Local Pricing Affects Subscription Conversion for Media, Entertainment, and Gaming](https://stripe.com/guides/how-local-pricing-affects-subscription-conversion-for-media-entertainment-and-gaming)
46. [Adaptive Pricing for Subscriptions : Stripe: Help & Support](https://support.stripe.com/questions/adaptive-pricing-for-subscriptions)
47. [localize prices](https://docs.stripe.com/payments/currencies/localize-prices)
48. [How Users Perceive Security During the Checkout Flow – Baymard](https://baymard.com/blog/perceived-security-of-payment-form)
49. [Visually Reinforce Your Credit Card Fields (89% Get it Wrong)](https://baymard.com/blog/visually-reinforce-sensitive-fields)
50. [The #1 AI Headshot Generator for Professional Headshots](https://www.headshotpro.com/legal/terms-and-conditions)
51. [The Realism Guarantee](https://www.headshotpro.com/refund)
52. [Final Results](https://www.investegate.co.uk/announcement/rns/moonpig-group--moon/final-results/9635380)
53. [National Storage Mechanism](https://data.fca.org.uk/artefacts/NSM/RNS/52bafef3-2f96-4ed0-9bf2-763ebd9ac696.html)
54. [Earnings call transcript: Moonpig H2 2026 results lift stock 10% on growth outlook By Investing.com](https://www.investing.com/news/transcripts/earnings-call-transcript-moonpig-h2-2026-results-lift-stock-10-on-growth-outlook-93CH-4760026)
55. [Turn 'Thank You' Into Joy and Profit](https://www.rokt.com/products/rokt-thanks)
56. [2025 Full-Year Results Announcement](https://www.moonpig.group/investors/press-releases/2025-full-year-results-announcement/)
57. [Half Year FY26 Results - Investor Factsheet](https://www.moonpig.group/media/53uonjys/moonpig-group-plc-fy26-half-year-results-investor-factsheet.pdf)
58. [Abandoned Cart Emails: Timing & 10 Examples](https://www.darkroomagency.com/observatory/abandoned-cart-email)
59. [Abandoned Cart Email Examples, Templates & Tips That Work](https://www.omnisend.com/blog/abandoned-cart-email/)
60. [Email Marketing Benchmarks: Open Rates, Clicks, and Conversions](https://www.omnisend.com/blog/email-marketing-benchmarks/)
61. [80+ Email Marketing Benchmarks for Ecommerce (2026)](https://branvas.com/blogs/news/ecommerce-email-marketing-benchmarks)
62. [Frequently Asked Questions about Canada's Anti-Spam Legislation](https://crtc.gc.ca/eng/com500/faq500.htm)
63. [TCPA text messages: Rules and regulations guide for 2026 - ActiveProspect](https://activeprospect.com/blog/tcpa-text-messages/)
64. [Eleventh Circuit Vacates TCPA 1:1 Consent…](https://www.kelleydrye.com/viewpoints/blogs/ad-law-access/eleventh-circuit-vacates-tcpa-11-consent-rule)
65. [Understanding the FCC one-to-one consent rule update - ActiveProspect](https://activeprospect.com/blog/fcc-one-to-one-consent/)
66. [TCPA and CTIA Compliance for SMS Marketing in the US](https://www.bloomreach.com/en/blog/understanding-tcpa-and-ctia-compliance-for-sms-marketing-in-the-us)
67. [Understanding US guidelines for SMS cart abandonment flows](https://help.klaviyo.com/hc/en-us/articles/4404189657755)
68. [TCPA regulations for text messages: what you must know in 2025](https://leadcompliant.com/articles/tcpa-basics/tcpa-regulations-text-messages)
69. [Doing Business in Canada: CASL](https://gowlingwlg.com/en/insights-resources/guides/2023/doing-business-in-canada-casl)

## Open questions

- Recommends A/B testing $4.99 against the already-**Accepted** $5.99 price (`decisions/0002-pricing-model.md`) — flagging rather than reopening the decision.
- The full Stripe payment stack described in Deliverable 4 is payments work; `AGENTS.md` says Stripe is deferred and must not be scaffolded, connected or mocked. Treat this doc as a future reference only.
- Introduces a CAD pricing recommendation (manual charm prices, e.g. CA$7.99) not present in `decisions/0002` or `product/experience.md`; relevant to the still-open currency decision D11a in `product/live-product.md`.
- Tax and legal items (US state digital-goods tax, Canadian GST/HST threshold, Quebec QST, CASL/TCPA consent for recovery emails) have no corresponding decision record yet — someone should decide where these get tracked before launch.
