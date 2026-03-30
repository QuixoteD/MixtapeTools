# Fletcher: Own All the Numbers

*A defamiliarization audit for empirical output.*

---

## The Story Behind This Skill

In March 2026, Scott Cunningham published a Substack post claiming that AI-generated economics papers from the Social Catalyst Lab's APE project showed evidence of p-hacking. The evidence was a Brodeur ratio of 1.52 — 52% more reconstructed t-statistics just above the 1.96 significance threshold than just below. He had used Claude Code to extract coefficients and standard errors from 651 LaTeX manuscripts and divided them to construct t-statistics.

Jason Fletcher left a comment a few days later:

> "Can you say something about rounding vs. p-hacking? What do you make of the huge spike at t-stat=1 in your first figure?"

Scott had looked at that figure many times before publishing. The spike at t=2 was what he was writing about. The spike at t=1 was sitting in the same figure. He had registered it and classified it as noise without asking why it was there — because the story he wanted to tell had already automated his perception.

That was the mistake. The spike at t=1 is the tell. There is no p-hacking story that produces a spike at t=1 — that value has no significance threshold. No researcher, human or AI, has any incentive to push results toward t=1. But rounding does produce it, for the same reason it produces spikes at t=2 and t=3: dividing two small rounded numbers yields a ratio of two small integers, and 1:1, 2:1, and 3:1 are the most common small integer ratios.

After removing the 68 exact-t=2 cases from the bunching window, the Brodeur ratio dropped from 1.52 to 1.02. The original p-hacking finding was entirely an artifact of computing coef/SE from rounded numbers extracted from a table, rather than using software-output t-statistics directly.

The full account, including the rounding mechanism and a simulation, is in [Claude Code 36](https://causalinf.substack.com/p/claude-code-36-i-was-wrong-about).

---

## Why Fletcher

Jason Fletcher described his practice as something he learned from his own graduate training — the habit of reviewing a student's table by stepping back from the main coefficient and asking about something else: an odd pattern, an unexpected sign, a sample size that didn't add up. More often than you'd like to admit, that question mattered.

After the exchange with Scott, Fletcher wrote a Substack post generalizing the lesson: [**"Owning All the Numbers: Why every number in your output is your responsibility"**](https://jasonmfletcher.substack.com/p/owning-all-the-numbers). It's worth reading in full. The argument is that research training tends to focus on getting *the coefficient of interest* — clean data → run model → format key output — but the real task is owning the table. Owning it means that every number in it, before anyone asks, is something you've already interrogated.

That habit is what Scott needed before he published. Fletcher approached the figure without a stake in the p-hacking conclusion and asked about the number Scott wasn't explaining. This skill tries to institutionalize that practice.

The Viktor Shklovsky principle: *art exists to defamiliarize — to make the stone stony again.* Habit makes perception automatic. We stop seeing our output because we've already decided what it means. The purpose of this audit is to break that. To make you see the figure as a stranger would, before the story has collapsed everything else into background noise.

---

## What This Skill Does

Fletcher is a checklist for auditing empirical output — a figure, table, or set of results — before you interpret or write about it. Six steps, each completed and crossed off. A ruling at the end: **CLEAR**, **CONDITIONAL**, or **HOLD**.

**Invoke it when:** you have output and are about to interpret or report it. Before writing begins. Before deciding what it means.

---

## The Six Steps

### Step 1: List Everything

Before interpreting anything, enumerate every visible feature of the output. Every coefficient and its sign. Every spike, dip, or discontinuity. Every pattern across columns. Every sample size. Every number that appears anywhere.

The main result is one item on this list. Write the full list before proceeding.

*The rule: if you can't list it, you haven't looked at it.*

---

### Step 2: What Would Generate This?

For each item on the list, ask: *what would generate this?*

Not "what does this mean for my hypothesis" — what could cause this feature, including explanations that have nothing to do with your hypothesis.

Work through mundane explanations first: rounding or discretization? Sample restriction? Measurement issue? Small-N noise? Then move to substantive explanations.

*The rule: "that's just noise" requires justification, not assertion.*

---

### Step 3: Find the Hardest One

Identify the single feature most difficult to explain under your preferred interpretation. State it. Attempt to explain it. If you cannot, flag it.

*The rule: the hardest feature is where the real problem lives, if there is one. Don't bury it.*

---

### Step 4: Own the Sample Size

Does N make sense? Is it the number you expected? If it changed from a prior run, do you know why? Are there dropped observations you haven't accounted for?

A sample size mismatch almost always traces to an undocumented decision.

*The rule: if you can't explain your N, you don't understand your data.*

---

### Step 5: Check the Pattern

Look across specifications, subgroups, time periods, or outcome variants. Do the signs cohere? Do the magnitudes tell a consistent story? Are there reversals or jumps you haven't addressed?

A single coefficient lives inside a pattern. If you don't have a story for the pattern, you don't yet understand the project.

*The rule: explain the whole pattern, not just the cell you care about.*

---

### Step 6: The Ownership Test

If someone pointed to any number in this output and said "what's going on with this?" — do you have an answer?

Go through the Step 1 list. For each item: can you give an account of it? If there is any number you would shrug at, you are not done.

*The rule: you don't own the output until you can account for all of it.*

---

## The Report

After the six steps, produce a Fletcher Report:

```
## Fletcher Report
**Output:** [what was audited]
**Date:** YYYY-MM-DD

### Step 1: Features Listed
[full list]

### Step 2: What Would Generate This?
[for each feature: candidate explanations]

### Step 3: Hardest Feature
[what it is, whether resolved, FLAG if not]

### Step 4: Sample Size
[N, whether it makes sense, any issues]

### Step 5: Pattern Check
[coherence assessment]

### Step 6: Ownership Test
[pass / fail / partial]

### Ruling
[ ] CLEAR — proceed to interpretation
[ ] CONDITIONAL — proceed but acknowledge open questions explicitly
[ ] HOLD — do not interpret or publish until flagged items are resolved
```

---

## Fletcher and Referee 2: Complements, Not Substitutes

**Both should be run. Neither replaces the other.**

| | Fletcher | Referee 2 |
|---|---|---|
| **Question** | Do you understand what you're looking at? | Is this implemented correctly? |
| **Timing** | When output first appears, before writing | After the project is complete, fresh session |
| **Persona** | Mentor at the whiteboard | Health inspector with a checklist |
| **Catches** | Misinterpretation, confirmation focus, unexplained features | Coding errors, replication failures, bad controls |
| **Would have caught the t=1 spike?** | Yes | No |
| **Would have caught a merge error?** | Maybe | Yes |

**Why they are separated from each other:**

Fletcher runs *during* analysis, in the same session, at the moment output appears. It is a pause — not a handoff. You invoke it yourself, on your own output, before you decide what it means. It doesn't require a fresh session because it isn't auditing implementation — it's auditing your perception of your own output.

Referee 2 runs *after* the project is complete, in a new terminal, by a Claude instance that has never seen the work. That separation is what gives it independence. The same Claude that built the pipeline cannot objectively audit it — it will rationalize its own choices and confirm its own assumptions. Independence is what makes the audit credible.

**The workflow:**

1. Produce output → `/fletcher` → interpret and write
2. Complete project → open fresh terminal → `/referee2`

Running Fletcher first makes Referee 2 more useful: interpretation problems are caught before the implementation audit begins, so Referee 2 can focus on what it does best.

---

## Installation

The Claude Code skill lives at `.claude/skills/fletcher/SKILL.md` in this repo. To use it, ensure this repo is on your Claude Code skills path. Invoke with `/fletcher` followed by a path to the figure or table and a brief description of what you think the main finding is.

See the [skills README](../README.md) for general installation instructions.
