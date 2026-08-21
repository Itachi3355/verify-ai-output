# verify-ai-output

**An Agent Skill that audits AI-generated content before you trust it.**

As AI writes more of the world's content, the scarce skill is no longer generating — it's *verifying*. This skill gives Claude (or any agent that supports the [Agent Skills](https://code.claude.com/docs/en/skills) format) a systematic protocol for auditing AI-generated text and producing a structured **Trust Report**.

## What it does

Given any AI-generated content — a research summary, code explanation, medical answer, business report — the skill:

1. **Extracts and classifies every claim**: Factual / Inference / Speculation / Unverifiable
2. **Verifies checkable claims against primary sources** (web search, official docs, or programmatic checks for code), load-bearing claims first
3. **Scans for 8 hallucination risk patterns** — fabricated citations, composition errors, invented API features, temporal decay, false consensus, and more (see `references/risk-signals.md`)
4. **Audits the language layer** for overconfidence, vague attribution, and missing caveats
5. **Outputs a fixed-format Trust Report** ending with "What to check before relying on this" and "Limits of this audit"

The core principle: an audit that says "looks fine" is worthless. An audit that says *"these 3 claims are load-bearing and unverified — check them here"* is valuable even when the content is mostly correct.

## Install

**Claude.ai / Claude app:** upload `verify-ai-output.skill` (or this folder's `SKILL.md`) in a chat and tap **Save skill**.

**Claude Code:** copy this folder into your skills directory:

```bash
git clone https://github.com/itachi3355/verify-ai-output.git
cp -r verify-ai-output ~/.claude/skills/verify-ai-output
```

## Usage

Just paste AI-generated content and say any of:

- "Verify this"
- "Can I trust this AI report?"
- "Check this for hallucinations before I send it"
- "Audit this summary"

## Example (abridged)

Input (AI-generated):

> "Sleep deprivation definitively reduces cognitive performance by 43%, as proven by Harrison & Chen (2019). The WHO currently classifies sleep deprivation as a Group 1 carcinogen."

Trust Report verdict: **SIGNIFICANT PROBLEMS FOUND**

| Claim | Type | Verdict |
|---|---|---|
| "43%... Harrison & Chen (2019)" | Fact | No source found — citation-shaped fabrication |
| "WHO: Group 1 carcinogen" | Fact | **Contradicted** — IARC classifies *night shift work* as Group **2A** ("probably carcinogenic"), not sleep deprivation as Group 1 |

Full worked examples are in [`examples/`](examples/). Test prompts are in [`evals/evals.json`](evals/evals.json).

## Repo structure

```
verify-ai-output/
├── SKILL.md                    # The skill: workflow + Trust Report format
├── references/
│   └── risk-signals.md         # 8 hallucination patterns + prioritization rule
├── evals/
│   └── evals.json              # Test prompts for regression-testing the skill
├── examples/                   # Worked Trust Reports from real test runs
└── LICENSE                     # MIT
```

## Why this matters for AI safety

This skill operationalizes epistemic hygiene: calibration auditing, hallucination detection, claim-level provenance, and honest reporting of verification limits. It is deliberately built to *refuse self-leniency* — when asked to audit its own output, the agent applies the identical protocol.

Contributions welcome — especially new risk patterns for `references/risk-signals.md` and adversarial test cases for `evals/`.

## License

MIT
