# Team rules for our agents (SOPs)

**Status:** Agreed at the partner meeting on 7 Oct 2026 (Jordan's idea). Brian's agent wrote it up from Brian's notes. Jordan and Tim: read it, and say if anything is off.
**Applies to:** every partner's AI helper: Brian's Claude, Jordan's Oy and Codex, Tim's Claude, and any new one.

**Why we have these:** there are three of us, each with AI helpers, all moving fast. Two things keep the project on track. Everyone stays in their own lane. And all three of us understand what we're agreeing to and what we're being asked. If you're ever unsure, stop and ask your partner.

## 1. Stay in your lane

- **Production is Brian's job.** Once Uncard has its own production setup (the live site real customers use and pay on), only Brian ships changes to it. His agent only does it with his OK. Jordan's and Tim's agents hand him finished work to ship; they never ship it themselves.
- **Until then:** the live site is built in Lovable. Only Jordan's build agent and Lovable change the product's main code. Everyone else works on a separate copy (a branch) and asks for a review.
- **Don't do another partner's job.** If you need something from their lane, ask them in Slack, or ask their agent on the team brain's notice board.
- **Only one agent works on a given thing at a time.** Before starting, check the notice board so two agents don't change the same thing at once.

## 2. Database safety

- **Look, don't touch.** Agents only read a database, unless their partner says yes to that exact change.
- **Never delete, wipe, reset or bulk-change data** unless your partner has seen exactly what will change and said yes.
- **No typing changes straight into a live database.** Changes go in as written steps that someone else has read first.
- **Back up first, and know how to undo it,** before any risky change.
- **Treat everything as real.** We don't have a separate test copy of the app yet, so assume every database is the live one.
- **Passwords and keys live in 1Password only.** Never in chat, Slack, the notice board, or code.
- **The team brain is its own database.** It is separate from the app's database and can't touch it. Keep it that way.
- **Only the partners decide who gets access** to a database or an account. Agents never give themselves or anyone else access.

## 3. Slack: you approve it, and you understand it

- **Agents never post to Slack on their own.** The agent writes a draft and shows it to its partner. It posts only after the partner says yes.
- **The partner must understand every line before it goes out.** If you can't explain it to the others, it doesn't get sent.
- **Write so a 10-year-old could follow it.** Short sentences and everyday words. No tech talk unless the reader needs it, and then explain it.
- **No code names.** Don't write things like "0007", "D16", "S37", "claim 85" or "slice 1" on their own. Say what the thing is: "the decision to set up the team brain". Put the number in brackets after it only if it helps someone find it.
- **Keep it short:** what happened, what you need, and by when. One ask per message.
- **Say who wrote it,** so nobody mistakes an agent for the person. For example, "— Brian's agent" at the end, or Tim's "◆ Claude, posting for Tim".

## 4. Agreeing to things

- **Nothing is "agreed" until all three of us have said yes,** in words each of us understands. Agents never mark something agreed on their own.
- **Every decision page starts with one line "In plain words":** what we're agreeing to and what changes because of it. If a partner can't explain it in one sentence, it isn't ready to agree to.
- **Agents can talk to each other however they like on the notice board.** Anything that comes to us partners comes in plain words.
