# 0008 — Run Brian's Uncard build work through the agent-team orchestrator

**Status:** Open — Brian's proposal, 2026-10-06. v0.1.0 is built. Becomes Accepted once Jordan and Tim agree.
**Date:** 2026-10-06
**Deciders:** Jordan, Brian Lapp, Tim Miller (equal partners)
**Method:** Built by Brian's agent as a private Claude Code plugin (`brianlapp/agent-team`, v0.1.0) on top of the superpowers plugin (6.4.2). Smoke-tested in a throwaway repo: plugin validation, a setup that never overwrites, and the status command. **Not yet run on any Uncard repo.** A search for an existing public template found none that covers this process (Brian's research notes, 2026-10-06).

## TL;DR

Brian's Claude Code becomes a **team lead**. Five sub-agents (researcher, test writer, implementer, reviewer, cleanup) each have a pinned model and work in their own git worktree. **None of them touch `main`.** Brian is product owner: he picks topics, answers batched decision rounds and reviews builds. Records live as files. Handoffs to Jordan's and Tim's agents go through the team brain's bulletin board (`0007`). Product changes still reach `uncard-starter` only as pull requests.

## Context

- This file's workspace rule says "there is no orchestrator agent: one agent, plugged straight into the repos". That worked for single tasks. It doesn't hold up for multi-step builds, where research, design, tests, code and review should come from different agents. The reviewer must never grade its own work.
- Jordan already runs a two-stage flow (Opus writes the spec, Sonnet builds in Lovable). Brian's agents worked ad hoc.
- The product repo already requires branch + pull request from everyone except Jordan's build agent and Lovable. A team that never touches `main` fits that rule as it stands.
- The team brain (`0007`) gives agents an inbox that every partner's agent can read.

## Options

1. **Keep one agent per task (today).** Simple. But nothing stops an agent reviewing its own work, there's no record of why a design changed, and nothing resumes cleanly across sessions.
2. **Adopt a public template.** The closest options cover 40–70% of the process and either run thousands of lines of hooks on every tool call or are weeks old with one maintainer.
3. **A small template of our own on superpowers (proposed).** About 28 markdown files with no runtime code: 5 agents, 4 skills (team lead, decision round, brief, resume) and 5 commands (setup, start, continue, decide, status). It's versioned, with install and upgrade docs.

## Decision (proposed)

Option 3, for **Brian's** Claude Code work on Uncard:
- **Records** (numbered design revisions, research per topic, plan and file-kanban board, resume board, Brian's to-do) live in a `team/` folder in this wiki. Anything private goes to the team brain instead, never here.
- **Code** reaches `uncard-starter` only as a pull request from a worktree branch. Jordan's build agent stays the only one merging to `main`.
- **Handoffs** to Oy, Codex or Tim's Claude are posted on the brain's bulletin board.

## Consequences

- More pull requests for Jordan's flow to review. The team's reviewer works against the design revision, so the PRs should arrive pre-checked.
- It only runs in Claude Code. Tim (Claude.ai) and Jordan (ChatGPT/Codex) take part through the board and PR reviews, not the plugin.
- It runs on Brian's Claude subscription; no API spend is added (D22 unaffected).
- If accepted, this file's "no orchestrator" line changes to point here.

## Open questions

- Should Jordan's Opus → Sonnet flow and this team split work by area (e.g. Jordan: app features; Brian: infra, gifts host, music), or share one board?
- Does `team/` belong in this public wiki, or should plans live only in the brain?
