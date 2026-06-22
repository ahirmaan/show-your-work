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

Claude either fires off a pile of generic questions before doing anything, or just guesses and you find out three messages later it got something wrong. Both cost more time than one well aimed question would have.

Say you ask Claude to build something, a website, a contract, a plan, and the prompt is missing a detail Claude actually needed. Right now it does one of two things. It interrogates you with questions that don't always matter, or it quietly fills the gaps with its own assumptions and hopes they land. When the guess is wrong, you're the one who has to notice, explain what's off, and wait for a redo. Sometimes more than once.

This skill replaces both habits with one rule. Figure out what's actually missing, ask only about the parts that would change the output, and if you'd rather skip the back and forth, go ahead anyway, but show exactly what got assumed. A wrong guess should cost one correction, not a full retry.

## Before / after

**Prompt:** *"Build me a website for my dental practice."*

**Without this skill**, Claude usually just builds something. It picks services, tone, and colors with no visibility into what got guessed, and you find out what's wrong by reading the whole thing.

**With this skill:**

> Before I build this, three things change the result a lot:
> 1. What services do you offer, general, cosmetic, pediatric, ortho?
> 2. Any brand colors or a logo, or should I pick a palette?
> 3. Who's the typical patient? It changes the tone a lot.
>
> Or just say "use your best judgment" and I'll go ahead. I'll flag exactly what I assumed.

Say "just guess," and the build still happens right away, but the response leads with this:

```
Assumptions made (no info given, so I picked defaults):
• Services: general + cosmetic dentistry, most common combo for a small practice
• Tone: warm, reassuring, typical for patient-facing healthcare sites
• Audience: local families and adults, not a pediatric specialty practice
• Colors: blue/white palette, common trust signal in healthcare

Swap any of these out and I'll rebuild just that part. No need to restate the whole brief.
```

One glance tells you what's real input and what's invention. Disagree with one bullet, say so, and only that part gets redone.

## How this is different from "interrogate me" skills

There's a well known style of skill that interviews you about a plan until every decision gets resolved before any work starts. That's genuinely useful when you want to think something through out loud with the model. This one is built for the opposite mood. You want one shot, fast, with full transparency on what got invented if you skip the conversation entirely. It only asks about gaps that would actually change the output, using a severity check rather than a fixed question count, and the "just guess, and show me" path is always offered as a real option, not an afterthought.

Neither approach is better in general. They suit different moments. Reach for this one when you want speed with receipts, not a design discussion.

## Install

This is a standard Claude Skill, just a folder with a `SKILL.md` file. Works with Claude Code, the Claude API, and Claude.ai where supported.

**Claude Code / personal skills:**
```bash
git clone https://github.com/ahirmaan/show-your-work.git
cp -r show-your-work ~/.claude/skills/show-your-work
```
Restart your Claude Code session, then ask it to do any underspecified task. It should trigger on its own. You can confirm it loaded by running `/skills`.

**Project-level (shared with a team via git):**
```bash
cp -r show-your-work .claude/skills/show-your-work
```

**Manual, no git:** download `SKILL.md` and `examples.md` from this repo and put them in a folder named `show-your-work` inside your skills directory.

## What's in this repo

```
show-your-work/
├── SKILL.md       the actual behavior: gap classification, severity triage, ask format, flag format
├── examples.md    two worked examples (website build, contract draft) showing the pattern end to end
├── README.md      this file
└── LICENSE        MIT
```

## Scope and limits

This is a v1, proven on purpose on two contrasting task types. A creative, visual deliverable (website) and a formal, legal one (contract), rather than claimed to work everywhere out of the box. The logic underneath, four gap categories and three severity tiers, is meant to generalize, but if you throw a very different kind of task at it and it asks the wrong things or misses something obviously important, that's useful to know. Open an issue with the prompt you used and what went wrong.

This skill does **not** remember anything across conversations or build a profile of your preferences over time. It's a single prompt completeness check. Does *this* request have enough information for *this* task, right now. Persistent memory across sessions is a different problem, solved by different tools.

## Contributing

Issues and PRs welcome, especially real examples of task types where the gap classification breaks down, asks about the wrong things, or misses a genuinely blocking gap. The goal is a skill that holds up across many kinds of requests, not just the two it shipped with.

## License

MIT, see `LICENSE`.
