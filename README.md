<div align="center">

```
 ███████╗██╗  ██╗ ██████╗ ██╗    ██╗
 ██╔════╝██║  ██║██╔═══██╗██║    ██║
 ███████╗███████║██║   ██║██║ █╗ ██║
 ╚════██║██╔══██║██║   ██║██║███╗██║
 ███████║██║  ██║╚██████╔╝╚███╔███╔╝
 ╚══════╝╚═╝  ╚═╝ ╚═════╝  ╚══╝╚══╝
   Y O U R   W O R K
```

**The Claude Skill that stops Claude guessing in the dark.**
Asks only what changes the output. Skips the rest. Shows you exactly what it invented when you tell it not to ask.

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Claude Skill](https://img.shields.io/badge/claude-skill-c77dff.svg)](SKILL.md)
[![Status](https://img.shields.io/badge/status-v1-orange.svg)](#scope-and-limits)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)

[Problem](#the-problem) · [Before/After](#before--after) · [Install](#install) · [Examples](examples.md) · [Scope](#scope-and-limits) · [Contributing](#contributing)

</div>

---

## The problem

Claude either interrogates you with generic questions before doing anything, or silently guesses and you find out it's wrong three messages later. Both cost more time than one well-aimed question would have.

You ask Claude to build something — a website, a contract, a plan — and the prompt is missing details Claude actually needs. Right now Claude does one of two things: asks a pile of generic clarifying questions before doing anything, or quietly fills the gaps with invented assumptions and hopes they're right. When the guess is wrong, you have to notice, explain what's off, and wait for a redo. Sometimes more than once.

This skill replaces both defaults with one rule: identify exactly what's missing, ask only about the parts that would actually change the output, and if you'd rather skip the back-and-forth, proceed anyway — but show you precisely what was assumed, so a wrong guess costs one correction instead of a full retry.

## Before / after

**Prompt:** *"Build me a website for my dental practice."*

**Without this skill**, Claude typically just builds something — picking services, tone, and colors with no visibility into what was guessed, leaving you to spot what's wrong by reading the whole output.

**With this skill:**

> Before I build this, three things change the result a lot:
> 1. What services do you offer — general, cosmetic, pediatric, ortho?
> 2. Any brand colors or a logo, or should I pick a palette?
> 3. Who's the typical patient? It changes the tone a lot.
>
> Or just say "use your best judgment" and I'll go ahead — I'll flag exactly what I assumed.

Say "just guess," and the build still happens immediately — but the response leads with this:

```
Assumptions made (no info given, so I picked defaults):
• Services: general + cosmetic dentistry — most common combo for a small practice
• Tone: warm, reassuring — typical for patient-facing healthcare sites
• Audience: local families and adults, not a pediatric specialty practice
• Colors: blue/white palette — common trust signal in healthcare

Swap any of these out and I'll rebuild just that part — no need to restate the whole brief.
```

One glance tells you what's real input and what's invention. Disagree with one bullet, say so, and only that part gets redone.

## How this is different from "interrogate me" skills

There's a well-known style of skill that interviews you relentlessly about a plan until every decision is resolved before any work starts — useful when you want to think something through out loud with the model. This skill is built for the opposite mood: you want one shot, fast, with full transparency on what got invented if you skip the conversation entirely. It only asks about gaps that would actually change the output (using a severity check, not a fixed question count), and it always offers the "just guess, and show me" path as a first-class option, not an afterthought.

Neither approach is better in general — they're suited to different moments. Reach for this one when you want speed with receipts, not a design discussion.

## Install

This is a standard Claude Skill — a folder with a `SKILL.md` file. Works with Claude Code, the Claude API, and Claude.ai (where supported).

**Claude Code / personal skills:**
```bash
git clone https://github.com/ahirmaan/show-your-work.git
cp -r show-your-work ~/.claude/skills/show-your-work
```
Restart your Claude Code session, then ask it to do any underspecified task — it should trigger automatically. You can confirm it loaded by running `/skills`.

**Project-level (shared with a team via git):**
```bash
cp -r show-your-work .claude/skills/show-your-work
```

**Manual / no git:** download `SKILL.md` and `examples.md` from this repo and place them in a folder named `show-your-work` inside your skills directory.

## What's in this repo

```
show-your-work/
├── SKILL.md       — the actual behavior: gap classification, severity triage, ask format, flag format
├── examples.md    — two worked examples (website build, contract draft) showing the pattern end to end
├── README.md      — this file
└── LICENSE        — MIT
```

## Scope and limits

This is a v1, deliberately proven on two contrasting task types — a creative/visual deliverable (website) and a formal/legal one (contract) — rather than claimed to work everywhere out of the box. The underlying logic (four gap categories, three severity tiers) is designed to generalize, but if you try it on a very different kind of task and it asks about the wrong things or misses something obviously important, that's useful signal — open an issue with the prompt you used and what went wrong.

This skill does **not** remember anything across conversations or build a profile of your preferences over time. It's a single-prompt completeness check — does *this* request have enough information for *this* task, right now. Persistent memory across sessions is a different problem, solved by different tools.

## Contributing

Issues and PRs welcome — especially real examples of task types where the gap classification breaks down, asks about the wrong things, or misses a genuinely blocking gap. The goal is a skill that holds up across many kinds of requests, not just the two it shipped with.

## License

MIT — see `LICENSE`.
