# Recipient Attention Research

**Status:** Draft
**Updated:** 2026-10-06
**Owner:** Jordan
**Method:** Written by Jordan's research agent and posted by Jordan in Slack #non-build-stuff on 2026-10-02. Ingested as written; the findings were not re-verified here.

## TL;DR

- **Front-load everything.** A real first frame (LCP) within ~2.5s at p75, the recipient's and giver's names on screen within 1s, one clear tap affordance within 3s, and a payoff within 5s of the first tap. The biggest drop-off in every comparable format happens at the very start, not the finale.
- **Default length: 60–120 seconds across 5 to 9 scenes** (hard ceiling 12 scenes / ~3 minutes), scaled by relationship — closer ties run longer and rougher, colleagues shorter and more polished.
- **Design for silence, measure lightly.** Most phone video is watched muted in public; every scene must make full sense with sound off (captions, visual rhythm), with audio unlocked inside the first tap gesture. Respect `prefers-reduced-motion` and WCAG 2.2 throughout.
- **The ending needs three things in order:** a one-tap reply (no signup), "keep this" with the link **kept alive for at least 12 months**, and a quiet, optional "make one for someone" that never blocks the reply.
- **Proposes a "privacy-minimal" analytics event list** (open, first_frame, scene_view, complete, replay, etc.) — counted per uncard rather than per person, no cookies, no fingerprinting, no third-party scripts — citing Quebec's Law 25 and PIPEDA, with legal review still needed before launch.

## Implication for Uncard

- **Scene count is shorter than what's decided.** This research's default length (5–9 scenes) is narrower than `decisions/0005-demo-is-source-of-truth.md`'s resolved "usually 8 to 10 scenes, default 9." That's a direct disagreement between this research and the current build target, not something to quietly split the difference on — see Open questions.
- **Hosting length is shorter than the decided business model.** Ending rule #19 says the link should stay "kept alive for at least 12 months." The wiki's pricing model (`decisions/0002-pricing-model.md`, `product/experience.md`) is 3 months of hosting included, then either a free keepsake download or $3/year to keep the same link live. These are two different economics for the same thing — flagged, not reconciled here.
- **The analytics instinct matches the privacy gate, but the detail goes further.** "Count events per uncard, never per person... no cookies, no fingerprinting, no IP storage, no third-party analytics scripts on uncard.gifts" lines up with `AGENTS.md`'s "Privacy is a hard gate" and `decisions/0006-gifts-on-uncard-gifts.md`'s "no analytics" rule for the gift Worker. But the proposed event list (per-scene dwell time, replay-session buckets, an `a11y_mode` flag) is considerably more granular than "no analytics" as currently written — see Open questions.
- **Skippable games and reduced-motion support already match `product/experience.md`** ("Every game can be skipped") and the Matinee illustration/motion rules in `brand/directions.md` ("Pop, don't wobble... Nothing loops").

## Source document

> The text below is the research file as posted in Slack on 2026-10-02 (`Uncard Holding the Recipient's Attention — Research Findings, Generator Rules and Metrics.md`), reproduced verbatim except for heading levels, which are shifted down so this page has a single top-level heading. Treat its content as the research agent's findings, not as wiki fact — see the header above and the caveats and sources inside it.

### Uncard: Holding the Recipient's Attention — Research Findings, Generator Rules and Metrics

**Date:** October 2026 · **File:** `uncard-recipient-attention-research.md` · **Purpose:** evidence-based rules, ranked recommendations, metrics and analytics events for making every uncard get opened, finished, felt and answered.

An uncard holds attention when it shows a real first frame within about 2.5 seconds on a mid-range phone and reveals something only this giver could know (a name, a specific memory, a friend's voice) within the first three scenes. It should run about 60 to 120 seconds across 5 to 9 scenes, asking for one obvious tap every 8 to 15 seconds. It must make complete sense with the sound off, and it should end with a reply that takes one tap. The biggest drop-off in every comparable format happens at the very start, so most of the effort belongs in the preview and the first five seconds, not the finale.

#### TL;DR

- **Front-load everything.** Socialinsider analysed 161,180 brand Instagram Stories from January–May 2024 and January–May 2025. Nearly one viewer in four (23.8%) left on the first frame, and exits fell to about 13% by frame 9. Akamai's Spring 2017 retail report cites an outside source finding that 53% of mobile visitors leave a page that takes longer than 3 seconds to load. The rules that follow from this: a real first frame (LCP) within 2.5 s at p75, a personal reveal by scene 2, and a first tap within 5 s.
- **Personal beats polished.** Peer-reviewed work shows recipients like a gift from a friend more when the wrapping is less polished (Rixom, Mas & Rixom, *Journal of Consumer Psychology*, 2019). Interactions that include voice create stronger bonds than text, with no added awkwardness (Kumar & Epley, *JEP: General* 150(3), 2021). Senders also badly underestimate how much a message of thanks or contact is appreciated (Kumar & Epley, *Psychological Science*, 2018; Liu et al., *JPSP*, 2022). Specific, voiced, slightly imperfect content should therefore outrank more effects.
- **Design for silence, measure lightly.** Most phone video is watched muted in public: 69% said so in Verizon Media and Publicis Media's April 2019 online survey of 5,616 US adults aged 18–54. Captions and visual rhythm are therefore the primary layer and music is a bonus. There are no public benchmarks for reply rate or "make one back" rate for a no-signup web card, so the starting targets below are labelled assumptions (grade C), to be measured with cookieless, event-only analytics.

---

#### 1. Generator rules

These are the rules the generator applies to every uncard. Where a number has weak sourcing it is marked "assumption".

##### Load and first frame
1. **Load budget.** First frame (LCP) ≤ 2.5 s at the 75th percentile on a mid-range Android on 4G; aim for ≤ 1.6 s. INP ≤ 200 ms. CLS ≤ 0.1.\[1\] Keep the critical payload for scene 1 under about 150 KB compressed (assumption) and stream later scenes, music and games after the first frame paints.
2. **Server-render the first scene and the preview tags.** The first visible frame should be real HTML/CSS with the recipient's name, not a spinner or a black canvas. Never hold scene 1 back waiting for audio, fonts or the game engine.
3. **Preview tags on every uncard.** Static, server-rendered `og:title`, `og:description`, `og:image` (HTTPS, absolute URL, 1200×1200 or 1200×630 with the key content in the centre safe area, JPEG under 1 MB).\[2\]\[3\] Use a per-recipient preview image showing their name and the occasion. Keep the title under about 40 characters, for example "Maya, this one's just for you 🎂". Never reveal the surprise in the preview.

##### First scene (0 to 5 seconds)
4. **Within 1 s:** the recipient's name and the giver's name on screen ("From Sam, for Maya").
5. **Within 3 s:** one clear, animated affordance for the first action, such as "Tap to open" on a wrapped object, with no text instructions longer than one short line.
6. **Within 5 s:** the first tap produces an immediate, satisfying payoff: the unwrap animation starts, and sound starts if allowed.
7. **The "open" gesture is the sound gesture.** The first tap unlocks audio (see the sound rules), so the recipient is never asked about sound as a separate step.

##### Length and structure
8. **Default length: 60 to 120 seconds of content across 5 to 9 scenes** (assumption based on Stories exit curves and playable-ad play lengths). Hard ceiling of 12 scenes and about 3 minutes, unless many friends contributed (see rule 10).
9. **Order:** (1) invitation or unwrap → (2) a personal reveal (photo, memory or voice) → (3 to N−2) a mix of story, mini-game and messages → (N−1) the emotional peak (wish, chorus, song) → (N) keepsake and reply.
10. **Scale with relationship and occasion:**
    - Close friend or partner: 90 to 150 s, inside jokes allowed, rougher and more handmade style.
    - Colleague or acquaintance: 45 to 75 s, a more polished style, no inside jokes needed.
    - Group "chorus" cards: show 3 to 5 messages in full, then offer the rest as a browsable wall the recipient can open, not a forced sequence.
    - Holidays and New Year (sent to many people): 30 to 60 s.
11. **Always show progress** (dots or a thin bar) and allow free tap-forward and back, as Stories do. Never trap the viewer.

##### Interaction rhythm
12. **One meaningful input every 8 to 15 seconds** (assumption), always one gesture type at a time (tap first; drag or choose later). No input should take more than 2 attempts. Any mini-game auto-resolves after 15 to 20 s or 3 failed tries.
13. **Every input changes something visibly within 100 ms** and moves the story forward. Never ask for a tap just to keep going when an auto-advance would do.
14. **Never require typing, an account, a payment or a permission prompt before the ending.**

##### Sound
15. **Start muted-safe.** Every scene must make full sense with sound off: burned-in captions for any voice, lyric lines for songs, and visual beat pulses (scale or glow under 3 flashes per second) timed to the music.
16. **Unlock audio inside the first tap handler.** Create or resume the AudioContext synchronously in that gesture. Keep a speaker toggle always visible, start at a moderate volume, never auto-play loud music, and fade in over about 1 s.
17. **Honour the iPhone silent switch by default.** Don't use tricks to force audio through silent mode on first open. Show a small "🔇 Sound makes this better: turn off silent mode" hint only on scenes that carry voice or song.

##### Access and comfort
18. Respect `prefers-reduced-motion` by swapping parallax, zoom and confetti for fades.\[4\] Never flash more than 3 times in any second. Provide pause for any motion longer than 5 s.\[5\] All text should meet 4.5:1 contrast. Never use colour alone to convey a game state. Provide a screen-reader path with a text transcript of every scene, ARIA live captions and focusable controls of at least 24×24 px.

##### Ending
19. **The last screen holds three things, in this order:** (a) one-tap reply options (a quick reaction, a short text, or a 10-second voice note, all without signup); (b) "Keep this" (save image or bookmark the link, with the link kept alive for at least 12 months); (c) a quiet, optional "Make one for someone" that never blocks the reply.
20. **Replay** must start instantly from cache and skip the unwrap delay the second time.

---

#### 2. The 10 highest-impact recommendations (ranked)

| # | Recommendation | Evidence grade | Expected effect | Effort | How to test |
|---|---|---|---|---|---|
| 1 | Hit a first frame within 2.5 s at p75 (target 1.6 s) with server-rendered scene 1 | A/B (Akamai Spring 2017 report: 27.7B beacons, about 10B visits to leading retail sites over one month; web.dev case studies) | Biggest single lever on whether people start at all; Renault saw a 14-point bounce drop per 1 s of LCP improvement below 1.6 s\[6\] | M | Real-user monitoring of LCP; A/B a lean versus heavy scene 1, comparing start rates |
| 2 | Per-recipient preview image and title (name plus occasion, surprise hidden) | C (platform documentation and vendor guides; no public A/B data for greeting cards) | Higher and faster tap-through from iMessage and WhatsApp | S | A/B a generic versus personal OG image; measure the open rate within 1 h and 24 h |
| 3 | A personal reveal (photo, memory or voice) by scene 2 | A (Socialinsider exit curve; nostalgia and autobiographical-memory research) | Cuts early exits, which are the largest loss point\[7\] | S | Compare the drop-off at scenes 1 to 3 against a generic-intro control |
| 4 | One obvious tap affordance within 3 s, with immediate payoff | B/C (playable-ad vendor data: a 3 s versus 4 s time to first interaction raised engagement from 72.6% to 82%)\[8\] | Faster first interaction and a higher rate of reaching scene 3 | S | Measure the time-to-first-interaction distribution; test hand-cue versus text prompts |
| 5 | Sound-off-first design (captions plus visual rhythm), with audio unlocked on the first tap | A/B (Verizon/Publicis 2019; Szarkowska et al., PLOS ONE 2024) | Comprehension and completion for the majority who open muted | M | Completion split by audio state; the share who turn sound on |
| 6 | Encourage and record givers' voices (friends' chorus as voice notes, with captions) | A (Kumar & Epley 2021: voice beats text for connection)\[9\] | Stronger "feel seen" scores and more replies | M | A/B voice versus text-only chorus; compare reply rate and a 1-tap "how did it feel" rating |
| 7 | Cap the default at 60 to 120 s and 5 to 9 scenes, scaled by relationship | B (Stories benchmarks; playable-ad 15 to 30 s play windows)\[10\] | Completion at or above 70%\[11\] | S | Completion by scene count; trial 6- versus 9-scene variants |
| 8 | A one-tap reply on the final screen, with voice-note and emoji options and no signup | A/B (Kumar & Epley 2018 on undervalued gratitude; the emoji-responsiveness literature) | Lifts the reply rate; the reply closes the loop for the giver | M | Reply rate by option offered; time from end screen to reply |
| 9 | Full reduced-motion, flash-safe and screen-reader paths | A (WCAG 2.2 normative) | Prevents harm and exclusion; legal risk reduction\[12\] | M | Automated checks plus manual VoiceOver and TalkBack runs on each template |
| 10 | Durable keepsake plus one well-timed "look back" (e.g. a month later or next year), sent by the giver, not to the recipient | B (Spotify Wrapped and Google Photos Memories scale)\[13\] | Replays weeks later without collecting the recipient's contact details | M | Replay rate at 7, 30 and 365 days; return visits from giver-shared resurfacing links |

**Flagged ideas (signup or payment):**
- "Make one back" turns the recipient into a giver, who may then hit uncard's creation signup or payment. The offer must never appear before the reply, must be skippable, and the reply itself must stay free with no account.
- A recorded *video* reaction needs camera permission, and a voice reply needs the microphone. Both must be opt-in, after the experience, never auto-recording.

---

#### 3. Recipient metrics with starting targets

There are no public benchmarks for most of these in a no-signup web greeting-card setting. Kudoboard tracks thank-yous per customer but publishes no aggregate rate.\[14\] Neither Apple nor Meta publishes reaction or reply rates for iMessage or WhatsApp. Targets graded C are assumptions to be replaced after about 500 real deliveries.

| Metric | Definition | Starting target | Grade | Reasoning |
|---|---|---|---|---|
| Open rate | Unique link opens ÷ uncards delivered, within 24 h (track 1 h and 7 d too) | ≥ 80% within 24 h; ≥ 90% within 7 d | C | Personal messages from a known sender are read quickly; SMS marketing claims of about 98% are inferred, not measured, so this target is set lower\[15\] |
| Time to first frame | LCP, p75, mobile | ≤ 2.5 s (stretch ≤ 1.6 s) | A/B | Core Web Vitals "good" threshold; the Renault curve\[1\]\[6\] |
| Time to first interaction | Page start → first deliberate tap, median | ≤ 5 s median; ≤ 10 s p75 | B/C | The playable-ad median is 8.76 s for unguided ads and good tutorials cut it about 40%; an uncard has a single, obvious tap\[8\] |
| Start-to-scene-3 rate | Reached scene 3 ÷ opens | ≥ 85% | C | Stories lose about 24% at frame 1; a personal reveal should beat brand content\[16\] |
| Completion rate | Reached the final screen ÷ opens | ≥ 70% (stretch 80%) | B/C | Instagram Stories averages 70% (Dash Social, 2,000+ brands, H1 2025) to 87% (Flick), depending on method; personal content from a friend should be at the high end |
| Sound-on rate | Sessions with audio unlocked ÷ opens | Track only; expect 30 to 50% | C | Muting is the norm in public (69%) but rarer in private (25%); people open cards in both settings\[17\] |
| Replay rate | Recipients with ≥ 2 sessions ÷ completers, within 30 d | ≥ 25% | C | No benchmark; keepsakes such as Google Photos Memories show strong revisit appetite, but uncards are one-off\[18\] |
| Reply rate | Any reply (reaction, text or voice) ÷ completers | ≥ 50% | C | No public benchmark for e-cards or group cards; the reply is one tap and social norms (72% send thank-yous after gifts, per an AYTM survey) support a high target\[19\] |
| "Make one back" rate | Recipients who start creating an uncard within 30 d ÷ completers | 5 to 10% start; 2 to 4% send | C | No public benchmark exists; it requires the recipient to become a giver (signup or payment), so it is expected to be an order of magnitude below reply |

---

#### 4. Analytics event list (privacy-minimal)

**Principle:** count events per uncard, never per person. Use no cookies, no fingerprinting, no IP storage, and no third-party analytics scripts on uncard.gifts. Use one random, per-load session ID held in memory only (not persisted). The uncard ID is already pseudonymous. Under Quebec's private-sector act (s. 8.1, in force since September 2023), any technology that can identify, locate or profile a person must be off by default, and PIPEDA treats tracking data as personal information.\[20\]\[21\]\[22\] Neither regulator has explicitly ruled on anonymous, cookieless first-party analytics, so get legal review before launch.

| Event | Needed / Optional | Payload (minimum) | Privacy note |
|---|---|---|---|
| `preview_fetched` | Optional | uncard ID, crawler family (iMessage, WhatsApp, etc.) from user-agent | Bot traffic only; drop the IP at the edge |
| `open` | Needed | uncard ID, session ID, timestamp bucketed to the hour, device class (phone, tablet, desktop) | No IP, no precise UA string; device class only |
| `first_frame` | Needed | LCP ms, connection type (4G/Wi-Fi if exposed) | Performance data only; no identity |
| `first_interaction` | Needed | ms since start | Timing only |
| `scene_view` | Needed | scene index, ms dwell | Enough for the drop-off curve; no gaze or scroll heatmaps |
| `interaction` | Optional | scene index, type (tap, drag, choose), success Y/N | Never log free text or choice content tied to the person |
| `audio_state` | Needed | on/off, scene index | Binary only |
| `a11y_mode` | Optional | reduced-motion Y/N, screen reader detected Y/N | Sensitive (it hints at disability). Aggregate only, never shown to the giver, drop after 90 d |
| `complete` | Needed | total ms, scenes skipped count | — |
| `replay` | Needed | session count bucket (2, 3–5, 6+), days since first open bucket | Count via the server-side uncard record, not a device cookie |
| `keepsake_save` | Needed | type (image, link) | — |
| `reply_sent` | Needed | type (reaction, text, voice) | The reply content goes to the giver as the product function; analytics gets the type only |
| `make_one_click` | Needed | — | Attribution via URL parameter on the creator site; no cross-site identifier |
| `error` | Needed | code, scene index, browser family | Strip URLs and stack traces of any personal content |
| `feel_rating` | Optional | 1-tap emoji scale after the reply | Opt-in, shown at most once, never required |

**What the giver sees:** "Opened ✓", "Watched to the end ✓", and the reply. Never show dwell times or replay counts, which would feel like surveillance to the recipient. Recipients should be told in one line at the end that the sender sees opened/finished.

---

#### 5. Things that lose people

- **A blank, spinner or black first screen**, or waiting for music or a game engine before showing anything.
- **A generic preview** (site logo, "uncard.gifts") that looks like spam or marketing.
- **A text wall of instructions** at the start, or a first tap with no obvious target.
- **Sound that blasts on open**, or a story that makes no sense muted.
- **Hard games**, timers, or any input that fails twice in a row.
- **Long forced sequences of friends' messages**, such as 20 tiles shown one by one with no skip.
- **Neat but empty polish**: lots of effects, nothing only this giver could know.
- **Any account, payment, permission or typing request** before the ending.
- **Flashing, parallax or confetti with no reduced-motion path.**
- **"Make one" pushed harder than "say thanks".**

---

#### Findings by question

##### Q1. The open
- iMessage builds its rich preview from Open Graph tags. Third-party guides report Apple's minimum width as 900 px and recommend 1200×1200 as the safest crop across iOS versions (OpenGraph+, 2026; grade C).\[23\] Titles are clipped at about 44 characters (mc.dev, undated; grade C).\[24\]
- Tags must be in server-rendered HTML; previews fail when tags are injected by JavaScript or served over HTTP (OGFixer, 2026; grade C).\[3\]
- In SMS, the preview loads reliably only when the URL sits at the start or end of the message and is the only URL (CelerSMS, undated; grade C).\[25\] The generator's suggested send message should therefore be "[short line] + link", with nothing after the link.
- **Sender framing.** People underestimate how much recipients value being reached out to (Liu, Rim, Min & Min, *JPSP*, July 2022; more than 5,900 participants; grade A). Lead author Peggy Liu (University of Pittsburgh) reported that the underestimate was largest when the contact was more surprising or the tie was weak (APA release, July 11, 2022). Framing such as "made this just for you" signals surprise and effort without revealing the content.
- **Timing.** "98% of SMS opened, 90% within 3 minutes" circulates widely, but MessageFlow (2026) notes it is inferred from delivery and response data, not measured (grade C).\[15\] I found no public data on the best send time for personal links. Default to scheduled delivery at the giver's chosen moment in the recipient's local morning, and let the giver send it themselves where possible.

##### Q2. Load and first seconds
- Core Web Vitals "good" thresholds are LCP ≤ 2.5 s, INP ≤ 200 ms and CLS ≤ 0.1 at p75 (web.dev, current as of 2026; grade A).\[1\]\[26\]
- Akamai's Spring 2017 retail report covered 27.7 billion beacons (about 10 billion visits) over one month on leading retail sites. It found:
  - 53% of mobile visitors leave pages slower than 3 s (a figure the report footnotes to an outside source, not its own data);
  - a 2 s delay raised bounce by up to 103%;
  - 100 ms of delay cut conversion by up to 7% across all devices (grade A, but dated and retail-specific; the effect is non-linear, per Quantable's critique).
- Renault's web.dev case study (10M+ visits, data from December 2020 to March 2021) found 1 s of LCP improvement cut bounce by 14 points when LCP was under 1.6 s, versus 5 points above it (grade B).\[6\]\[26\]
- In other web.dev case studies, The Economic Times cut LCP from 4.5 s to 2.5 s and reduced bounce 43% (2021; grade B).\[27\] NDTV halved LCP alongside other changes and saw bounce fall 50% (grade B, confounded).\[28\]
- Only about 56% of origins pass all three Core Web Vitals (secondary summary of CrUX data, May 2026; grade C),\[1\] so meeting the bar is a real differentiator, not a given.
- In the first 3 to 5 seconds, the playable-ad data says the outcome is mostly decided early. Without guided interaction, median drop-off in the first 3 s is 46.7%, and the median time to first interaction is 8.76 s (sett.ai, 2026; vendor, grade C). A good tutorial cuts that by about 41%, and Stacky Dash's move from a 4 s to a 3 s first interaction lifted engagement from 72.6% to 82% (same source; grade C).\[8\]

##### Q3. Sound
- Verizon Media and Publicis Media's April 2019 online survey of 5,616 US adults aged 18–54 found:
  - 69% watch with sound off in public, versus 25% in private;\[17\]
  - 80% are more likely to finish a video with captions;\[29\]
  - 37% say captions encourage them to turn sound on (grade B; older).\[29\]\[30\]
- Watching subtitled video with the sound off lowers comprehension, immersion and enjoyment, and raises cognitive load (Szarkowska et al., *PLOS ONE*, October 2024; eye-tracking, mixed methods; grade A).\[31\]\[32\] Captions are a fallback, not an equivalent, so music should be an enhancement with visual rhythm carrying the beat.
- On iOS, media with sound needs a user gesture (WebKit, "New video policies for iOS", 2016; grade A as platform documentation).\[33\] Developer reports describe how the ring/silent switch mutes Web Audio unless a media element puts the page into a playback session, and how `navigator.audioSession.type` is available from iOS 17 (GitHub issue threads, 2025–2026; grade C).\[34\]\[35\]
- I found no public figure for the share of interactive-story users who turn sound on. Track it yourself.

##### Q4. Length and pacing
- In Socialinsider's analysis of 161,180 brand Stories (January–May 2024 and January–May 2025), exits were 23.8% at frame 1, 20.5% at frame 2, 18.5% at frame 3, 15.7% at frame 4, 13.3% by frame 9 and about 12.5% at frame 15. Video frames had higher exit rates than images (grade A/B, large sample, vendor-published).
- Average completion is 70% across 2,000+ brands with at least 1K followers, January–June 2025 (Dash Social; 70.5% for 1.1M+ followers, 68.3% under 190K; grade B), versus about 87% across about 15,000 accounts in late 2024 (Flick; grade B). The two methods differ, so treat 70% as the floor.
- Playable ads typically run 15 to 30 s of interactive play with a tutorial of 5 s or less (Segwise, 2026; grade C).\[36\]
- **Implication:** because exits flatten after scene 3, a longer uncard costs less than a weak opening does. Spend the effort on scenes 1 to 3. The relationship-based length rules are a reasoned assumption (grade C). The wrapping study (Q6) supports a rougher, more intimate style for close ties and a more polished one for acquaintances.

##### Q5. Interaction
- Playable-ad practice: one core mechanic, the first tap obvious within about 2 s, no instruction screen, and a reward within seconds (AdMapix, 2026; Unity, undated; grade C).\[37\]\[38\]
- People spend only about 1.7 s reading start-screen instructions (GeoSpot, undated; vendor; grade C).\[39\]
- No source gave a validated "inputs per minute" figure for narrative experiences. The 8 to 15 s rhythm is an assumption, derived from 15 to 30 s playable loops containing 2 to 4 inputs and from Stories' tap-forward behaviour (56 to 66% tap forward on image frames, per Socialinsider, 2025).\[16\]

##### Q6. Feeling seen
- **Wrapping and reveal.** In three experiments, gifts from friends were liked more when sloppily wrapped. Neat wrapping raised expectations that the gift then failed to meet. For acquaintances, neat wrapping signalled that the giver valued the relationship (Rixom, Mas & Rixom, *Journal of Consumer Psychology*, 2019; grade A).\[40\]\[41\]\[42\] Howard (1992) found wrapped gifts generally cue a happier mood than unwrapped ones (grade A, older).\[43\]\[44\]
- **Gratitude.** Kumar & Epley (*Psychological Science*, June 2018; grade A) found that gratitude-letter writers predicted recipient mood of 3.11, against an actual 4.12 (−5 to +5 scale). They predicted awkwardness of 2.95, against an actual 1.95 (0–10 scale).\[45\]
- **Voice.** Voice-based contact created significantly stronger bonds than text, without more awkwardness, and video added nothing measurable beyond voice (Kumar & Epley, *JEP: General*, 2021; grade A).\[46\]
- **Photos and memories.** Personal photos and nostalgic memories reliably raise positive affect and social connectedness (Oba et al. and others, reviewed in *Social Cognitive and Affective Neuroscience*, 2022; grade A).\[47\] One 2023 trial found personally relevant and generic positive-memory images equally effective at raising positive affect (*Current Psychology*, 2023; grade A).\[48\] The power comes from the specific memory the image cues, not the image alone, so pair every photo with the giver's line about why it matters.\[49\]
- **Inside jokes and names.** I found no direct peer-reviewed comparison. Rank them below specific memories and voice (grade C).
- **Ranking for the generator:** specific memory with the giver's caption > friends' voices > personal photos > name > inside jokes > generic effects.

##### Q7. Replies
- I found no public reply-rate benchmark for e-cards, group cards (Kudoboard, GroupGreeting, Evite, Paperless Post) or birthday messages.
- Kudoboard emails the recipient within an hour of delivery with a "thank your contributors" option, and reports thank-yous in paid analytics, but publishes no aggregate rate (Kudoboard Help Center, undated; grade B).\[14\]\[50\] Kudoboard's claim that "92% of people feel happier" is marketing (grade C).\[51\]\[52\]
- In an AYTM survey, 72% usually send a thank-you note after receiving a gift, but only 12% mostly send them electronically (grade C, year unclear).\[19\]
- Emoji make text replies feel more responsive: 4.43 versus 3.57 (*PLOS ONE*, 2025; grade A).\[53\] Replies mirror emoji use, especially between close contacts (*Journal of Nonverbal Behavior*, 2023; grade A).\[54\] This supports a one-tap emoji reaction as the lowest-effort reply.
- Given Kumar & Epley's voice findings, a 10-second voice-note reply is likely the most meaningful option for the giver. Offer it, but don't make it the default.

##### Q8. Replays and keepsakes
- **Spotify Wrapped 2025** reached 200 million engaged users in about 24 hours, up 19% on 2024 (when 200 million took 62 hours). It recorded more than 500 million shares on day one, up 41% (Spotify via TechCrunch and PRWeek, December 2025; grade B).\[55\]\[56\] By the end of Q4 it had more than 300 million engaged users and 630 million shares (Spotify Q4 2025 results; grade B).\[57\]
- Spotify's communications co-head CJ Stanley framed Wrapped as a gift and said no one wants to unwrap the same thing every year. The 2024 edition drew criticism for thin stats and an AI podcast (TechCrunch, December 2025).\[55\]\[56\]
- Spotify found younger users often screenshot Wrapped to share privately. In 2022 it added direct sharing to WhatsApp and Instagram DMs (TechCrunch, 2022; grade B).\[58\] For uncard, this argues for easy private save and share of the keepsake.
- **Google Photos Memories** is used by more than 500 million people a month (Google, 2024; grade B).\[13\]\[59\] Google noted that users want to go back to the more meaningful moments, not just a daily stream (Fast Company, 2023; grade B).\[18\]
- **Implication:** replays come from a surprise resurfacing at a meaningful date and an easy, private keepsake. Because uncard must not collect the recipient's contact details, the resurfacing should go through the giver ("send Maya her birthday uncard again on her anniversary").

##### Q9. Access and comfort (WCAG 2.2)
- **2.2.2 Pause, Stop, Hide (A):** any auto-starting motion lasting more than 5 s alongside other content needs a pause control.\[60\]
- **2.3.1 Three Flashes or Below Threshold (A); 2.3.2 Three Flashes (AAA):** design to the AAA rule (no more than 3 flashes in any second) because cards are celebratory and confetti-heavy.\[61\]
- **2.3.3 Animation from Interactions (AAA):** satisfied by `prefers-reduced-motion` (W3C technique C39).\[62\]
- **1.4.2 Audio Control (A):** auto-playing audio over 3 s needs a stop or volume control.
- All from W3C, current as of 2026; grade A.
- A 2026 audit found 96.8% of 186 AI-generated web interfaces shipped animation with no reduced-motion guard (MotionSpec, September 2026; grade C).\[63\] A generator like uncard's is at real risk of this by default, so make the guard part of the template, not the theme.

##### Q10. Measurement
- See the event table. The legal position is unsettled.
- Quebec's government guidance says identifying, locating or profiling functions must be off by default (Quebec.ca, provisions in force September 2023; grade A as official).\[64\]\[65\]
- The CAI's consent guidelines (October 31, 2023) are non-binding.\[66\]\[67\]
- The OPC's 2011 guidance treats tracking data as personal information.\[22\]
- Consent-platform vendors claim all analytics need opt-in.\[68\] They have a commercial interest, and that reading goes beyond the text.
- Aggregate, cookieless, per-uncard counting is the defensible design. Have it confirmed by counsel.

---

#### Caveats

- Many speed and Stories figures come from retail sites and brand accounts, not personal gifts. Personal content from a friend probably holds attention better, so treat these benchmarks as floors.
- Several key numbers (Akamai 2017, Verizon/Publicis 2019, Howard 1992) predate the preferred 2023 to 2026 window. They remain the most-cited primary sources, but should be re-validated with uncard's own data.
- Playable-ad and OG-image figures come from vendors (grade C) and are directional only.
- The reply, replay and "make one back" targets are assumptions. Replace them after the first holiday cohort (mid-November 2026 onward), which will be the first large sample.

#### Sources

1. [Core Web Vitals Benchmarks 2026: What Good Looks Like](https://www.digitalapplied.com/blog/core-web-vitals-benchmarks-2026-pass-rate-reference)
2. [iMessage Preview Image Missing: How to Fix It - OpenGraph+](https://opengraphplus.com/consumers/apple/issues/image-not-displaying)
3. [iMessage Link Preview Not Working? How to Fix OG Tags on iOS](https://ogfixer.com/blog/imessage-link-preview-not-working)
4. [prefers-reduced-motion CSS media feature - MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@media/prefers-reduced-motion)
5. [How to Create Engaging and Accessible WCAG-Compliant Animations - The A11Y Collective](https://www.a11y-collective.com/blog/wcag-animation/)
6. [How Renault improved its bounce and conversion rates by measuring and optimizing Largest Contentful Paint](https://web.dev/case-studies/renault)
7. [2025 Instagram Stories Benchmarks](https://www.socialinsider.io/social-media-benchmarks/instagram-stories-benchmarks)
8. [Playable Ads: The Complete Guide for Mobile Games](https://www.sett.ai/content/playable-ads-complete-guide/)
9. [It's Surprisingly Nice to Hear You: Misunderstanding the Impact of Communication Media Can Lead to Suboptimal Choices of How to Connect With Others](https://www.researchgate.net/publication/344232654_It's_surprisingly_nice_to_hear_you_Misunderstanding_the_impact_of_communication_media_can_lead_to_suboptimal_choices_of_how_to_connect_with_others)
10. [Instagram Stories Video Length (2026)](https://www.moonb.io/blog/instagram-stories-video-length)
11. [Instagram Stories Engagement Benchmarks (2026)](https://www.dashsocial.com/blog/every-instagram-stories-performance-benchmark-you-need-to-know)
12. [Animated Content and Timing](https://usability.yale.edu/digital-accessibility/accessibility-resources/accessibility-articles/animated-content-and-timing)
13. [A new, scrapbook-like Memories view in Google Photos](https://blog.google/products-and-platforms/products/photos/google-photos-memories-view/)
14. [Analytics (Site Metrics)](https://support.kudoboard.com/hc/en-us/articles/20855933145491-Analytics-Site-Metrics)
15. [SMS Marketing Benchmarks 2026: CTR, Open Rates by Industry](https://messageflow.com/blog/sms-marketing-benchmarks/)
16. [Instagram Stories Statistics 2026: Completion Rates, Views ...](https://www.upgrow.com/blog/instagram-stories-2026-completion-rates-views-engagement-benchmarks)
17. [Captions increase viewership, accessibility and reach](https://www.newtontech.net/en/blog/23083-captions-increase-viewership-accessibility-and-reach/)
18. [Google Photos will let you alter your Memories](https://www.fastcompany.com/90938324/google-photos-just-got-much-better-heres-how-exclusive)
19. [Thank You Notes: Paper Notes Considered More Meaningful](https://aytm.com/post/thank-you-notes-survey)
20. [Québec Law 25: Privacy Requirements for Websites](https://www.cookiebot.com/en/law-25/)
21. [Quebec Law 25 Cookie Consent 2026: Section 8.1 & the CAI](https://cookiebeam.com/guides/quebec-law-25-cookie-consent-2026)
22. [Canadian Privacy Commissioner Issues Guidelines for Online Behavioral Advertising](https://www.loeb.com/en/insights/publications/2011/12/canadian-privacy-commissioner-issues-guidelines-__)
23. [iMessage Link Preview Image Size Guide (2026) - OpenGraph+](https://opengraphplus.com/consumers/apple/images)
24. [Enabling Rich Previews Of Shared Links](https://mc.dev/enabling-rich-previews-of-shared-links/)
25. [CelerSMS: SMS with Link Preview](https://www.celersms.com/sms-link-preview.htm)
26. [Core Web Vitals Explained for Marketers: LCP, INP, and CLS in Plain English](https://yassersoliman.com/blog/core-web-vitals-explained-marketers/)
27. [How The Economic Times passed Core Web Vitals thresholds and achieved an overall 43% better bounce rate](https://web.dev/case-studies/economic-times-cwv)
28. [NDTV achieved a 55% improvement in LCP by optimizing for Core Web Vitals](https://web.dev/ndtv/)
29. [Mobile Videos Often Watched Without Audio, Study Finds](https://www.nexttv.com/news/mobile-videos-often-watched-without-audio-study-finds)
30. [Subtitle Stats: How Many People Use Subtitles in 2024?](https://www.kapwing.com/resources/subtitle-statistics/)
31. [Watching subtitled videos with the sound off affects viewers' comprehension, cognitive load, immersion, enjoyment, and gaze patterns: A mixed-methods eye-tracking study](https://journals.plos.org/plosone/article?id=10.1371%2Fjournal.pone.0306251)
32. [Watching subtitled videos with the sound off affects viewers' comprehension, cognitive load, immersion, enjoyment, and gaze patterns: A mixed-methods eye-tracking study](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11458047/)
33. [New \<video\> Policies for iOS](https://webkit.org/blog/6784/new-video-policies-for-ios/)
34. [fix(sound): Audio unlocks on iPhone Safari: a phone starts muted and the speaker's tap turns sound on; resume inside the gestures WebKit counts, the silent-switch media unlock, interrupted contexts resumed by AriSweedler-at · Pull Request #128 · AriSweedler-at/hyperagent-web-apps](https://github.com/AriSweedler-at/hyperagent-web-apps/pull/128)
35. [Streaming read-aloud is silent on iPhone when the ring/silent switch is off · Issue #44 · wltiger/my-cloudcli](https://github.com/wltiger/my-cloudcli/issues/44)
36. [Playable Ads Guide 2026: Formats, Specs, Examples and Best Practices](https://segwise.ai/blog/understanding-playable-ads-guide)
37. [Mobile Ad Metrics for Creatives| Unity](https://unity.com/blog/3-in-ad-data-metrics-to-optimize-in-your-mobile-game-ad-creative-and-how)
38. [Playable Ad Examples 2026: Teardowns, Mechanics & End Cards](https://www.admapix.com/blog/ad-intelligence/playable-ad-examples)
39. [Playable Ads Examples That Doubled User Engagement - GeoSpot Media](https://blog.geospot.media/playable-ads-guide/)
40. [(PDF) Presentation Matters: The Effect of Wrapping Neatness on Gift Attitudes](https://www.academia.edu/80850350/Presentation_Matters_The_Effect_of_Wrapping_Neatness_on_Gift_Attitudes)
41. [The science of gift wrapping explains why sloppy is better](https://theconversation.com/the-science-of-gift-wrapping-explains-why-sloppy-is-better-128506)
42. [There Is a Science to Gift Wrapping - The National Interest](https://nationalinterest.org/blog/buzz/there-science-gift-wrapping-106086)
43. [Research: Lovely Wrapping Makes Us Happier About The Gift](https://www.smu.edu/news/archives/2015/holidays-gift-wrapping-24nov2015)
44. [Is it Really the Thought That Counts? The Psychology of Gift Wrapping - Duck, Duck, Platypus!](https://duckduckplatypus.com/is-it-really-the-thought-that-counts-the-psychology-of-gift-wrapping/)
45. <https://uploads-ssl.webflow.com/5c484e0f4aa6f839dc553c45/5c9a38dff7d06d3980dad2df_KumarEpley2018.pdf>
46. [Researchers asked people to reconnect with an old friend either by phone or by email, and the people who predicted the phone call would feel awkward were wrong — it left them significantly more connected than email did, with no extra awkwardness at all - The Blog Herald](https://blogherald.com/blog-tips/n-researchers-asked-people-to-reconnect-with-an-old-friend-either-by-phone-or-by-email-and-the-people-who-predicted-the-phone-call-would-feel-awkward-were-wrong/)
47. [Patterns of brain activity associated with nostalgia: a social-cognitive neuroscience perspective](https://academic.oup.com/scan/article/17/12/1131/6585517)
48. [s12144 023 04582 5](https://link.springer.com/article/10.1007/s12144-023-04582-5)
49. [Looking at Your Photos Can Be Uplifting, Enlightening, or Bittersweet](https://www.psychologytoday.com/us/blog/longing-for-nostalgia/202401/looking-at-your-photos-can-be-uplifting-enlightening-or)
50. [How do I thank my contributors? (recipient)](https://support.kudoboard.com/hc/en-us/articles/360059701493-How-do-I-thank-my-contributors-recipient)
51. [Modern Employee Recognition and Online Group eCards](https://www.kudoboard.com/)
52. [Get Well Soon Cards from a Group](https://www.kudoboard.com/cards/get-well-soon-cards/)
53. [The impact of emojis on perceived responsiveness and relationship satisfaction in text messaging](https://journals.plos.org/plosone/article?id=10.1371%2Fjournal.pone.0326189)
54. [Smile Back at Me, But Only Once: Social Norms of Appropriate Nonverbal Intensity and Reciprocity Apply to Emoji Use](https://link.springer.com/article/10.1007/s10919-023-00424-x)
55. ['No one wants to unwrap the same thing every year': How Spotify Wrapped shook things up this year](https://www.prweek.com/article/1942739/no-one-wants-unwrap-thing-every-year-spotify-wrapped-shook-things-year)
56. [Spotify Wrapped 2025 logo](https://techcrunch.com/?p=3072762)
57. [Spotify hits a record 751M monthly users thanks to Wrapped, new free features](https://finance.yahoo.com/news/spotify-hits-record-751m-monthly-140014439.html)
58. [techcrunch.com](https://techcrunch.com/?p=2449677)
59. [Image Credits:Google](https://techcrunch.com/?p=2583152)
60. [Understanding Success Criterion 2.2.2: Pause, Stop, Hide](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
61. [WCAG 2.3.2 Three Flashes — The Zero-Threshold Rule](https://accessibility.build/wcag/2-3-2)
62. [C39: Using the CSS prefers-reduced-motion query to prevent motion](https://www.w3.org/WAI/WCAG21/Techniques/css/C39)
63. [prefers-reduced-motion, explained (and how to test it) — MotionSpec](https://motionspec.dev/blog/prefers-reduced-motion)
64. [La Commission d'accès à l'information du Québec présente un guide de rédaction d'une politique de confidentialité à publier sur un site Web](https://mcmillan.ca/fr/perspectives/publications/la-commission-dacces-a-linformation-du-quebec-presente-un-guide-de-redaction-de-la-politique-de-confidentialite-a-publier-sur-un-site-web/)
65. [Identification, localisation et profilage](https://www.quebec.ca/gouvernement/travailler-gouvernement/normes-gouvernance-pratiques-internes/protection-des-renseignements-personnels/technologie-et-droit-a-la-protection-des-renseignements-personnels/identification-localisation-profilage)
66. [Critères de validité…](https://www.cai.gouv.qc.ca/actualites/criteres-validite-consentement-commission-adopte-lignes-directrices)
67. [Commission d'accès à l'information](https://edilexpert.edilex.com/2024/01/19/les-nouvelles-lignes-directrices-sur-les-criteres-de-validite-du-consentement-de-la-commission-dacces-a-linformation/)
68. [Is Cookie Consent Required in Canada? PIPEDA, CASL & Law 25 (2026)](https://www.cookie-banner.ca/blog/cookie-consent-canada-guide-2026)

## Open questions

- **Scene count contradiction:** this research's default is 5–9 scenes; `decisions/0005` resolved the product's scene count as "usually 8 to 10, default 9." Both are 2026 sources — someone needs to decide whether the generator rules follow the research or the standing decision.
- **Hosting-length contradiction:** this research assumes the link stays live "at least 12 months"; the decided pricing model (`decisions/0002`, `0005`) gives 3 months of included hosting, then a free keepsake or $3/year to keep the link live. These can't both be the plan as written.
- **Analytics granularity:** the proposed event list (scene-level dwell time, replay buckets, `a11y_mode`) is more detailed than "no analytics" / "recipients are never tracked" (D12, `decisions/0006`). The same tension shows up in `research/sharing-referral-loop.md`'s event schema — worth resolving once, not per-document.
- **Legal review not yet tracked.** The Quebec Law 25 / PIPEDA read here is explicitly unverified by the research itself and has no corresponding decision record or owner yet.
