# Product Experience

**Status:** Draft
**Updated:** 2026-09-30
**Owner:** Brian Lapp
**Method:** Extracted from the UNCARD brand demo artifact (v0.1, Sep 29, 2026) — its page copy, the two playable sample uncards and its data. The demo is a **design artifact, not the product**: none of this is confirmed as built (unverified). Where the demo cites the spec (`Tapcard_Product_and_Build_Spec_v2`), the spec itself was not available.

## TL;DR

What the giver does, what the recipient gets, and what happens after. The demo shows it end to end in both brand directions with identical behaviour; only the voice differs.

## The nine-beat arc

An uncard is **8–10 scenes, default 9**, following one arc (demo, citing spec §4.2):

| # | Beat | Job |
|---|---|---|
| 1 | Arrive | Land inside their world |
| 2 | Recognise | Show you know them |
| 3 | Remember | Bring a real story to life |
| 4 | Play | Let them do something |
| 5 | Breathe | Change the pace |
| 6 | Cameo | Hear from someone else |
| 7 | Pay off | Return to an earlier joke |
| 8 | Mean it | Say what matters |
| 9 | Finish | End on a high |

Each scene is filled by a section from `../catalogue/`. Worked examples: `../catalogue/samples.md`.

**Conflict:** the catalogues build 8-section decks with informal beats. See Open questions.

## For the giver: five steps

1. **Tell us about them.** Free text, "the way you would to a friend". One or two follow-up questions at most. Anything marked *avoid* stays private and never becomes a joke.
2. **We pitch one idea.** One direction in plain words — not a wall of templates. Options: *Make it*, *Try another direction*, or nudge it: *more playful*, *less roast*, *more heartfelt*.
3. **Preview the real thing.** Every scene works in the preview exactly as the recipient will see it. Change requests in plain words. **Lock** scenes you love so later edits never touch them.
4. **Give them the link.** One link, any phone or computer.
5. **They play. Everyone keeps it.**

What the giver explicitly does **not** do: scroll 100 templates, fill in a 30-question form, design anything, write it all themselves, or make the recipient download an app.

## Studio

The creator is conversational with a live preview beside it. Shown in the demo:

- The pitch arrives as a named concept ("Mission: Level Nine") with a one-paragraph summary of every scene
- Chat-style change requests ("Make Bean's lines a bit cheekier")
- Per-scene lock; a change rewrites only the scenes it touches
- Autosave; *Preview as {name}*; *Give this uncard*

## Give & share

| Control | Options |
|---|---|
| Who can open it | Anyone with the link (unlisted, not searchable) · **Link + PIN** (recommended for kids) |
| Which moments can be shared | Per-scene toggle. Private scenes (e.g. The Letter) are excluded |
| What a share opens | This moment only · the full uncard (**off automatically when a PIN is set**) |
| Keepsake download | On/off for the recipient's family |

Every scene produces a **share tile** with a caption, in 9:16, 4:5 and 1:1. *Share* hands the tile to the phone's share sheet; there is **no promise of posting to any social network**.

## For the recipient

- Opens on any phone. No app, no account.
- Sound is their choice; it starts on a tap.
- Tap through at their own pace. **Every game can be skipped** and the ending is still reached.

## Hosting and the keepsake

| When | What happens |
|---|---|
| Day one | Given. The link goes live. |
| Three months | Hosting included. No countdown is ever shown to the recipient. |
| 30 and 7 days before | Reminders to the giver, by email and in their account. |
| After | Download the keepsake free, or keep the same link live for **$3/year**. |

The **keepsake** is a single file that plays the whole uncard offline, games included.

## Promises made on the site

- No account needed to open one
- No ads or trackers inside an uncard
- Private notes stay private
- Kids never get accounts
- The giver chooses what's shared
- The keepsake works offline
- No fake social proof or invented replay counts in marketing

These are product commitments stated publicly in the demo. Each needs to be true of the build before anything ships with this copy.

## Pricing shown

$5.99 per uncard · $9.99/month for two · hosting as above. **This conflicts with the spec baseline** — see `../decisions/0002-pricing-model.md`.

## Open questions

1. 8 sections (catalogues) or 8–10 scenes on the nine-beat arc (demo)?
2. Pricing: demo $5.99 / two for $9.99 vs spec $4.99 / three credits for $9.99.
3. "No trackers inside an uncard" and "no PII in telemetry" (`scope.md`) need to be reconciled into one analytics rule.
4. The spec `Tapcard_Product_and_Build_Spec_v2` is referenced throughout but is not in this wiki.
