# Worked Examples

Trust Reports produced by the skill during testing. Use these as reference for the expected output quality and format.

---

## Example 1 — Health blog paragraph (Eval #1)

**Input:** "Sleep deprivation definitively reduces cognitive performance by 43%, as proven by Harrison & Chen (2019, Journal of Cognitive Science). Researchers agree that eight hours is the universally optimal sleep duration for all adults. The WHO currently classifies sleep deprivation as a Group 1 carcinogen. Since memory consolidation occurs during REM sleep, students should always study immediately before bed."

# Trust Report: Sleep & cognition blog paragraph

## Verdict
**SIGNIFICANT PROBLEMS FOUND.** One claim is directly contradicted by primary sources, one citation could not be located, and the confident universal language is not supported. Do not publish without rewriting. This is health content — the audit does not replace professional medical review.

## Claim audit
| # | Claim (abridged) | Type | Verdict | Evidence / source |
|---|---|---|---|---|
| 1 | Cognitive performance reduced by 43% per Harrison & Chen (2019) | F | No source found | No matching paper located; "Journal of Cognitive Science" + author pair + precise 43% figure fits the fabricated-citation pattern |
| 2 | Researchers agree 8h is universally optimal for all adults | F | Contradicted | Sleep-need guidance (e.g., AASM/Sleep Research Society) gives a *range* (7+ hours) and notes individual variation; no universal consensus on exactly 8h for all |
| 3 | WHO classifies sleep deprivation as Group 1 carcinogen | F | **Contradicted** | IARC (WHO's cancer agency) classifies *night shift work* as Group **2A** ("probably carcinogenic to humans"), reaffirmed 2019 (IARC Monographs Vol. 124). Wrong agent, wrong category |
| 4 | Consolidation occurs during REM → study right before bed | I | Logic gap | Consolidation also occurs in slow-wave sleep; even if the premise held, "always study immediately before bed" doesn't follow from it |

## Red flags
- Citation-shaped fabrication (signal #1): plausible authors + year + journal, no locatable paper
- Suspiciously specific number (signal #2): "43%"
- Composition error (signal #6): real IARC classification (night shift work, 2A) morphed into a false one (sleep deprivation, Group 1)

## Calibration issues
- "definitively", "as proven by", "universally", "always" — absolute qualifiers on contested/unsupported claims
- "Researchers agree" — false consensus with no citation

## What to check before relying on this
1. Search Google Scholar for the exact Harrison & Chen (2019) paper; if it cannot be found, delete claims 1's figure entirely.
2. Replace claim 3 with the accurate IARC statement (night shift work, Group 2A) and cite IARC Monographs Vol. 124.
3. Replace claim 2 with a sourced range from AASM or NIH sleep guidance.

## Limits of this audit
Verification used web search of secondary/primary sources; the IARC monograph itself was not read in full. No sleep-medicine domain expert reviewed the rewrite suggestions.

---

## Example 2 — Python API claim (Eval #2)

**Input:** "The requests library's requests.get() has supported a built-in retries parameter since version 2.25, so you can just write requests.get(url, retries=3)."

# Trust Report: requests retry claim

## Verdict
**SIGNIFICANT PROBLEMS FOUND.** The central claim is contradicted by the library's actual API, verified programmatically.

## Claim audit
| # | Claim (abridged) | Type | Verdict | Evidence / source |
|---|---|---|---|---|
| 1 | `requests.get()` accepts `retries=` since v2.25 | F | **Contradicted** | Inspected `requests.get` signature in requests 2.33.1: parameters are `(url, params, **kwargs)`; passing `retries=3` reaches the adapter layer where it is not a supported request kwarg. Retries are configured via `requests.adapters.HTTPAdapter(max_retries=...)` mounted on a `Session` (or `urllib3.util.Retry`) |

## Red flags
- Invented API feature (signal #4) — fluent, plausible, wrong. The single most common failure mode in AI-generated code advice.
- Suspiciously specific version number ("since 2.25") attached to a feature that never existed.

## What to check before relying on this
1. Run `inspect.signature(requests.get)` in your own environment, or read the official requests docs on transport adapters.

## Limits of this audit
Verified against requests 2.33.1 locally; behavior in hypothetical future versions not checked (the claim's "since 2.25" framing was checked against the changelog pattern, not every historical release).

---

## Example 3 — Business deck stats (Eval #3)

**Input:** "Studies show that remote teams are 40% more productive than in-office teams. Many experts believe hybrid work is now the permanent standard, and it could be argued that companies mandating office returns will inevitably lose their best talent."

# Trust Report: Remote-work deck paragraph

## Verdict
**NEEDS VERIFICATION.** Nothing here is checkably false as written — because almost nothing here is checkable as written. The paragraph presents speculation in the costume of research.

## Claim audit
| # | Claim (abridged) | Type | Verdict | Evidence / source |
|---|---|---|---|---|
| 1 | "Studies show" remote teams 40% more productive | F | No source found | No specific study cited; published research on remote productivity is mixed and highly methodology-dependent. The bare "40%" is unanchored |
| 2 | Hybrid work is now the permanent standard | S | — | Prediction phrased as expert consensus ("many experts believe") |
| 3 | RTO mandates will inevitably cost best talent | S | — | "It could be argued" + "inevitably": a hedge and an absolute in the same sentence |

## Red flags
- Vague attribution (signal #3): "studies show", "many experts believe"
- Suspiciously specific number (signal #2): "40%"

## Calibration issues
- "inevitably" — absolute qualifier on a prediction
- "it could be argued" — hedge smuggling an assertion the deck treats as a conclusion

## What to check before relying on this
1. Find and cite the actual study behind "40%" (or cut the number). Candidate real literature: Stanford/Bloom WFH studies — but note their findings are more nuanced than a flat 40%.
2. Rephrase claims 2–3 explicitly as your company's *position*, not as established fact.

## Limits of this audit
No search performed on the contested productivity literature beyond confirming no single canonical "40%" source exists; a literature review would be needed to state the true effect range.
