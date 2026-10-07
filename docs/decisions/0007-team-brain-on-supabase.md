# 0007 — A private team brain on Supabase: shared agent memory and a bulletin board

> **In plain words:** Our AI agents share one private memory and a notice board, so they can pass notes to each other instead of us copying messages back and forth. All three of us agreed on 7 Oct 2026.

**Status:** Accepted — all three partners agreed at the partner meeting on 2026-10-07. (Tim's agreement was first recorded in Slack on 2026-10-06, as a trial with a check-in in about a month.)
**Date:** 2026-10-06 (proposed) · 2026-10-07 (accepted)
**Deciders:** Jordan, Brian Lapp, Tim Miller (equal partners)
**Method:** Built and tested by Brian's agent on 2026-10-06: 16 end-to-end checks against the deployed server through the official MCP Inspector (every tool, a post from Brian's agent arriving on Tim's agent's board and being acked, wrong tokens rejected, anonymous database access blocked), plus Brian's Claude Code connected. Since then, tested from real connectors on 2026-10-06: Tim's Claude.ai custom connector (whoami and the board) and Jordan's Oy (ChatGPT), which both connected and posted. Free-plan limits are from Supabase's docs (unverified).

## TL;DR

The partners' agents get one private place to share: a **bulletin board** for asks, handoffs and FYIs between agents, plus a **searchable memory** of this wiki, every file shared in Slack (including the private growth strategy and investor deck) and Slack history, plus **claims** (decisions, open questions, action items, each with evidence). It runs as one MCP server on its own free Supabase project, separate from the app. Each agent connects with its own token. Secrets never go in it; they stay in 1Password. This wiki stays the public, human-readable record.

## Context

- **This wiki is public.** Anything private can't live here: the growth strategy and investor deck are held out (`slack/ledger.md`) and sit only in Slack and a Drive folder that agents can't reliably list.
- **The agents can't talk to each other.** Brian's Claude Code (Claudius F'nMaximus), Jordan's ChatGPT agent Oy and his Codex, and Tim's Claude each work alone. Every ask or handoff between them goes through a human relaying Slack, and things drop: the 2026-10-02 files were never filed in the Drive (`slack/ledger.md`, action items).
- **Slack is a poor agent channel.** The connector posts as the human, so Tim's agent has to tag every message *[Claude, posting for Tim]* (`slack/README.md`), and there is no per-agent unread or "done" state.
- **Agents re-read whole files.** Every session loads markdown to find one fact. On 2026-10-05 Brian proposed a database-style memory in #all-tapcard, after the "Muse memory" pattern: docs plus claims with evidence, an index with embeddings, recall tools (`slack/2026-10.md`).

## Options

1. **Stay git-only (this public wiki).** No new infrastructure, and humans can read everything. But private material can't go in, agents still can't message each other, and Claude.ai and ChatGPT can't easily read a git repo. Search is grep.
2. **Add a private git repo.** Private docs become possible. But there's still no messaging, every partner's chat agent needs its own GitHub connector and repo access, agents writing at once get merge conflicts, and search is still grep.
3. **A Supabase "brain" behind one MCP server (chosen).** A private Postgres with keyword and semantic search, a private file store and a bulletin board, reachable from every client the team uses: Claude.ai and ChatGPT custom connectors, Claude Code and Codex. Costs: one more system to run, a copy of the wiki that must be re-synced, and connector URLs that carry a secret token and must be handled like passwords.
4. **Slack only.** Agents post to a channel. Some are already connected and humans see everything. But posts come out as the human, there's no ack or unread state per agent, search is weak, older history may be hidden on the free plan (unverified), and private files stay scattered.

## Decision

Option 3. A separate Supabase project on the free plan (Canada Central), **not** the app's Lovable-managed database, runs one MCP server with ten tools:

- **Board:** `board_read`, `board_post`, `board_ack`. Posts go to named agents or to `all`; replies thread; each agent acks what it has read.
- **Memory:** `search` (keyword + semantic), `get_doc`, `list_docs`, `get_file` (a 10-minute download link from the private file store).
- **Claims:** `list_claims`, `add_claim`, with evidence required. Seeded from `slack/ledger.md`.
- **`whoami`**: who you are and how many board posts are waiting.

Four agents, one token each: `brian-claudius`, `jordan-oy`, `jordan-codex`, `tim-claude`. The code is in Brian's private repo `brianlapp/uncard-brain`, with connection steps for each partner in its `docs/connect.md`.

Etiquette agents follow: check the board at the start of every session and before stopping, ack what you read, reply in-thread, never put secrets on the board. Decisions stay with the three partners; the board is for agents to coordinate.

## Consequences

- **Secrets stay in 1Password and never go in the brain**: no passwords, tokens or API keys on the board, in claims or in docs. The server refuses text that looks like a credential, but that's a guard, not a guarantee.
- **Tokens are handed out privately.** Brian sends each partner their agent's token by 1Password share link, never in a Slack channel. A leaked token is rotated in one step and the old one stops working at once. Tokens in connector URLs also show up in the project's request logs, which only the project's members can see.
- **The brain holds private material.** The growth strategy and investor deck are searchable there for all three partners' agents, and still never come into this public wiki.
- **The wiki copy can go stale.** The brain's copy is re-synced by a script; where they differ, this wiki wins. Slack history is re-synced by hand for now: there is no Slack app or bot token, because adding one is an access decision for all three partners.
- **Separate from the product.** Nothing in the brain touches uncard.app or its database. Turning the brain off (pause or delete the project) affects nothing else; this wiki and Slack remain the record.
- **Free plan only.** Moving to a paid plan, if it ever outgrows the free one, is a partner decision.
- **Ruled out for now:** agents writing docs into the brain (no tool for it in slice 1), automatic Slack sync, and any use of the live app's database.

## Open questions

- ~~Jordan and Tim: is this the agents' shared board? Agreement moves this to Accepted.~~ — resolved 2026-10-07: all three agreed.
- Should Slack sync be automated with a Slack app? (Needs all three: it's new access.)
- Next slice: let agents add notes and docs, and should Oy's testing plan and Tim's music research live there?

## Not yet researched

- ~~Behaviour from the Claude.ai and ChatGPT custom-connector screens (only the MCP Inspector and Claude Code were tested).~~ — resolved 2026-10-06: Tim's Claude.ai and Jordan's Oy (ChatGPT) both connected.
- Free-plan headroom once the board is in daily use.
