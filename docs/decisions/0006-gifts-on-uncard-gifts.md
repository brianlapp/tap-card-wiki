# 0006 — Gift links live on uncard.gifts, served by a Cloudflare Worker

**Status:** Open (proposed by Brian, 2026-10-02)
**Date:** 2026-10-02
**Deciders:** Jordan, Brian Lapp, Tim Miller (equal partners)
**Method:** Read from the product repo at `ffd1adc` (gift route, gift server functions, Give panel, player, spec W-37/W-47/W-48) and Cloudflare's Workers permissions docs. Not built or tested. Anything marked (unverified) needs checking before it is relied on.

## TL;DR

Serve every gift from **uncard.gifts/{id}** through the `uncard-gifts` Worker (already created, 2026-10-02), not through the Lovable app. Lovable never sees a recipient, which settles W-37 and D16 together, and the gift link finally matches what the product copy already promises. Built in four thin slices; each one can be undone by removing a route or reverting one line.

## Context

- Gifts are served today at **uncard.app/c/{id}**. The Give panel copies `${window.location.origin}/c/{id}` (`src/uncard/site/make/GivePanel.tsx`).
- The product copy already says gifts live on **uncard.gifts** (`src/uncard/data/facts.ts`: `GIFTS_URL = 'https://uncard.gifts'`, sample links `uncard.gifts/r7Qm2xVb`).
- The player was built framework-free on purpose because "it also runs on uncard.gifts and in the offline keepsake" (`src/uncard/README.md`).
- **W-37:** Lovable's hosting analytics record every page's path, device and country (spec N6). Recipients are never to be tracked (D12), so gift pages must stay out of them before any real gift is sent.
- **D16** (open, no default): serve gifts from uncard.app, or from uncard.gifts. The spec's W-48 assumed uncard.gifts would mean a second Lovable project.
- The gift page's rules, which any new host must keep: the same neutral 404 for unknown, closed, withdrawn and expired links; headers `X-Robots-Tag: noindex, nofollow`, `Referrer-Policy: no-referrer`, `Cache-Control: no-store`; no request from the browser on a visit, only when a PIN is entered; nothing stored in the browser; no third-party requests.
- Cloudflare (2026-10-02): the `uncard-gifts` Worker exists in Jordan's account (404 placeholder, workers.dev and preview URLs off, no route). Brian has Editor on that Worker plus DNS and Workers Routes rights on the uncard.gifts zone. A **route** works with that per-Worker access; a Custom Domain doesn't yet.

## Options

1. **Stay on uncard.app/c/{id}.** No work. But Lovable's analytics see every gift visit (W-37 unsolved), and the link doesn't match the product copy.
2. **Worker proxies uncard.gifts/* to uncard.app/c/*.** Small. But every visit still passes through Lovable, so its analytics most likely still see recipients (unverified). Nicer link, same privacy problem.
3. **Worker serves gifts itself (recommended).** The Worker serves the framework-free player and the gift page as static files, and asks the app for the card server-to-server through two secret-protected endpoints that carry no gift id in the address. Lovable never sees a recipient's device, country or visit. Matches the design the code already anticipates.
4. **Second Lovable project (spec W-48).** Analytics can be switched off there, but it's a second project to keep in sync, still on Lovable hosting, and only the owner login can create it.

## Decision (proposed)

Option 3. It replaces W-48's second Lovable project.

## How it gets built: four slices

| # | Slice | Who | Undo |
|---|---|---|---|
| 1 ✅ | **Plumbing.** *Done 2026-10-02: uncard.gifts/* answers 404 "This uncard isn't here." from the Worker, verified with curl. The placeholder doesn't send the three gift headers yet; slice 3 adds them.* Proxied DNS record on uncard.gifts plus route `uncard.gifts/*` → `uncard-gifts`. The placeholder answers every address with the neutral 404 and the three gift headers. Proves the domain end to end with nothing real behind it | Brian's agent (has the rights) | Delete the route and record |
| 2 | **App endpoints.** Two server routes on uncard.app: `POST /api/gifts/open {id}` → live / pin / missing, and `POST /api/gifts/pin {id, pin}` → the existing PIN answer. Both reuse `loadGift` and `tryPin` unchanged and refuse any request without the shared secret header. No id in the path, so even the app's own logs never list gift ids | PR to the product repo, reviewed by the build agent | Endpoints do nothing without the secret |
| 3 | **The gift Worker.** Code in the product repo at `workers/gifts/`, importing `src/uncard/player` and the gift words and headers, so there's one source of truth. Serves the player, styles and fonts as static files; renders the three states; forwards PIN tries. No cookies, no storage, no analytics, no third-party requests | Brian's agent, deployed with wrangler | Point the route back at the placeholder |
| 4 | **Switch the link.** The Give panel copies `uncard.gifts/{id}`. uncard.app/c/{id} redirects there, so links already sent keep working | PR to the product repo | Revert one line |

**Checks before slice 4 goes live:** run the existing `tools/qa/gift-flow.mjs` against uncard.gifts (the eight odd addresses, identical 404s, PIN lockout after five tries, no request to any other host, nothing in browser storage), plus the phone checks from the Phase 5 report.

## Consequences

- Recipients' visits never reach Lovable, so D12 ("recipients never tracked") holds by construction, not by a setting.
- The app stays the only place that touches the database; the Worker holds one shared secret and no database keys.
- The player has to stay framework-free, which it already is. The offline keepsake can reuse the same bundle later.
- A second deploy target exists (the Worker). It deploys from the same repo, so there's still one codebase.

## Open questions

- Can Brian deploy with wrangler under a per-Worker Editor role, including uploading static files? (unverified; wrangler needs Node 22+, and Brian's Mac has Node 20) Fallback: Jordan's Codex deploys, or an account API token scoped to `uncard-gifts`.
- Does Lovable's analytics log server-to-server POSTs to `/api/...`? (unverified) Without an id in the path and with Cloudflare's IP as the source, nothing about a recipient would be in them either way.
- The shared secret has to be set in two places: Lovable's secrets (write-only) and the Worker's. Generate it once and save it in 1Password.
- Should `www.uncard.gifts` redirect to the bare domain? (assumption: yes)
