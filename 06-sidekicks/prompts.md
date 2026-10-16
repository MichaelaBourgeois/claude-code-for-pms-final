# 06 · Sidekicks — prompts

**Context:** You joined Rook two weeks ago as PM on Dispatch.
Release 4.2 shipped on 12 August, just before you arrived, and
landed badly. You've spent five sessions on it: finding out what
went wrong, then building the fix nobody had — a working prototype,
by hand, in one sitting, for one room.

At the end of the session, type wrap up, and Claude Code saves the
prompts you wrote yourself below — not the starter prompt — updates
CLAUDE.md, and saves your work to GitHub. By Module 6 this file is a
prompt library built from your own questions.

---

### 1.

I want to save a habit as something I can reuse. When I review a brief before it goes any further, here's what I actually check for:
- It names who owns it
- It says how we'll know it worked
- The scope at the end matches the scope at the start
- It explains the problem before it proposes a fix

Turn that into a skill called review-checklist, so I can point it at any brief and get the same check every time, without me explaining it again.

### 2.

I want to save a habit as something I can reuse. When I review a brief before it goes any further, here is what I check:
- It names who owns it
- It says how we will know it worked
- The scope at the end matches the scope at the start
- It explains the problem before it proposes a fix
- Every claim is labeled confirmed, likely, or unknown, with a source
- Numbers name their time window
- The timeline has owners and dates marked "proposed"
- It says what it deliberately does not do
- It fits the length limit (2 pages)

Turn this into a skill called review-checklist. If one already exists, update it instead of making a new one. When I point it at any brief, it should check each item, say Pass, Partly, or Missing with a short reason and a quote from the brief, then list the top 3 fixes. It must not invent facts or rewrite the brief unless I ask

### 3.

I want to save a habit as something I can reuse. When I review a brief before it goes any further, here is what I actually check for:
- It names who owns it
- It says how we will know it worked
- The scope at the end matches the scope at the start
- It explains the problem before it proposes a fix
- Every claim is labeled confirmed, likely, or unknown, with a source
- Numbers name their time window (for example "late August" vs "since 12 Aug")

Turn that into a skill called review-checklist, so I can point it at any brief and get the same check every time, without me explaining it again. If one already exists, update it instead of making a new one. For each item, say Pass, Partly, or Missing, with a short reason and a quote from the brief. Then list the top 3 fixes. Do not invent facts or rewrite the brief unless I ask.

### 4.

Schedule review-checklist to run every Monday morning, and let me know what it finds. Nothing needs to be ready for it to fire today. I'm setting the habit, not waiting on the result.