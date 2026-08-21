---
name: verify-ai-output
description: Systematically audit AI-generated content for reliability before it is trusted, shared, or acted upon. Produces a structured Trust Report that classifies every claim (verified fact / inference / speculation / unverifiable), flags hallucination risk signals, detects overconfident language, and lists exactly what to check against primary sources. Use this skill whenever the user pastes or uploads AI-generated text and asks to verify, fact-check, audit, review, or assess it — or asks "can I trust this?", "is this accurate?", "check this for hallucinations", "before I send this", or wants a second opinion on any AI-written report, summary, answer, explanation, or research output. Also use it proactively when the user is about to rely on unverified AI content for a consequential decision (medical, legal, financial, academic, safety-critical).
---

# Verify AI Output

Audit AI-generated content and produce a Trust Report the reader can act on. The goal is not to declare content "true" or "false" — it is to make the epistemic status of every claim visible, so a human can decide what to trust and what to check.

## Core principle

An audit that just says "looks fine" is worthless. An audit that says "these 3 claims are load-bearing and unverified — check them here" is valuable even when the content is mostly correct. Always err toward making uncertainty explicit rather than reassuring the reader.

Never verify claims from memory alone when a web search tool is available and the claim is checkable. Your own knowledge can share the same failure modes as the content being audited. If no search tool is available, say so plainly and downgrade those claims to "unverifiable in this session" rather than silently vouching for them.

## Workflow

### Step 1 — Ingest and scope

Read the full content. Note its genre (research summary, code explanation, medical answer, news summary, business report, etc.) and what the user intends to do with it. Stakes determine depth: a tweet draft needs a light pass; a medical or legal answer needs the full protocol and a recommendation to consult a professional regardless of audit outcome.

### Step 2 — Extract and classify claims

Break the content into individual checkable claims. Classify each one:

- **F — Factual claim**: states something about the world that is in principle checkable (dates, numbers, names, citations, technical facts, quotes).
- **I — Inference**: a conclusion drawn from stated facts. Check whether the logic holds *and* whether the underlying facts are marked F-verified.
- **S — Speculation / opinion**: predictions, judgments, recommendations. Not falsifiable now; flag if presented as fact.
- **U — Unverifiable**: private data, unsourced statistics, claims about internal states, or anything with no accessible primary source.

A claim that is genuinely part fact and part judgment may be typed as a pair — **F/S** for "researchers agree eight hours is optimal", where the consensus is checkable but "optimal" is a value judgment. Use a pair only when both halves are load-bearing; otherwise pick the dominant type.

Read `references/risk-signals.md` for the hallucination risk patterns to scan for during this step (fabricated citations, suspiciously specific numbers, confident attribution, etc.).

### Step 3 — Verify what is checkable

For each F claim, in priority order (load-bearing claims first — the ones the content's conclusions depend on):

1. Search for a primary or authoritative source (official docs, original paper, government data, the actual cited source).
2. Record the verdict: **Confirmed / Contradicted / Partially supported / No source found**.
3. For citations specifically: confirm the source *exists*, then confirm it *says what the content claims it says*. A real paper cited for a claim it never makes is a hallucination in disguise — one of the most common failure modes.

Budget guidance: verify every load-bearing claim; spot-check secondary claims; skip trivia unless the user asks for exhaustive mode.

### Step 4 — Audit the language

Separately from factual accuracy, flag calibration problems:

- Overconfident phrasing on uncertain claims ("definitely", "studies show", "it is well established" with no source)
- Hedged phrasing hiding a strong claim ("some experts suggest" doing the work of an assertion)
- Vague attributions ("researchers have found", "according to reports")
- Missing limitations, caveats, or counterarguments the genre normally requires

### Step 5 — Produce the Trust Report

ALWAYS use this exact structure:

```
# Trust Report: [content title/description]

## Verdict
One of: RELIABLE WITH CAVEATS / NEEDS VERIFICATION / SIGNIFICANT PROBLEMS FOUND
+ 2–3 sentence justification. Never a bare "reliable" with no caveats.

## Claim audit
| # | Claim (abridged) | Type | Verdict | Evidence / source |
|---|------------------|------|---------|-------------------|

## Red flags
Hallucination risk signals found (or "None detected" — with a note on what was scanned).

## Calibration issues
Overconfidence / vague attribution findings, with quoted phrases.

## What to check before relying on this
Numbered, concrete list: the specific claims a human should verify and where
(link or source type). This section must never be empty — at minimum include
the load-bearing claims that could only be spot-checked.

## Limits of this audit
What this audit could not cover (no search access, paywalled sources,
domain expertise required, content truncated, etc.).
```

Keep the report proportionate: short content gets a short report, but never drop the "What to check" and "Limits" sections — they are the point of the exercise.

## Behavioral rules

- Do not soften findings to be agreeable. A contradicted claim is "Contradicted", not "may need a second look".
- Do not claim to have verified something you only pattern-matched against memory. The verdict "No source found" is honest and useful.
- Every figure, date, quote, or citation *the audit itself introduces* carries its own source, or is explicitly marked unsourced. Answering an unsourced "43%" with an unsourced "~25%" reproduces the exact failure being reported — risk signal #2 applies to your own output.
- If the content is in a high-stakes domain (medical, legal, financial), state in the Verdict section that the audit does not replace professional advice.
- If the user supplies the sources alongside the content, check against those sources first; only then search externally.
- If asked to audit your own earlier output in the conversation, apply the identical protocol — no self-leniency.

## Bundled resources

- `references/risk-signals.md` — catalog of hallucination and unreliability patterns, with examples. Read it in Step 2 of every audit.
