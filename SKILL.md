---
name: show-your-work
description: Check whether the user's request has enough information to do the task well before producing output, instead of silently inventing missing details or asking generic clarifying questions. Use this whenever a task is underspecified in ways that would change the actual output — building a website, writing a contract, drafting a business plan, designing a brand, planning an event, writing a spec, or any deliverable where two competent people doing the same task from the same prompt would produce visibly different results. Always offer the user a choice: answer the specific gaps, or say "just use your best judgment" — and if they choose the latter, proceed but visibly flag every assumption made so the user can correct any single one without restarting the whole task. Do not use this for simple, fully-specified requests, or for tasks where guessing wrong costs nothing (e.g. "summarize this article," "fix this typo").
---

# Show Your Work

## The problem this solves

When a request is missing information a task actually needs, there are two bad defaults: ask a pile of generic clarifying questions before doing anything (slow, annoying, often asks about things that don't matter), or silently guess and hope (fast, but when the guess is wrong, the user has to notice, explain what's wrong, and wait for a redo — often more than once). Both waste more time than one well-aimed question would have.

The fix is to identify exactly what's missing, judge whether it's worth asking about at all, and if the user would rather skip the back-and-forth, proceed anyway — but make every invented detail visible, so a wrong guess costs one correction instead of a full retry.

## Step 1: Classify the task, not by name, but by what it commits to

Before writing anything, ask: **if two competent people did this same task from this same prompt, without talking to each other, where would their outputs differ?** Those points of divergence are the actual information gaps — not a checklist memorized per task type, but a question applied fresh to whatever the task is.

Sort whatever divergence you find into four buckets. Most tasks have something in each, though not always:

- **Output-shape facts** — things that change what the deliverable literally contains (for a website: which services to list; for a contract: which clauses apply). Guessing wrong here means the wrong content entirely, not just the wrong style.
- **Stylistic/brand facts** — tone, voice, visual identity. Guessing wrong here means the content is right but feels off.
- **Audience/context facts** — who this is for, what they already know, what they're deciding. Guessing wrong here means right content, wrong framing.
- **Constraint facts** — platform, length, budget, jurisdiction, deadline, format. Guessing wrong here can mean the output is unusable regardless of quality.

This frame is the part of this skill that generalizes. It works whether the task is a website, a legal document, a workout plan, a SQL schema, or a marketing email. Don't reach for a stored list of "what websites need" — reason it out for the specific request in front of you.

## Step 2: Triage each gap — not every gap deserves a question

This is the step that keeps this skill from turning into the same generic-clarifying-questions problem it's meant to fix. For each gap found in Step 1, classify its severity:

- **Blocking** — the task cannot proceed sensibly without this. A contract with no named jurisdiction. A dental site where "general, cosmetic, or pediatric" changes the entire structure, not just the wording.
- **Shaping** — the task can proceed, but a wrong guess produces something a human would visibly reject on sight. Brand colors. Tone. Target audience framing.
- **Cosmetic** — the task proceeds fine either way, and no reasonable person would care which default was picked. Exact button copy. Minor formatting choices.

**Only blocking and shaping gaps get surfaced to the user — as a question, or later as a flagged assumption.** Fill cosmetic gaps silently, with no mention at all. If everything gets flagged, the flags stop being useful; the entire point is that the user can tell real signal from noise at a glance.

If a gap is severe enough that an incorrect guess could be actively harmful or void (e.g. fabricating a governing-law clause in a contract, inventing a medical claim), do not offer to guess on that specific point — ask for it directly, even in "just guess" mode, and explain briefly why.

## Step 3: Ask, but only for what actually matters — and always offer the opt-out

If there are blocking or shaping gaps, ask about exactly those — nothing generic, nothing the prompt already answered. Always end with the explicit alternative to answering: proceeding under best judgment, with everything flagged.

Use this shape:

```
Before I [do the task], a few things change the result a lot:
1. [Specific blocking/shaping question — answerable in a phrase, not an essay]
2. [Next specific question]
3. [As many more as the task genuinely needs — see below for how to judge that]

Or just say "use your best judgment" and I'll go ahead — I'll flag exactly what I assumed so you can correct anything that's off.
```

There's no fixed number of questions to cap this at — a one-page landing site might have one real gap; a multi-party contract or a full brand system might legitimately have eight. The right number is "however many blocking/shaping gaps actually exist for this specific task," not a rule of thumb borrowed from a different kind of task. What matters is that every question on the list earns its place via Step 2's triage — if you're tempted to pad the list with anything cosmetic just to look thorough, cut it. A long list of all-necessary questions is fine; a short list padded with unnecessary ones defeats the point.

If the gaps are so extensive that answering them would basically mean designing the whole thing through Q&A (e.g. the task is really "help me figure out what I even want," not "build this for me"), say that plainly rather than dumping every question at once — it's a sign the request needs a different kind of conversation, not a longer list.

## Step 4: If the user opts to skip Q&A, proceed and flag

When the user says something like "just guess," "use your best judgment," "you decide," or simply doesn't answer the clarifying questions and asks for the output anyway — produce the task, then lead with a compact assumptions block, before or alongside the actual deliverable (not buried at the end where it's easy to skip past).

ALWAYS use this exact shape for the flag block:

```
Assumptions made (no info given, so I picked defaults):
• [Gap]: [what was assumed] — [one short reason this default was reasonable]
• [Gap]: [what was assumed] — [one short reason this default was reasonable]
• [Gap]: [what was assumed] — [one short reason this default was reasonable]

Swap any of these out and I'll redo just that part — no need to restate the whole brief.
```

Rules for this block:
- Only list blocking/shaping assumptions — never list cosmetic defaults here, even though they were also guessed. This keeps the block short enough to actually be read.
- Give a one-line reason for each assumption, not just the assumption itself. "Blue/white palette — common trust signal in healthcare" lets the user judge whether your reasoning was sound, not just whether they like the color.
- Keep it to bullets, not prose. It needs to be scannable in a few seconds, not read like an explanation.
- End with the cheap-correction line every time. That line is what actually saves the user time — it tells them they can fix one bullet instead of rewriting the whole prompt.

## Step 5: When the user answers some but not all gaps

Treat answered gaps as settled facts — don't re-ask or second-guess them. For any gaps the user's answer didn't cover, apply Step 4's flagging to just those remaining ones. Partial answers are common; this skill should handle them gracefully rather than insisting on all-or-nothing.

## What this skill is not

This is not about remembering things across conversations, learning the user's preferences over time, or building a profile. It's a single-prompt check: does *this* request have enough information for *this* task, right now, regardless of any history. If the user has a persistent-memory tool or has told Claude their preferences before, that's separate context this skill doesn't manage or replace.

This also isn't a tool for interrogating the user on every detail of a plan before any work happens — if that's what's wanted, a different approach (lots of sequential questions, working through a full decision tree together) fits better. This skill is for the opposite situation: minimal necessary friction, maximum visible honesty about what got invented when friction was skipped.

## Worked examples

See `examples.md` for two full worked examples — a website build and a contract draft — showing the gap classification, the ask, and the flag format applied end to end.
