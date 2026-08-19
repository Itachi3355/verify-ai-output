# Hallucination & Unreliability Risk Signals

Scan the content for these patterns during claim extraction. A signal is not proof of error — it raises the priority of verification for the claims it touches.

## 1. Citation-shaped fabrications
- Author names + year + plausible journal, but no DOI/link, or a link that doesn't resolve.
- Real authors paired with a paper title they never wrote.
- Real paper cited for a claim it does not make (verify the *content* of the source, not just its existence).
- Legal citations with correct formatting but nonexistent case numbers.

**Example:** "As shown in Smith et al. (2021, Nature Neuroscience), memory consolidation doubles during REM sleep." → Verify the paper exists AND makes that specific quantitative claim.

## 2. Suspiciously specific numbers
- Precise statistics with no source ("increases productivity by 37%").
- Round-number chains that look like invented benchmarks ("improved accuracy from 82% to 94%").
- Dates and version numbers for events near or after the generating model's knowledge cutoff.

## 3. Confident attribution
- Named quotes from real people ("As Einstein said…") — famous-person quotes are among the most-fabricated content categories.
- "Studies show", "researchers agree", "it is well documented" with no citation.
- Institutional claims ("the WHO recommends…") — check the current, actual guidance; recommendations change.

## 4. Plausibility padding
- Technical explanations that are fluent but circular (defining the term with its own synonyms).
- Feature lists for products/APIs that mix real capabilities with invented ones (very common for software: check each function/flag/parameter against official docs).
- Historical narratives that smooth over genuine ambiguity or scholarly disagreement.

## 5. Temporal risk
- Anything stated in the present tense about leadership, prices, laws, versions, or availability ("the current CEO is…", "the latest version supports…"). These decay fast; verify with a fresh search regardless of how confident the phrasing is.

## 6. Composition errors
- Two individually true claims combined into a false one ("X was founded in 1998" + "X's founder invented Y" → wrong founder credited).
- Correct data attached to the wrong entity (right statistic, wrong country/company/year).

## 7. Calibration red flags (language layer)
- Absolute qualifiers: "always", "never", "proven", "definitely", "undeniably".
- Hedges that smuggle assertions: "many believe", "it could be argued", "some say" followed by a claim treated as established downstream.
- Missing standard caveats for the genre (medical content without contraindications; financial content without risk disclosure; benchmarks without methodology).

## 8. Structural signals
- Uniform confidence across all claims — real expert writing varies its certainty.
- No acknowledged limitations anywhere in a research-style document.
- Perfectly balanced "on one hand / on the other hand" for questions that actually have a settled answer (false balance), or a one-sided treatment of a genuinely contested question (false certainty).

## Prioritization rule

When time or search budget is limited, verify in this order:
1. Claims the content's main conclusion depends on (load-bearing).
2. Claims the user will act on directly.
3. Citations and quotes (high fabrication rate, cheap to check).
4. Numbers and dates.
5. Everything else, spot-checked.
