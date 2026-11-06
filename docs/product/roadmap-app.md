# The Roadmap App (build.uncard.app)

**Status:** Draft
**Updated:** 2026-11-06
**Owner:** Brian Lapp
**Method:** Read from the private repo [`JNabsRepo/uncard-team-roadmap`](https://github.com/JNabsRepo/uncard-team-roadmap) at `main` = **`cdccea4`** (2026-11-03). Files: `README.md`, `AGENTS.md`, `docs/ARCHITECTURE.md`, `docs/OVERSIGHT.md`, the runbook, `docs/SETUP-AFTER-MERGE.md`, the build reports (`final.md`, `followup.md`, `playbook-v3.md`), `docs/agents/*.md`, sections 1 to 4 of `docs/MCP.md`, and `Walkthroughs.tsx` (the connect steps). Role use was checked in the code with grep. Live checks, no sign-in tried: `GET /agents` and an unsigned `POST /mcp` on 2026-11-06. **Not checked:** signing in, the live screens, the live database, or connecting any assistant. Where the repo's docs disagree, the newest (Playbook v3, 2 Nov) wins.

## TL;DR

- The Roadmap is the three partners' private board for planning, reviewing and handing off work. It lives at **build.uncard.app**.
- It is its own app, with its own database and its own sign-in. It never reads uncard.app's database, its customers, the team brain or Slack (`docs/OVERSIGHT.md`, "Data boundaries").
- Work moves from Ideas to Delivered in seven stages. Priority is a vote by all three partners. Roles are labels, not permissions.
- People and assistants use it through three doors: the website, REST and MCP. All three run the same commands.
- No real Claude, Claude Code or ChatGPT connection has been recorded yet. The connect steps below are **untried**.
- On 2 Nov Jordan asked everyone to hold off adding things until he has organized it, and to keep agents human-directed ([`slack/2026-11.md`](../slack/2026-11.md)).

## How work moves through it

Stages are worked out from the records. Nobody sets them by hand (`src/roadmap/lifecycle.ts`).

```
Ideas → Plan & design → Review spec → Ready to build → Building → Check & release → Delivered
```

1. **Ideas.** Anything goes in. Each partner scores each idea from 1 to 10, and the queue is the average score. When two different partners **clear** an idea, it can get a spec.
2. **Plan & design.** One drafter at a time takes the idea, writes the plan and prepares the spec.
3. **Review spec.** Another partner (usually through their assistant) writes a review with suggestions marked *must*, *should* or *could*. The drafter answers every suggestion. Anyone can raise a concern. A concern never blocks.
4. **Ready to build.** The spec must be cleared, testable, measurable, reversible and fully reviewed. Then it is frozen as **Final v{n}**, and anyone can pick it up. No one person's approval is needed.
5. **Building.** **Take this build** hands a Ready item to your own assistant or to a builder key. Opening the sheet claims nothing. The builder saves checkpoints. If its session runs out of usage, any partner can press **Continue**.
6. **Check & release.** A different agent or person checks the build. Some work can't be undone, touches accounts or payments, or changes a public promise. That work needs one release approval from a partner who neither drafted nor built it. **The Roadmap never merges, deploys or publishes anything.** A person does that and records it.
7. **Delivered.** When the item's time window ends, someone records *continue*, *change* or *stop*. A lesson is then drafted.

The **Needs you** page lists what is waiting on you: scores, clears, reviews, stalled builds and window results. Ready is never permission to release (`docs/OVERSIGHT.md`).

## Who does what

**Partners.** Since Playbook v3 (2 Nov), every partner can do everything. Roles are labels for display and defaults. The code says so (`src/roadmap/auth/capabilities.ts`), and so does the Members screen ("A label, not a permission"). The setup docs label Jordan `product_owner`, Brian `technical_owner` and Tim `experience_owner`.

**Brian's `technical_owner` label** gives him no approve or revoke power the others lack. Any partner can revoke a key or an assistant, pause GitHub, or give the "technical" approval a policy needs. What the code still sends to the technical owner by default:
- requests for a platform-fit review, when nobody is named;
- a verifier's escalated question about a build;
- delivery requests, which go to "the integrator (Brian by default)".

One leftover still reads roles: lesson promotion. The builder flagged it as open (`playbook-v3.md`). Older docs (the 1 Nov runbook, `final.md`) say only Jordan sets priority and Brian must review releases. Playbook v3 replaced both rules.

**Assistants and keys.** An assistant is your Claude or ChatGPT, connected with your sign-in. It acts as you and is labelled "via <assistant>". A key is for a build agent and is made on the site.

| Caller | Can | Never |
|---|---|---|
| Assistant, **Read** | Read what you can read, follow items, see your inbox | Change anything |
| Assistant, **Read + Write** (default) | Add and shape ideas, comment, edit plans and specs, take the draft, claim and report on builds | Vote, clear, review or decide |
| Assistant, **+ Decide** | As you: vote, clear, review, mark ready, continue a build, give release approval | Web-only jobs (keys, policies, redaction, export, pausing GitHub, the purpose protocol) |
| Builder key (`urk_…`) | Claim Ready work, report, hand back a build | Vote, clear, review, decide, check its own work |
| Verifier key | Check a build it was assigned, pass it or send it back | Vote, clear, review, decide |
| Import key | Bring in draft ideas | Anything else |

Big team-wide rules (the "purpose protocol") need all three partners, signed in. No assistant can approve them.

## The three doors

| Door | Address | Who uses it |
|---|---|---|
| Website | `build.uncard.app` | Partners, signed in |
| REST | `/api/v1` | Scripts and agents with a token or key |
| MCP | `/mcp` | Claude, Claude Code, ChatGPT and build agents |

All three end in the same commands. The same caller and input give the same result and the same audit log entry, whichever door was used. The REST routes, the MCP tools and the `/agents` connect page are all generated from one tool list (`AGENTS.md`, `docs/MCP.md` section 1).

## How to connect your assistant

> **Untried.** These steps come from `Walkthroughs.tsx`, the `/agents` page. The repo says they follow the vendors' docs and that no real client has been connected (commit `cdccea4`). Menu names change. If yours differ, look for "custom connector" or "remote MCP server".

**Recommendation:** leave **Decide** off. Read and Write are enough to read, capture and comment. Decide lets your assistant vote, clear and approve as you. Jordan asked on 2 Nov that agents act only when a human directs them.

**Address:** copy it from `build.uncard.app/agents`. It should be `https://build.uncard.app/mcp`: the unsigned check below pointed its sign-in info at `build.uncard.app`.

On the approval page you sign in, name the connection, and pick **Read** (always on), **Write** (on by default) and **Decide** (off by default). Then ask: *"Who am I on the Uncard Roadmap?"* It should name you and list what it may do.

**Claude Code**
1. Run `claude mcp add --transport http uncard-roadmap https://build.uncard.app/mcp`
2. In Claude Code, open `/mcp`, choose **uncard-roadmap** and sign in. A browser tab opens the approval page.
3. Don't add an `Authorization` header. If you do, Claude Code skips the sign-in.

**Claude (web and desktop)**
1. Open **Customize → Connectors**, then **Add custom connector**.
2. Paste the address and name it "Uncard Roadmap". If asked, choose **Sign in now** and **Register automatically**. Leave the client ID and secret empty.
3. Click **Add**, then **Connect**, and approve.
4. Switch it on from the **+** in a chat, under **Connectors**.
5. On Team or Enterprise plans, an owner adds it once under Organization settings → Connectors. Each member then clicks **Connect**.

**ChatGPT**
1. Open `chatgpt.com/plugins`, click **+** and choose **Add custom MCP server**. Some accounts show this under **Settings → Apps & Connectors**.
2. Name it, add a description, choose a public endpoint and paste the address.
3. For authentication, choose **OAuth**. Leave the client ID and secret empty.
4. Accept the warning, create it, approve, then start a new chat with it switched on.
5. ChatGPT can't use a pasted key, so use OAuth only.

## Where it's hosted and how it's built

- **Lovable** project "Uncard Roadmap", in Jordan's NorthSTR workspace (runbook). The project link is in the private repo's `README.md`.
- **Stack:** TanStack Start (React 19, Vite) on Lovable Cloud, which is Supabase Postgres plus private storage. This is a separate database from uncard.app's (`docs/ARCHITECTURE.md`).
- **GitHub sync:** `main` syncs both ways with Lovable. Keep `main` building, and never force-push or rewrite pushed history (`AGENTS.md`).
- **Built by** Jordan's Sonnet 5.5 build agent, 1 to 3 Nov 2026 (git log).
- **Migrations:** `db/migrations/001` to `014`, plain SQL files. To apply one, a person pastes it into the Lovable chat and checks its size and fingerprint. Never apply SQL from code.
- **Outside calls:** only `api.github.com`, for an optional copy of items as GitHub Issues.
- **Docs:** `docs/spec/` (the source of truth), `docs/OVERSIGHT.md`, `docs/MCP.md` (generated), `docs/agents/`, `docs/integrations/`, `docs/build-reports/`.

| Folder | What lives there |
|---|---|
| `src/roadmap/commands/` | The one command layer. Every rule lives here |
| `src/roadmap/auth/` | Who is calling, and what each kind of caller may do |
| `src/roadmap/tools/` | The tool list that REST, MCP and `/agents` are built from |
| `src/roadmap/transport/`, `doors/` | REST and MCP servers, sign-in for assistants, keys |
| `src/routes/`, `src/components/roadmap/` | Pages and screens |
| `db/migrations/`, `tools/`, `tests/` | SQL, helper scripts, tests |

## Live status

| Check | Result | Date | Source |
|---|---|---|---|
| `GET https://build.uncard.app/agents` | 200, page title "Connect an assistant · Uncard Roadmap" | 2026-11-05 (Brian's check), 2026-11-06 (this page) | curl |
| Unsigned `POST /mcp` | 401, asks for a sign-in token (expected) | 2026-11-06 | curl |
| Partners given access | Jordan gave all three access | 2026-11-02 | [`slack/2026-11.md`](../slack/2026-11.md) |
| Migration 014 (Playbook v3) | "Not applied anywhere" | 2026-11-02 | `playbook-v3.md` |
| Real Claude, Claude Code or ChatGPT connection | Not done | 2026-11-03 | `playbook-v3.md` |

The `/agents` page builds itself in the browser, so its text was not checked. **Unknown:** which commit is published, which migrations are live, who has signed in, whether the GitHub copy and the scheduled jobs are on.

## Open questions

- Is migration 014 applied on the live site? Until it is, the Playbook v3 tools fail there (`playbook-v3.md`).
- Who connects first and records it? The compatibility table on the site starts empty.
- When does Jordan lift the 2 Nov "hold off" ask?
- Lesson promotion still checks roles. Who is the "second key" now that roles are labels?
- The 1 Nov runbook and `final.md` still describe Jordan-only priority and required reviewers. Should they be marked superseded in the repo?

## Sources

At `cdccea4` unless noted. The repo is private, and links go to `main`, which may have moved.

- [`README.md`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/README.md), [`AGENTS.md`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/AGENTS.md), [`docs/ARCHITECTURE.md`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/docs/ARCHITECTURE.md), [`docs/OVERSIGHT.md`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/docs/OVERSIGHT.md)
- [`docs/MCP.md`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/docs/MCP.md) (sections 1 to 4), [`docs/agents/assistant.md`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/docs/agents/assistant.md), [`build.md`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/docs/agents/build.md), [`verify.md`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/docs/agents/verify.md), [`import.md`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/docs/agents/import.md)
- [`docs/spec/JORDAN-RUNBOOK-what-happens-next.md`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/docs/spec/JORDAN-RUNBOOK-what-happens-next.md), [`docs/SETUP-AFTER-MERGE.md`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/docs/SETUP-AFTER-MERGE.md)
- [`docs/build-reports/final.md`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/docs/build-reports/final.md), [`followup.md`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/docs/build-reports/followup.md), [`playbook-v3.md`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/docs/build-reports/playbook-v3.md)
- [`src/components/roadmap/agents/Walkthroughs.tsx`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/src/components/roadmap/agents/Walkthroughs.tsx), [`src/roadmap/auth/capabilities.ts`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/src/roadmap/auth/capabilities.ts), [`src/roadmap/types.ts`](https://github.com/JNabsRepo/uncard-team-roadmap/blob/main/src/roadmap/types.ts)
- This wiki: [`slack/2026-11.md`](../slack/2026-11.md) (Jordan's 2 Nov ask)
