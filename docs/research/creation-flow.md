# Creation Flow Research

**Status:** Draft
**Updated:** 2026-10-06
**Owner:** Jordan
**Method:** Written by Jordan's research agent and posted by Jordan in Slack #non-build-stuff on 2026-10-02. Ingested as written; the findings were not re-verified here.

## TL;DR

- **Ask less, but ask better.** Cap required intake at about three open, scene-seeking questions (roughly 2–4 minutes to the first preview) with everything else skippable; open-text turns cost more per step than tap-quiz benchmarks, so every extra required step compounds drop-off.
- **Authorship is the product.** Recipients penalize gifts they learn were AI-made (rated "lazy," "insincere") — but the penalty shrinks when the giver's own words are visibly quoted and attributed. uncard should read as the giver's words crafted by uncard, never as uncard writing the giver's feelings for them, and should never claim "Sam wrote this."
- **Make the wait feel like work being done for them.** A determinate, named-stage progress bar on the giver's own material (the "labor illusion") beats a blank spinner; target a first scene visible within ~20s, a full preview at a median of ~60s and a 120s hard ceiling.
- **Editing should feel like steering, and every edit must visibly succeed.** One-tap tone chips, per-scene swap and always-on undo build ownership (the IKEA effect); edits that fail or regenerate everything kill it.
- **Price up front, no account before the preview, wallet pay first.** Show the price on landing, never force login before the preview, lead the paywall with Apple Pay/Google Pay, and never default into the subscription — surprise end-of-flow costs are the most common complaint across comparable products' reviews.

## Implication for Uncard

- **Matches the built studio's shape, with one gap to watch.** `product/live-product.md`'s "How making an uncard will feel like (built, shut)" already does six quick basics plus up to ten more skippable questions, drafts at three facts, and five rewrites per card — directionally aligned, but it allows up to 16 questions where this research argues for capping *required* open turns at three. Worth a look once there's real session data, not a reason to rebuild anything now.
- **Pricing lines up exactly.** The $5.99-per-uncard / $9.99-per-month-for-two numbers and the "no subscription surprise" framing match `decisions/0002-pricing-model.md` and `decisions/0005-demo-is-source-of-truth.md`.
- **Payments is still deferred.** This doc's checkout design (price on landing, wallet-first paywall, no login before pay) is useful as a future spec, but `AGENTS.md`'s "Stripe is deferred. Do not scaffold, connect or mock payments" rule stands — nothing here is a green light to start that work.
- **Suno appears only as a UX benchmark, not a vendor pick.** The wait-time research (§3) cites Suno's generation-wait pattern as a design reference. Suno itself has since been ruled out as a music vendor (`slack/ledger.md`, decided 2026-10-05, no public API and terms ban automation/redistribution) — the citation is about the progress-bar pattern, not an endorsement to use Suno.
- **Children's-data handling matches the privacy gate.** "Collect only a first name and age band from the adult giver" (Kids and Families) matches `AGENTS.md`'s "no child accounts, no child contact data" rule.

## Source document

> The text below is the research file as posted in Slack on 2026-10-02 (`Making an Uncard Feel Like a Joy Research-Backed Creation Flow, Landing to Paid.md`), reproduced verbatim except for heading levels, which are shifted down so this page has a single top-level heading. Treat its content as the research agent's findings, not as wiki fact — see the header above and the caveats and sources inside it.

### Making an Uncard Feel Like a Joy: Research-Backed Creation Flow, Landing to Paid

The flow that gets the most givers to finish and makes them proudest is short and specific. Ask three questions that each pull out one real detail, show the giver their own words being built into the uncard while it generates, and then let them steer the result with one-tap edits. The gift-psychology and AI-disclosure research gives one clear warning: the uncard must read as the giver's words crafted by uncard, never as AI writing the giver's feelings for them. When recipients know AI wrote a personal message, they judge the sender lazy and insincere.\[1\] When the giver's own specifics are visible, that penalty shrinks.

#### TL;DR

- **Ask less, but ask better.** Use three substantive turns before the first preview, about 2 to 3 minutes. Make each one an open, scene-seeking question ("tell me about a time…"), add one follow-up that digs into what the giver said, and make everything else optional. Every extra step compounds drop-off. Vendor onboarding benchmarks put it at 20 to 35% per screen. The scarce resource is not the number of questions but how specific each answer is.
- **Authorship is the product.** Recipients penalize gifts and messages they believe were AI-made: 1,300+ participants in Zhu and Molnar's 2026 Computers in Human Behavior study rated senders "lazy" and "insincere" when AI authorship was disclosed, though undisclosed messages were judged just as positively as human-written ones. The penalty shrinks when the giver's own input is visible. So uncard should quote the giver, attribute the uncard to the giver, and never fake a handwritten note. The 2025 IKEA-effect meta-analysis (d = 0.57) says a few successful edits will deepen ownership, as long as each edit visibly works.
- **Make the wait feel like work being done for them.** Show progress with named stages and the giver's words turning into scenes. Put the price on screen from the start, and allow no account wall or subscription surprise before payment. Surprise charges at the end are the most common complaint in Paperless Post, JibJab and Suno reviews.

#### Key Findings

##### 1. Intake: how many questions, and what makes chat feel like a friend

**Drop-off compounds per step, and the first few steps matter most.** In SurveyMonkey's analysis of 100,000 surveys (data from 2009–2010, so pre-2023, grade A for sample size), the sharpest rise in drop-off came with each added question up to 15. Respondents who got past that point were much more tolerant.\[2\] Vendor benchmarks are grade C and self-interested, but they point the same way:
- Outgrow's 2025 benchmarks claim 65–85% completion for 3–7 question quizzes, 45–65% for 8–15, and 25–45% for 16+, and call question 3 "the danger zone."\[3\]
- UXCam puts typical onboarding drop-off at 20–35% per screen.\[4\]
- ConvertFlow's 2026 guide shows the compounding: a six-step quiz with 70% step completion delivers only 12% of starters to the end.\[5\]

These numbers come from tap-to-answer quizzes. Uncard's open text answers cost more effort per turn, which argues for fewer turns, not more.

**There is a counterweight: too few prompts produces generic material.** Cameo reviewers on Google Play complain that "only being able to lay out 3 facts" is "maddening" (undated, preview-only quote collected for this report).\[6\] Givers who care want room to say more. The resolution is to make three turns required and leave optional depth unlimited: an "add another memory" chip and a free-text "anything else?" that never blocks the preview.

**What makes it feel like a friend rather than a form:**
- **It reflects back what it heard.** The best signal of attention is a follow-up that uses the giver's own words ("You said she sings in the car. What song?"). Oral-history practice codifies this. The Smithsonian Institution Archives guide says "If you get a short answer, follow up with tell me more, who, what, when, where, how and why."\[7\] The National Park Service recommends probes like "Can you give me an example of that?"\[8\] The Columbia guide advises "Ask for visual descriptions of people, places, or objects" (practitioner guidance, grade C).\[9\]
- **One question at a time, short, never yes/no.** All three oral-history guides say this.\[7\]\[8\]\[10\]
- **No small talk or filler.** Nielsen Norman Group's guidance on site chatbots, "Less Chat, More Answer," says users type short, imperfect queries and that bots should cut filler.\[11\] NN/g's work on prompt controls (August 2, 2024) and use-case prompt suggestions finds that tappable suggestions near the input lower interaction cost and offer inspiration (grade B/C).\[12\]\[13\]
- **State scope up front.** Practitioner summaries of NN/g's chatbot guidance stress being clear about what the bot does.\[14\]\[15\] For uncard, that means one line: "Three quick questions, then you'll see the whole uncard."

##### 2. Drawing out specifics

**What the products do.**
- StoryWorth sends one prompt a week, lets storytellers edit, skip or write their own questions, and offers "Magic Interviews" in which "we'll ask follow-up questions over a phone call to bring your story to life" (StoryWorth FAQ).\[16\]
- Remento is built on voice. Storytellers "record memories in their own voice through guided prompts," family members "contribute questions and vote on future prompts," and photos can serve as prompts (Remento FAQ).\[17\]
- A StoryWorth reviewer on Trustpilot (August 2026, preview-only quote) praised that "One question a week was not daunting and I appreciated being able to change the questions-or skip them."\[18\]

Three lessons for uncard: let givers skip or swap any question, accept voice as well as text, and treat the follow-up as the real interview.

**What reliably surfaces vivid material (synthesized from the oral-history guides, grade C):**
1. Ask for a scene, not a summary. "Tell me about a time…" beats "What's she like?"\[10\]
2. Ask for sensory and visual anchors: what it looked like, what they said, what song was playing.\[9\]
3. Ask for exact words: catchphrases, nicknames, the thing they always say.
4. Ask for contrasts or surprises: "What would surprise someone who just met him?"
5. Follow up once, on the most concrete noun in the answer.\[8\]

**For someone in a hurry on a phone:** offer voice input, give a one-line example under each question so the giver sees what "specific" means, and offer tappable "starter" chips (e.g., "a trip," "a habit," "a thing they always say") that open a sentence for the giver to finish. Remento's voice-first design rests on the premise that many people speak more easily than they write.\[17\]

##### 3. Time to wow: waiting 30–120 seconds

- **Attention limits.** Nielsen's response-time limits (NN/g; the original work predates 2023 but NN/g still maintains it) put about 10 seconds as the limit for keeping attention on a task. Past that, users need a percent-done indicator, and they "will need to reorient themselves when they return."\[19\] NN/g's progress-indicator guidance: looped spinners only for 2–10 seconds, percent-done for 10 seconds or more (grade B, long-standing practitioner research).\[20\]
- **Labor illusion.** Buell and Norton (Management Science, 2011, pre-2023, grade A) found that "when websites engage in operational transparency by signaling that they are exerting effort, people can actually prefer websites with longer waits to those that return instantaneous results—even when those results are identical."\[21\]\[22\] Their waiting screen showed a changing list of what was being searched. Later field work by Buell and colleagues (2017) found operational transparency "contributed to a 22.2% increase in customer-reported quality," as summarized by Bray (Kellogg, 2023 download).\[23\]
- **How current generators handle the wait:**
  - Suno returns two variations in roughly 30 to 90 seconds (Layer3 Labs guide, 2026, grade C).\[24\] Suno's help center says a single generation can now run up to 8 minutes of music.\[25\]
  - Gamma shows an editable outline first, then builds the deck "usually in under 60 seconds" while "you'll watch the slides appear in sequence" (MindStudio tutorials, grade C).\[26\]\[27\]\[28\]
  - Udio first generates roughly 30-second clips that users extend in increments.\[29\]
- **The common pattern:** a cheap checkpoint before the expensive step, a visible build, and the first usable piece arriving before the whole.

For uncard, the target is a first scene visible within about 20 seconds, a full preview at median 60 seconds or less, and 120 seconds as the hard ceiling at the 90th percentile.

##### 4. Co-creation and the IKEA effect

- **The meta-analysis.** Pelled, Demetriades and Walter's meta-analysis (Psychology & Marketing, first published October 14, 2025; k = 55, N = 5,454; grade A) found "a significant moderate impact of self-assembly labor on valuation (d = 0.57)," plus effects on liking, self-concept and sense of ownership.\[30\] In the related dissertation analysis, "only sense of ownership emerged as a reliable significant predictor" of the effect.\[31\]
- **The original study and its boundary.** Norton, Mochon and Ariely (2012, pre-2023) found builders paid a 63% premium.\[32\] The effect disappears when creations are left unfinished or destroyed. Effort has to end in visible success.\[33\]
- **Generative AI.**
  - Mehler, Ellenrieder and Buxmann (ECIS 2024; 174 participants in Germany) found people "valued images higher if more human effort was invested during collaborative co-creation with GenAI."\[34\] They did not find the effect for text generation (grade A/B, conference paper).\[35\]
  - A later randomized trial with ChatGPT, published in MSI Journal, says it did find the IKEA effect for text once all known triggers were included (grade B).\[35\]\[36\]
  - A 2026 Frontiers in Psychology study argues for "productive friction" so that AI output becomes "personally appropriated."\[37\]

**What this means for uncard:** the giver's labor should be small, meaningful and always successful. Supplying the specifics is the labor that counts, and one to three edits that visibly land add ownership. Forced busywork does not add value, and neither do edits that fail or regress.

##### 5. Gift psychology, finding by finding

| Finding | Source and grade | What it means for uncard |
|---|---|---|
| Givers expect expensive gifts to be appreciated more; recipients don't appreciate them much more\[38\]\[39\] | Flynn and Adams, JESP 2009 (pre-2023, A) | A $5–6 price is not a handicap. Don't add "premium" upsells that suggest more spend means more love |
| Recipients appreciate requested gifts more than unrequested ones; givers wrongly think unrequested gifts show more thought\[40\]\[41\] | Gino and Flynn, JESP 2011 (pre-2023, A) | Uncard is inherently unrequested, so it has to earn its place through accuracy. Optionally capture "something they've been wanting" and reference it |
| Givers avoid sentimental gifts out of fear they'll miss; recipients prefer them\[42\]\[43\] | Givi and Galak, JCP 2017 (pre-2023, A); Givi, WVU, May 2023 | Uncard's core value is lowering the risk of going sentimental. A preview and easy edits make the "home run" safer to try |
| Givers focus on the moment of exchange; recipients care about value over time\[44\]\[45\] | Galak, Givi and Williams 2016 (pre-2023, A) | Keepsake and hosting matter. Say what the recipient keeps |
| Thoughtfulness raises appreciation only when something triggers the recipient to think about it; thinking hard makes the giver feel closer\[46\]\[47\]\[48\] | Zhang and Epley 2012 (pre-2023, A) | Make the giver's thought legible (their words, the specific memory). The intake itself is a benefit to the giver: it makes them feel closer, which feeds pride |
| Gifts preselected with AI help are seen as less thoughtful because they signal less effort; the gap shrinks when givers explain the attributes they chose\[49\] | "The Gift of Choice?", Psychology & Marketing, Dec 2024 (A) | Visible giver input ("Made by Sam, who remembered…") counteracts the AI-effort penalty |
| Givers overestimate how much late gifts harm relationships\[50\] | Haltman et al., JCP 2025 (A) | A "belated" uncard is a legitimate occasion. Don't shame late givers |

##### 6. Trust, taste and the AI penalty

- **Disclosure penalty.**
  - Jiaqi Zhu and Andras Molnar (University of Michigan; Computers in Human Behavior, 2026; 1,300+ US participants aged 18–84) found a clear "AI disclosure penalty": senders whose messages were known to be AI-made were rated "lazy," "insincere," "lack of effort." When authorship wasn't disclosed, impressions were just as positive as for human-written messages.
  - An Ohio State study by Bingjie Liu, Jin Kang and Lewen Wei (Journal of Social and Personal Relationships, 2024; 208 adults) found friends who used AI help were seen as spending less effort on the relationship; as Liu put it, "people feel less satisfied with their relationship with their friend and feel more uncertain about where they stand." The penalty also applied when another human helped.
  - Kirk and Givi (Journal of Business Research, October 16, 2024) found AI-written emotional messages triggered moral disgust.\[51\]
  - Khadpe, Wenzel, Loewenstein and Kaufman (arXiv:2509.09645, AIES 2025) found "messages labeled as AI-assisted are viewed as less diagnostic of the sender's moral character," and "an AI-assisted apology makes the sender appear less warm."
- **Givers feel it too.** Hass et al. (Journal of Consumer Behaviour, 2026, A) found that passing off AI messages as one's own causes guilt, "driven by perceived dishonesty." The guilt also arose when a friend secretly wrote the message, "but not when it comes on a pre-printed greeting card."\[52\] That is the most useful finding in this report for positioning: honest crafted-gift framing, like a printed card, avoids the dishonesty trap that ghostwriting falls into. A Zeta Global survey of 2,000 US adults who use AI weekly (Business Wire, October 28, 2025; vendor survey, C) found "62% would not tell a loved one if AI helped them select the perfect gift." Hiding AI is what people tend to do, and it is what produces guilt and the risk of discovery.
- **Creepiness.**
  - Personalization turns creepy when it uses data the person didn't knowingly give. Hanson, Wei, Veys, Kugler, Strahilevitz and Ur (CHI 2020, pre-2023; 25 in-person and 280 online participants) found hyper-personalized ads built on out-of-context data provoked strong negative reactions: "Participants reacted negatively to the personalized ad, yet answered nearly all invasive questions accurately."
  - A 2024 arXiv legal analysis notes that consumers find covertly personalized ads "intrusive," "creepy," and "annoying."\[53\]
  - A study in Internet Research ("Antidote for the personalization-privacy paradox," DOI 10.1108/INTR-08-2023-0672) found algorithm literacy reduced privacy concerns for highly personalized advertising, with literate consumers showing higher click intention "when algorithms were transparent," and that transparency was the more effective of the two.
  - For uncard: personalize only from what the giver typed, and show where each detail came from.
- **Quality failures that kill trust.**
  - A Suno reviewer on Trustpilot reports that Suno "added its own verbiage into lyrics," including one line about children eating hot coals (undated).\[54\]
  - StoryWorth's Trustpilot summary flags editing "without an easy undo option."\[55\]
  - A Cameo reviewer on Trustpilot (February 8, 2026) said the message was "really poor. Couldn't send it on to the person."\[56\]
  - Invented facts and unwanted content are the failures to guard against first.

##### 7. What reviews say people praise and hate

Review collection for this report covered the US App Store, Trustpilot and Google Play. Trustpilot pages that don't invite reviews skew negative;\[56\]\[57\] app-store ratings run far higher.
- **Praise centers on the recipient's reaction and on being understood.**
  - JibJab, App Store, May 26, 2023: "they'll sit there and giggle laugh."\[58\]
  - Suno, App Store: "The song produced for me by Suno in less than a minute bordered on the miraculous--perfectly expressing my feelings."\[59\]
  - Cameo, App Store: "we were NOT disappointed."\[60\]
- **Complaints center on surprise costs at the end.**
  - Paperless Post, Trustpilot: "spent hours creating an invite, after which it tried to charge me an exorbitant amount."\[57\]\[61\]
  - Paperless Post, Trustpilot, July 29, 2026: a "ridiculous coins system."\[57\]
  - JibJab, Trustpilot, January 12, 2026: "I was told I was paying 3 dollars a month. a bill came for 36."\[62\]
  - Suno, App Store: "$8/month… the charge came through as $96."\[63\]
- **Other complaints:** template sameness ("the same 50 or so videos," JibJab on Google Play),\[64\] delivery failures for recipients (Paperless Post, July 23, 2026: "unable to open it"),\[57\]\[65\] and missed dates (Cameo, February 2026).\[56\]
- **Ratings:**
  - StoryWorth: 4.7 on Trustpilot from about 65,000 reviews.\[55\]\[66\]
  - JibJab: 4.8 on the App Store from 263,000 ratings, against 1.6 on Trustpilot.\[58\]\[67\]
  - Cameo: 4.9 on the App Store from 48,000 ratings, against 1.9 on Trustpilot.\[56\]\[68\]

#### The 10 Highest-Impact Recommendations (ranked)

**1. Make "one thing only you'd know" the heart of intake, follow up once on the giver's own words, and quote the giver in the uncard.**
- **What:** Use 2–3 open, scene-seeking questions. Generate one follow-up from the most concrete detail in each answer. Render at least one verbatim giver phrase in the uncard, with attribution ("in Sam's words").
- **Evidence:** Givi and Galak 2017 (A, pre-2023). "The Gift of Choice?" 2024 (A): giver-supplied information reduces the thoughtfulness penalty.\[49\] Zhang and Epley 2012 (A, pre-2023): thought must be made salient. Oral-history guides (C).
- **Expected effect:** no data on completion. Expected to raise pride and recipient appreciation the most of any change.
- **Effort:** M.
- **Test:** A/B a fixed second question against a generated follow-up. Measure specificity of answers (count of proper nouns, quotes and sensory words), giver pride, and preview-to-paid.

**2. Cap required intake at three substantive turns, about 2.5 minutes, and move everything else after the preview.**
- **What:** Two tap turns (who and occasion, tone) and three short open-text turns, with any of them skippable. Add-ons ("add a memory," "add a photo," "invite family") appear after the first preview.
- **Evidence:** SurveyMonkey, 100,000 surveys (A, pre-2023). Quiz benchmarks (C). Onboarding drop-off of 20–35% per screen (UXCam, C).\[4\]
- **Expected effect:** each removed step plausibly saves 5–30% of the people who reach it, with a wide range (vendor data, C). No uncard-specific data.
- **Effort:** S.
- **Test:** 3 against 5 required open turns. Measure start-to-preview and an answer-specificity score. Choose the version with the best product of completion and pride, not completion alone.

**3. Position uncard as an honest crafted gift: the giver is the author, uncard is the studio.**
- **What:**
  - The recipient sees "from Sam," with a small, unapologetic "made with uncard" credit, much as a card names its publisher.
  - Never present AI-generated personal sentiment as a handwritten note. Offer a short "your own words" note that the giver types or approves line by line.
  - Never claim "Sam wrote this."
- **Evidence:** Zhu and Molnar 2026 disclosure penalty. Liu et al. 2024. Kirk and Givi 2024. Hass et al. 2026: dishonesty drives guilt, but pre-printed cards don't (all A).\[52\]
- **Expected effect:** no direct data. The downside it prevents is large: discovery of hidden AI damages both the gift and the relationship.
- **Effort:** S.
- **Test:** Recipient-side survey experiment rating two otherwise identical uncards for thoughtfulness: one with visible giver quotes and the credit, one generic.
- **Flag:** concealing AI risks giver guilt and recipient distrust. Leave the honest credit in.

**4. Turn the generation wait into visible work on the giver's material.**
- **What:**
  - Show a determinate progress bar with named stages that use their content, e.g. "Writing the road-trip scene," "Teaching the dog to dance," "Rhyming 'Maya' (hard!)."
  - Stream the first finished scene as soon as it's ready.
  - Offer an optional, never-required micro-choice during the wait, such as picking a color.
  - Announce stages to screen readers.
- **Evidence:** Buell and Norton 2011 (A, pre-2023). Buell et al. 2017, 22.2% higher customer-reported quality (A, pre-2023).\[23\] NN/g on progress indicators (B). The visible builds in Gamma and Suno (C).\[26\]\[69\]
- **Expected effect:** no data for generative waits specifically. The labor-illusion studies suggest a longer, transparent wait can beat a shorter, opaque one.\[21\]
- **Effort:** M.
- **Test:** Spinner against staged progress plus streaming. Measure abandonment during generation and pride.

**5. Add a 10-second "Here's what I heard" recap before generating.**
- **What:** Show a card listing the details uncard will use (name, the memory, the phrase, the tone), each editable in place, with one "Make it" button.
- **Evidence:** Gamma's outline-first checkpoint (C).\[27\]\[28\]\[70\] Oral-history practice of reflecting back (C).
- **Expected effect:** fewer wasted generations and fewer "that's wrong" edits. No data.
- **Effort:** S.
- **Test:** With and without the recap. Measure correction edits after the preview and time to an accepted preview.

**6. Make editing feel like steering, and make every edit succeed.**
- **What:**
  - One-tap tone chips: "more heart," "more roast," "shorter," "sillier."
  - Per-scene "swap this scene."
  - A plain-language box ("make the dog a cat").
  - "Surprise me."
  - Always-visible undo and version history.
  - Apply edits locally where possible, scene by scene, not as a full regeneration.
- **Evidence:** IKEA meta-analysis d = 0.57, with ownership as the mediator (A, 2025). Failed or destroyed work kills the effect (Norton et al. 2012, A, pre-2023).\[33\] Mehler et al. 2024 (A/B).\[34\] StoryWorth's "no easy undo" complaints (C).\[55\]\[71\]
- **Expected effect:** no data on conversion. Expected to lift pride.
- **Effort:** M–L.
- **Test:** Measure pride and paid conversion by number of edits (0, 1–3, 4+). If 4+ correlates with lower pride, edits are failing, so fix edit quality.

**7. Put the price up front, take no account and no subscription before payment, and offer wallet pay.**
- **What:**
  - Show "$5.99 when you love it" (or the final price) on the landing page and on the preview.
  - Build and preview with no login.
  - Offer Apple Pay or Google Pay first.
  - Create the account after payment, only to manage the link.
  - Make the two-a-month plan an explicit, clearly priced choice, never a default.
- **Evidence:**
  - Baymard 2024 (B): the average checkout has 11.3 fields while most need about 8, and 17% of shoppers have abandoned over complexity.\[72\]
  - Baymard data summarized by Dextora: 18% have abandoned over forced accounts.\[73\]
  - Review complaints about end-of-flow price shock at Paperless Post, JibJab and Suno (C).
- **Expected effect:** Baymard estimates large sites could gain up to 35% in conversion from checkout UX fixes overall (B).\[74\]\[75\] No uncard-specific data.
- **Effort:** S–M.
- **Test:** Price shown on landing against price shown at the paywall. Measure start rate, preview-to-paid and refund or complaint rate.

**8. Run quality gates before any preview is shown.**
- **What:** Automated checks against a brief built from the giver's answers:
  - Every scene uses at least one giver detail.
  - No invented biographical facts (names, events, relationships) that the giver didn't provide.
  - Tone matches the chosen setting.
  - Safety and child-appropriateness filters, plus profanity or roast limits when the recipient is a child or a colleague.
  - Names spelled exactly as typed.
  - Games are winnable and the page renders on a small screen.
  - If a gate fails, regenerate silently within the time budget.
- **Evidence:** Suno's inserted-lyrics complaint and Cameo's "really poor" message (C).\[54\]\[56\] Using a second model as critic is common practice (no public benchmark found).
- **Expected effect:** fewer "this is wrong" edits and refunds. No data.
- **Effort:** M.
- **Test:** Track gate failure rate, the share of previews needing a factual correction, and pride.

**9. Personalize only from what the giver typed, and make that visible and controllable.**
- **What:**
  - No scraping of social profiles. No inferred details.
  - A "where this came from" view on the recap.
  - A per-detail "keep this between us" toggle for details used to set tone but never shown to the recipient.
  - Recipient pages are unlisted, with no indexing.
  - For children, collect the minimum needed (first name, age band) from the adult giver only.
- **Evidence:** CHI 2020 study on out-of-context hyper-personalization (pre-2023, A).\[76\] The 2024 arXiv analysis of covert personalization (C).\[53\] Internet Research on algorithm transparency (A).\[77\] FTC amended COPPA Rule: published April 22, 2025, effective June 23, 2025, compliance by April 22, 2026, per FTC releases and law-firm summaries of the Federal Register notice.\[78\]\[79\]
- **Expected effect:** protects trust. No conversion data.
- **Effort:** S–M.
- **Flag:** privacy risk. Kids' uncards need legal review under COPPA, especially if a recipient experience could be considered directed to children.

**10. End on a high-five moment, then a one-tap send and a peek at what the recipient will see.**
- **What:**
  - After payment, show a short celebration in the uncard brand voice ("Maya is going to lose it"), then a share sheet with the link.
  - Offer a "see it as Maya will" preview.
  - Ask one pride question (1–5) and "Make another for someone?" with the next occasion.
- **Evidence:** Mailchimp's high five. Aarron Walter describes an "anxiety leading up to it, then joy" journey, and users "started to high five their computer screens" (practitioner case, B/C).\[80\]\[81\] Haltman et al. 2025 supports offering "belated" uncards without guilt.
- **Expected effect:** no data. Expected to raise "would make another."
- **Effort:** S.
- **Test:** Celebration on against off. Measure share-link click-through within 10 minutes and 30-day repeat purchase.

#### Proposed Flow: Landing to Paid

Target time from first tap to preview is about 3.5–4 minutes at the median, including generation. Paid within 7 minutes at the median.

| # | Turn | What the giver sees and does | Target time |
|---|---|---|---|
| 0 | Landing in the studio | One line: "Three quick questions, then you'll see the whole uncard. $5.99 if you love it." Big bottom button: "Start." No login. | 5–10 s |
| 1 | Who | "Who's this for?" Name field plus relationship chips (partner, parent, child, friend, colleague, other). Chips sit in the bottom third of the screen. | 10 s |
| 2 | Occasion and tone | Occasion chip (birthday defaults). Tone slider "roast ↔ heart," with "mostly heart" preselected. For a child or colleague the roast end is softened automatically. | 10 s |
| 3 | The specific thing | "Tell me one thing about Maya that only you'd know." Example underneath ("She narrates her cat's thoughts in a British accent"). Starter chips: a habit, a trip, a thing she always says. Mic button. | 40–60 s |
| 4 | The follow-up | Generated from their answer: "A British accent! What's the cat's name, and what does it 'say'?" Skippable. | 30–45 s |
| 5 | One more angle | Relationship-specific question from the bank below (e.g., "What's a moment you were proud of her?"). Skippable. "Add another memory" chip for those who want more. | 30–45 s |
| 6 | Recap | "Here's what I heard": 3–5 editable lines plus tone. Toggle "keep private" per line. Button: "Make Maya's uncard." | 10–15 s |
| 7 | Generation | Staged determinate progress using their details. First scene appears within about 20 s. Full preview at a median of 60 s or less; 120 s ceiling at p90. | 30–90 s |
| 8 | Preview and steer | Full uncard plays. Bottom bar: "More heart / More roast / Shorter / Surprise me." Per-scene "swap," a plain-language box, undo. Optional "Add your own note" (giver-typed). | 1–3 min (optional) |
| 9 | Pay | "Love it? $5.99." Wallet pay first, card second. No account. Plan options shown plainly. | 20–40 s |
| 10 | Celebrate and send | High-five moment, then the share sheet with the link, "See it as Maya will," pride question (1–5) and "Make another?" Account created after the fact, by email link, to manage the uncard. | 15–30 s |

**Tradeoffs behind the design:**
- Turn 4 is the most valuable and the most expensive turn. If funnel data shows a large drop there, make it a tap ("Want to add a detail? Yes / Skip") rather than cutting it.
- Real funnel data from the live generator would change these targets. None was available for this report.

#### Metrics and Starting Targets

There are no public benchmarks for AI gift creation. These targets are reasoned starting points, to be reset after about 500 sessions of real data.

| Metric | Starting target | Basis |
|---|---|---|
| Start-to-preview rate (tapped Start → saw full preview) | ≥ 60% | Short-quiz completion of 65–85% (Outgrow 2025, C),\[3\] discounted for open-text effort |
| Time to first preview (first tap → preview playable) | Median ≤ 4 min; generation p50 ≤ 60 s, p90 ≤ 120 s | NN/g 10-second attention limit; Suno and Gamma generation times of 30–90 s (C)\[24\]\[27\] |
| First scene visible | ≤ 20 s after "Make it" | Streaming pattern used by Gamma (C)\[26\] |
| Edits per uncard | Median 1–2; ≥ 50% of payers make ≥ 1 edit; < 10% make 6+ | IKEA effect needs successful, light effort (A). Heavy editing signals poor first drafts |
| Preview-to-paid rate | ≥ 25% to start, goal 40% | No benchmark found; set internally |
| Giver pride (1–5, asked after send) | Mean ≥ 4.3; ≥ 60% answering 5 | No benchmark; internal |
| "Would make another" (yes/no) | ≥ 70% yes | No benchmark; internal |
| Factual-correction edits | < 15% of previews | Quality-gate health; internal |

Instrument drop-off per turn, not only overall. Several vendors observe that one step usually does most of the damage.\[82\]\[83\]

#### 25 Intake Questions by Relationship

Every question was checked against four rules drawn from the oral-history guides and the sentimental-gift research. It must be open (not yes/no). It must ask for a scene, a quote or a sensory anchor rather than a summary. It must be answerable in one or two sentences on a phone. It must not require information the giver might not know. After any answer, uncard asks one follow-up on its most concrete detail.

**Partner**
1. Tell me about a moment early on when you thought, "oh no, I really like this person."
2. What's something they say so often you could do the impression?
3. Describe a perfectly ordinary day together that you'd happily repeat forever.
4. What's a small thing they do for you that nobody else notices?
5. What's the running joke only the two of you get?

**Parent**
6. What's a phrase of theirs you've caught yourself saying?
7. Tell me about a time they showed up for you when it mattered.
8. What did your kitchen, car or house sound or smell like growing up because of them?
9. What's their signature move: the dance, the dish, the dad joke?
10. What's something they taught you without meaning to?

**Child** (the giver is the parent or relative; no data is collected from the child)
11. What are they completely obsessed with right now?
12. Tell me about something they did this year that made you burst with pride.
13. What's the funniest thing they've said lately, word for word?
14. If they were a superhero, what would their power be, based on what they're actually like?
15. What's a bedtime, car-ride or weekend ritual you two have?

**Friend**
16. How did you two become friends? Give me the actual scene.
17. Tell me about the trip, night out or disaster you still bring up.
18. What would they order, say or do that's completely them?
19. When did they have your back in a way you haven't forgotten?
20. What's the inside joke you'd have to explain for ten minutes?

**Colleague** (kept warm and work-safe; roast is capped by default)
21. What's a moment at work when they saved the day, big or small?
22. What are they known for around the office or on Slack?
23. What's something they do that makes the team better that might go unnoticed?
24. What's their go-to snack, mug, phrase or meeting habit?
25. What do you hope their next year looks like?

**Follow-up templates** (generated from the answer): "What did they say exactly?" / "Where were you?" / "What happened next?" / "What did it look like?"

#### Phones and Access

- **One thumb.** Steven Hoober observed 1,333 people (2013, pre-2023). 49% used one hand, 36% cradled the phone, 15% used two hands, and most tapping was done with the thumb.\[84\]\[85\] Keep every primary action and chip in the bottom third. Put edit chips in a bottom bar. Never require a top-corner tap to continue.\[86\]\[87\]
- **Screen readers.**
  - Each chat turn should be a heading with a labelled input.
  - Generation stages should be announced through a polite live region, rather than relying on animation alone.
  - The uncard itself needs a text or story mode that conveys every scene, and games need a non-timed, non-visual way to "win" or skip.
  - Respect reduced-motion settings.
  - The W3C's WCAG 2.2 (October 2023) sets a 24×24 CSS-pixel minimum target size. Chips should be well above it.
  - **Flag:** if games lack alternatives, a blind recipient is left with extra work or locked out.
- **Second-language writers.**
  - Accept input in any language and let the giver choose the uncard's language separately, including bilingual uncards.
  - Keep questions short and literal, with an example under each.
  - Don't "correct" a giver's phrasing when quoting it unless they ask. Their exact words are the evidence of thought.
  - Voice input helps here too.

#### Kids and Families

- **When the recipient is a child:**
  - Use age-band templates (reading level, length, game difficulty).
  - Default to "heart," with gentle silliness and no roast.
  - Filter strictly for content.
  - Collect only a first name and age band, from the adult.
  - Prefer read-aloud or audio so pre-readers can enjoy it with a parent.
  - The amended COPPA Rule (effective June 23, 2025; compliance by April 22, 2026)\[78\] makes legal review essential before launching child-recipient uncards. **Flag:** privacy risk.
- **When several family members contribute:**
  - Remento's model, where family "contribute questions and vote on future prompts," shows group contribution works in this category.\[17\]
  - For uncard, the organizer completes the core flow alone and gets the preview first. Then they can optionally share an "add your memory" link: one question, no login, a 24–72 hour window, with each contribution becoming a scene or a quote.
  - Never block the gift on contributors.
  - **Flags:** this adds work for contributors, though not for the recipient. It also needs moderation and a privacy toggle, because one relative may share something another wouldn't want shown.

#### Delight Moments: What to Borrow

Only the Mailchimp case was verified in this research. The other entries come from first-hand product observation and are unverified (grade C).

| Product moment | Fit for uncard | Cost to the giver |
|---|---|---|
| Mailchimp high five on send: celebrates relief after effort (Aarron Walter)\[81\] | Strong: a branded "they're going to love this" beat after payment | None (under 2 s) |
| Spotify Wrapped-style story cards: personal facts in shareable vertical frames | Strong for the recipient's "your uncard" share card, which they can post if they choose | None for the giver; optional for the recipient |
| Duolingo-style micro-celebrations on completing a step | Light touch on finishing intake ("That's the good stuff") | None, if kept under 1 s |
| Headspace-style calm animation during waits | Good inspiration for the generation screen, combined with staged progress | None |
| Apple setup's multilingual "hello" | A greeting in the recipient's name, in the chosen language, on the reveal | None |
| Airbnb-style warm, specific microcopy | Name-aware copy throughout ("Maya's uncard") | None |

Delight must never sit in the path: no unskippable animations and no confetti before the preview.

#### Things to Avoid

- Pretending the giver wrote AI-generated sentiment, or hiding uncard's role. That is the documented source of giver guilt and recipient distrust.
- Inventing facts, memories or relationships the giver didn't provide.
- Charging at the end after a free build without saying the price up front, defaulting to subscriptions, or using a coin system.
- Requiring login before preview.
- More than three required open questions before the first preview.
- Personalizing from scraped, inferred or other-context data. **Flag:** privacy risk.
- Generic summary questions ("Describe your mom"). They produce generic uncards. **Flag:** template risk.
- A fixed scene catalogue visible across uncards, such as the same jokes or the same game with the name swapped. Reviewers punish "the same 50 or so videos."\[64\] **Flag:** template risk.
- Recipient-side friction: an app, a login, a heavy download, or games that must be won to see the message. **Flag:** recipient work.
- Edits that regenerate everything and lose what the giver liked.
- Roast defaults for children or colleagues.

#### Caveats

- Several anchor findings come from before 2023: Flynn and Adams 2009, Gino and Flynn 2011, Zhang and Epley 2012, Norton et al. 2012, Buell and Norton 2011, Hoober 2013, and SurveyMonkey's 2009–2010 data. Newer support exists for the IKEA effect (the 2025 meta-analysis, Mehler 2024) and the sentimental-gift mismatch (Givi et al. 2023 review). The price-appreciation and requested-gift findings were not re-tested here.
- No study directly measures recipient reactions to AI-crafted interactive cards. The AI-penalty studies concern messages and gift selection, and uncard sits between those and a pre-printed card.
- Drop-off figures for quizzes and onboarding are vendor benchmarks (grade C) from tap-based flows.
- Review quotes marked "preview only" during collection should be re-checked before external use. Trustpilot samples skew negative for companies that don't invite reviews.
- Generation times for Suno and Gamma come from third-party guides, not the companies.
- No uncard funnel, generation-time or edit data was available. Real time-to-preview and per-turn drop-off would most change recommendations 2, 4 and 6.

#### Sources

1. [Most people do not realize when a personal message they receive was written by AI, study finds](https://theconversation.com/most-people-do-not-realize-when-a-personal-message-they-receive-was-written-by-ai-study-finds-278874)
2. [Does Adding One More Question Impact Survey Completion Rate?](https://www.surveymonkey.com/curiosity/survey_questions_and_completion_rates/)
3. [Quiz Engagement Benchmarks: What is a Good Completion Rate?](https://outgrow.co/blog/quiz-engagement-benchmarks-completion-rates)
4. [Drop-Off Rate: Formula, Benchmarks, and How to Diagnose it](https://uxcam.com/blog/drop-off-rates/)
5. [How to Fix Ecommerce Quiz Funnel Drop Off in 2026](https://www.convertflow.com/blog/how-to-fix-ecommerce-quiz-funnel-drop-off-in-2026)
6. [Cameo - Personal celeb videos - Apps on Google Play](https://play.google.com/store/apps/details?id=com.baronapp.cameo&hl=en&gl=US)
7. [How to Do Oral History](https://siarchives.si.edu/history/how-do-oral-history)
8. [oral history resources interviewing](https://home.nps.gov/articles/000/oral-history-resources-interviewing.htm)
9. [Resources for Oral History](https://www.mei.columbia.edu/more-oral-history)
10. [aub.edu.lb.libguides.com](https://aub.edu.lb.libguides.com/OralHistory/BestPractices)
11. [Less Chat, More Answer: Site AI Chatbots Need to Get to the Point - NN/G](https://www.nngroup.com/articles/less-chat-more-answer/)
12. [UX & Usability Articles from Nielsen Norman Group - NN/G](https://www.nngroup.com/articles/?apage=53&page=38&vpage=13)
13. [Prompt Controls in GenAI Chatbots: 4 Main Uses and Best Practices - NN/G](https://www.nngroup.com/articles/prompt-controls-genai/)
14. [Practical AI UX Playbook For Websites: Chatbots And Recs](https://spiralscout.com/blog/ai-ux-playbook-for-websites)
15. [Nielsen Norman Group publishes practical chatbot design guidelines](https://ultimatedesigntools.com/blog/wire-nng-chatbot-guidelines/)
16. [Storyworth FAQs](https://welcome.storyworth.com/frequently-asked-questions)
17. [Frequently asked questions (FAQ)](https://www.remento.co/faq)
18. [Storyworth Reviews](https://au.trustpilot.com/review/storyworth.com)
19. [Response Time Limits: Article by Jakob Nielsen - NN/G](https://www.nngroup.com/articles/response-times-3-important-limits/)
20. [Progress Indicators Make a Slow System Less Insufferable - NN/G](https://www.nngroup.com/articles/progress-indicators/)
21. [The Labor Illusion: How Operational Transparency Increases Perceived Value](https://pubsonline.informs.org/doi/10.1287/mnsc.1110.1376)
22. [The Labor Illusion: How Operational Transparency Increases Perceived Value - Article - Faculty & Research - Harvard Business School](https://www.hbs.edu/faculty/Pages/item.aspx?num=40158)
23. [This article was downloaded by: \[165.124.85.81\] On: 28 August 2023, At: 08:55](https://www.kellogg.northwestern.edu/faculty/bray/doc/transparency/transparency.pdf)
24. [Suno AI Explained: Pricing, Licensing, and How It Works (2026)](https://www.layer3labs.io/guides/suno-explained)
25. [How long will my song be?](https://help.suno.com/en/articles/13924929)
26. [How to Create a Professional AI Presentation in Gamma in Under 10 Minutes](https://www.mindstudio.ai/blog/create-professional-ai-presentation-gamma-under-10-minutes)
27. [How to Use Gamma AI to Build Presentations from Scratch: A Step-by-Step Tutorial](https://www.mindstudio.ai/blog/how-to-use-gamma-ai-build-presentations-tutorial)
28. [How to Use Gamma AI for Business Presentations: A Step-by-Step Guide](https://www.mindstudio.ai/blog/how-to-use-gamma-ai-business-presentations)
29. [Udio](https://en.wikipedia.org/wiki/Udio)
30. [Labor Leads to Love, Right? A Meta‐Analysis of the IKEA Effect - Pelled - 2026 - Psychology & Marketing - Wiley Online Library](https://onlinelibrary.wiley.com/doi/10.1002/mar.70064)
31. [When labor leads to persuasion: The Ikea effect in persuasive texts By](https://asset.library.wisc.edu/1711.dl/JID6TZKYVT67P8N/R/file-a31f1.pdf)
32. [The IKEA effect: When labor leads to love Citation](https://dash.harvard.edu/bitstreams/7312037d-2473-6bd4-e053-0100007fdf3b/download)
33. [IKEA effect — Grokipedia](https://grokipedia.com/page/IKEA_effect)
34. [AIS Electronic Library (AISeL) - ECIS 2024 Proceedings: The Influence of Effort on the Perceived Value of Generative AI: A Study of the IKEA Effect](https://aisel.aisnet.org/ecis2024/track09_coghbis/track09_coghbis/6/)
35. [The IKEA effect in human-AI collaboration. Part I.](https://msijournal.com/the-ikea-effect-in-human-ai-collaboration-does-the-effect-exist-for-non-physical-products-part-i/)
36. [(PDF) The IKEA effect in human-AI collaboration: Does the effect exist for non-physical products? Part I.](https://www.researchgate.net/publication/397976398_The_IKEA_effect_in_human-AI_collaboration_Does_the_effect_exist_for_non-physical_products_Part_I)
37. [Frontiers](https://www.frontiersin.org/journals/psychology/articles/10.3389/fpsyg.2026.1823846/full)
38. [Give Them the Gift They're Expecting](https://www.gsb.stanford.edu/insights/give-them-gift-theyre-expecting)
39. [(PDF) Gifts and Money Pollmann draft](https://www.researchgate.net/publication/343765727_Gifts_and_Money_Pollmann_draft)
40. [Give them what they want: The beneﬁts of explicitness in gift exchange](https://static1.squarespace.com/static/55dcde36e4b0df55a96ab220/t/55e746dee4b07156fbd7f6bd/1441220318875/Gino+Flynn+JESP+2011.pdf)
41. [It's the thought that counts…](https://brandforlife.wordpress.com/2012/12/14/its-the-thought-that-counts/)
42. [Let's Talk Business: Julian Givi Shares Gift-Giving Insights](https://business.wvu.edu/news-and-events/news/2023/05/09/guest-blog-julian-givi)
43. [Secret to giving the perfect gift: Stop being afraid](https://www.sciencedaily.com/releases/2017/07/170725100701.htm)
44. [Want to Give a Good Gift? Think Past the “Big Reveal”](https://www.psychologicalscience.org/news/releases/good-gift-givers-think-beyond-the-big-reveal.html)
45. [Carnegie Mellon University](https://www.cmu.edu/piper/news/archives/2016/december/gifting-errors.html)
46. [\[PDF\] Exaggerated, mispredicted, and misplaced: when "it's the thought that counts" in gift exchanges.](https://www.semanticscholar.org/paper/Exaggerated,-mispredicted,-and-misplaced:-when-the-Zhang-Epley/b1f9e16ae8af3e1a0714749e962b05a152d0f229)
47. [ERIC - EJ993742 - Exaggerated, Mispredicted, and Misplaced: When "It's the Thought That Counts" in Gift Exchanges, Journal of Experimental Psychology: General, 2012-Nov](https://eric.ed.gov/?id=EJ993742)
48. [What the brain wants for Christmas](https://edition.cnn.com/2012/12/21/health/psychology-holiday-giving)
49. [(PDF) Gift giving in the age of AI: The role of social closeness in using AI gift recommendation tools](https://www.researchgate.net/publication/381189620_Gift_giving_in_the_age_of_AI_The_role_of_social_closeness_in_using_AI_gift_recommendation_tools)
50. [Better late than never? Gift givers overestimate the relationship harm from giving late gifts - Haltman - 2025 - Journal of Consumer Psychology - Wiley Online Library](https://myscp.onlinelibrary.wiley.com/doi/abs/10.1002/jcpy.1446)
51. [Are Messages From Robots Trustworthy?](https://www.nyit.edu/news/articles/do-customers-perceive-ai-written-communications-as-less-authentic/)
52. [AI Ghostwriting Remorse: Guilt for Using Generative AI in Interpersonal Heartfelt Messages - Hass - 2026 - Journal of Consumer Behaviour - Wiley Online Library](https://onlinelibrary.wiley.com/doi/10.1002/cb.70057)
53. [Consumer Manipulation via Online Behavioral Advertising](https://arxiv.org/pdf/2401.00205)
54. [Suno Reviews](https://ca.trustpilot.com/review/suno.com?page=3)
55. [Storyworth Reviews](https://www.trustpilot.com/review/storyworth.com)
56. [Cameo is rated "Poor" with 1.9 / 5 on Trustpilot](https://www.trustpilot.com/review/cameo.com?page=2)
57. [Paperlesspost is rated "Bad" with 1.6 / 5 on Trustpilot](https://ca.trustpilot.com/review/paperlesspost.com?page=2)
58. [JibJab: Funny Ecards, GIFs, AI - Ratings & Reviews - App Store](https://apps.apple.com/us/app/jibjab-funny-ecards-gifs-ai/id875561136?see-all=reviews&platform=iphone)
59. [Suno - AI Songs, Music, Lyrics - Ratings & Reviews - App Store](https://apps.apple.com/us/app/suno-ai-songs-music-lyrics/id6480136315?see-all=reviews)
60. [Cameo - Personal celeb videos - Ratings & Reviews - App Store](https://apps.apple.com/us/app/cameo-personal-celeb-videos/id1258311581?see-all=reviews)
61. [Paperlesspost Reviews](https://nz.trustpilot.com/review/paperlesspost.com)
62. [JibJab Reviews](https://au.trustpilot.com/review/www.jibjab.com)
63. [Suno - AI Songs, Music, Lyrics - App Store - Apple](https://apps.apple.com/us/app/suno-ai-songs-music-lyrics/id6480136315)
64. [JibJab: Funny Birthday Cards - Apps on Google Play](https://play.google.com/store/apps/details?id=com.jibjab.android.messages.fbmessenger&hl=en_US)
65. [Paperlesspost Reviews](https://au.trustpilot.com/review/paperlesspost.com)
66. [Storyworth reviews 2026: the complaints that actually recur · Yourtale](https://www.yourtale.art/en/blog/storyworth-reviews)
67. [JibJab Reviews](https://www.trustpilot.com/review/www.jibjab.com)
68. [Cameo - Personal celeb videos - App Store - Apple](https://apps.apple.com/us/app/cameo-personal-celeb-videos/id1258311581)
69. [How to Make a Song with Suno: Create Songs With a Few Clicks](https://suno.com/hub/how-to-make-a-song)
70. [How to Use Gamma AI to Create Professional Presentations in Minutes](https://www.mindstudio.ai/blog/how-to-use-gamma-ai-create-professional-presentations)
71. [Storyworth Reviews](https://uk.trustpilot.com/review/storyworth.com?page=3)
72. [Checkout Optimization: Minimize Form Fields](https://baymard.com/blog/checkout-flow-average-form-fields)
73. [The Checkout That Loses 35% of the Revenue: A Breakdown of the Baymard Data](https://dextora.agency/en/insights/checkout-that-loses-revenue-what-baymard-data-shows/)
74. [What Percentage of Online Shoppers Abandon Carts in 2026?](https://redstagfulfillment.com/percentage-of-online-shoppers-abandon-their-cart/)
75. [Cart Abandonment Rate 2026: 70.22% — Industry & Device ...](https://zerocartai.com/blog/cart-abandonment-statistics-2025)
76. [Taking Data Out of Context to Hyper-Personalize Ads: Crowdworkers’ Privacy Perceptions and Decisions to Disclose Private Information](https://dl.acm.org/doi/fullHtml/10.1145/3313831.3376415)
77. [Antidote for the personalization-privacy paradox: Does algorithm transparency trigger higher ad click-through intention than algorithm literacy?](https://www.emerald.com/intr/article/doi/10.1108/INTR-08-2023-0672/1344288/Antidote-for-the-personalization-privacy-paradox)
78. [Amendments to the FTC COPPA Rule Now in Effect](https://natlawreview.com/article/amendments-ftc-coppa-rule-now-effect)
79. [FTC Announces Significant Amendments to COPPA](https://www.mayerbrown.com/en/insights/publications/2025/04/ftc-announces-significant-amendments-to-coppa)
80. [Transcript: Designing Emotional Experiences with Aarron Walter](https://uxmastery.com/transcript-designing-emotional-experiences/)
81. [Mailchimp — Aarron Walter](https://aarronwalter.com/portfolio/mailchimp)
82. [How to Build a Quiz Funnel That Converts (2026 Guide)](https://uplup.com/blog/how-to-build-a-quiz-funnel)
83. [Onboarding Completion Rate — Guide and Benchmarks](https://onboarding-hub.com/guides/onboarding-completion-rate)
84. [The Thumb Zone: A Practical Guide to Mobile UX/UI Design](https://parachutedesign.ca/blog/thumb-zone-ux/)
85. [Designing for the Thumb Zone: A Modern Guide to Mobile UX That Respects Human Anatomy - Timothy Graf](https://timgraf.com/ux-design/designing-for-the-thumb-zone-a-modern-guide-to-mobile-ux-that-respects-human-anatomy/)
86. [Designing Thumb-Friendly Mobile Interfaces](https://www.themeignite.com/blogs/news/thumb-friendly-mobile-interfaces)
87. [Thumb zone](https://subux.pro/glossary/thumb-zone)

## Open questions

- The built studio interview (`product/live-product.md`) allows up to 16 questions (6 basics + up to 10 more), all skippable; this research recommends capping *required* open turns at three. Not a contradiction since the extra questions are optional, but worth revisiting with real funnel data.
- This doc's checkout/paywall design (price shown up front, wallet pay, no login before payment) is ahead of where the build is allowed to go — `AGENTS.md` still says Stripe is deferred and must not be scaffolded, connected or mocked.
- No mention of the Matinee brand voice (`brand/directions.md`: "uncard, scene, world, your person, give") — this research uses generic terms ("card," "recipient," "sender") throughout, which is expected for third-party research but means none of its sample copy should be used verbatim without a voice pass.
