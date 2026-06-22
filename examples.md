# Worked Examples

Two scenarios, chosen deliberately for contrast rather than similarity: one creative/visual (gaps are mostly brand, audience, content), one legal/formal (gaps are mostly constraint-level, where a wrong guess isn't just ugly, it can be void or dangerous). If the underlying gap-classification logic in SKILL.md holds up across both, it's likely to generalize to most other task types too.

---

## Example 1: Website build (creative deliverable)

**User prompt:**
> Build me a website for my dental practice.

**Step 1 — classify the gaps using the four buckets:**

- *Output-shape*: which services are offered (general, cosmetic, pediatric, ortho?) — unknown. Number of pages — unknown.
- *Stylistic/brand*: tone (warm/reassuring vs. clinical/efficient), brand colors, existing logo — unknown.
- *Audience/context*: who the typical patient is (families, anxious patients, young professionals) — unknown.
- *Constraint*: platform/hosting, must-have sections (booking form? insurance info?) — unknown.

**Step 2 — triage:**

- Blocking: services offered (changes the entire site structure, not just wording).
- Shaping: tone, brand colors, target patient profile.
- Cosmetic: exact button copy, footer layout, stock photo choices — fill these silently, never mention.

**Step 3 — the ask:**

> Before I build this, three things change the result a lot:
> 1. What services do you offer — general dentistry, cosmetic, pediatric, ortho, or some mix?
> 2. Any existing brand colors or a logo, or should I pick a palette?
> 3. Who's the typical patient — families, young professionals, people who are a bit anxious about dental visits? It changes the tone a lot.
>
> Or just say "use your best judgment" and I'll go ahead — I'll flag exactly what I assumed so you can correct anything that's off.

**If the user replies "just use your best judgment, go ahead":**

The site gets built, and the response leads with:

```
Assumptions made (no info given, so I picked defaults):
• Services: general + cosmetic dentistry — the most common combination for a solo or small practice
• Tone: warm and reassuring, not clinical — typical for patient-facing healthcare sites, since most people don't love going to the dentist
• Audience: local families and adults, not a pediatric-only specialty practice
• Colors: blue and white palette — a common trust signal in healthcare branding

Swap any of these out and I'll rebuild just that part — no need to restate the whole brief.
```

Note what's absent: no mention of the stock photos chosen, the exact footer text, or other cosmetic defaults. Flagging those would bury the assumptions that actually matter.

---

## Example 2: Contract draft (formal/legal deliverable)

**User prompt:**
> Draft a freelance contract for a web design project I'm doing for a client.

**Step 1 — classify the gaps:**

- *Output-shape*: payment structure (fixed fee vs. milestones vs. hourly), deliverables, revision limits — unknown.
- *Stylistic*: largely irrelevant here — legal documents have less stylistic variance than creative ones. (Not every bucket applies equally to every task; that's expected.)
- *Audience/context*: is the client a business or an individual — affects some standard clauses.
- *Constraint*: which jurisdiction's law governs, payment terms/late fees, IP ownership transfer timing, termination conditions — unknown, and some of these are not safe to guess.

**Step 2 — triage, including the harm carve-out:**

- Blocking: governing jurisdiction, payment structure, IP ownership terms — the contract is genuinely unusable or risky without these.
- Shaping: revision limits, termination notice period, late fee structure.
- Cosmetic: section headers, formatting style, exact recital language.
- **Harm carve-out applies**: jurisdiction and IP ownership terms are exactly the kind of gap where guessing wrong isn't just "off-tone," it can make the contract unenforceable or sign away rights incorrectly. Per Step 2, these get asked directly even if the user says "just guess" on everything else.

**Step 3 — the ask:**

> Before I draft this, a few things matter a lot for a contract specifically:
> 1. Which jurisdiction's law should govern this agreement (your state/country, the client's, or somewhere else by agreement)?
> 2. How is payment structured — fixed fee, milestones, or hourly — and what are the terms (deposit, due dates)?
> 3. Who owns the design work and IP, and when does ownership transfer — on final payment, or immediately?
> 4. Any revision limits or termination terms you want included, or should I use standard freelance defaults?
>
> Questions 1 and 3 I'd rather not guess on — a wrong assumption there can make the contract unenforceable or transfer rights incorrectly. For the others, just say "use your best judgment" and I'll flag what I assumed.

Notice the ask itself explains *why* two of the four questions aren't skippable — this is the harm carve-out from Step 2 surfacing at the asking stage, not just the flagging stage.

**If the user answers jurisdiction and IP, but says "guess on the rest":**

```
Assumptions made (no info given for these, so I used standard defaults):
• Payment: 50% deposit upfront, 50% on delivery — common structure for freelance web design
• Revision limit: two rounds of revisions included, additional rounds billed hourly — standard to prevent scope creep
• Termination: either party can terminate with 14 days' written notice — a common neutral default

Jurisdiction and IP terms are set as you specified, not guessed.
Swap any of the above out and I'll redo just that clause — no need to restate the whole brief.
```

This is Step 5 in action: settled facts (jurisdiction, IP) are stated as given, not re-flagged or hedged, and only the genuinely-guessed remainder gets the assumption treatment.

---

## What carries over to other task types

Looking at both examples side by side, the parts that transferred without modification were the four-bucket classification, the blocking/shaping/cosmetic triage, and the flag-block format. The parts that were genuinely different were *which* buckets had content (the contract's stylistic bucket was nearly empty; the website's wasn't) and the harm carve-out mattering a lot more for the contract than the website. That's the expected shape of a generalizable skill: same reasoning process, different output depending on what the task actually needs.
