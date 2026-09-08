---
name: gfit-adlc-observe
description: Use when examining outcome signals after a release, experiment, operational change, or explicitly labeled simulation.
metadata:
  author: "GFIT ADLC"
  version: "1.0.0"
---

# Observe

Evaluate the predeclared signal and guardrails without rewriting the hypothesis after seeing results. Read project instructions, the Intent, release record, metric definitions and available data. Use `gfit-adlc-govern` after the evidence report is ready. Use [the observation template](assets/observation-template.md) when the project has no report format.

1. Verify provenance before assigning an evidence class. Record source, collection method, revision or cohort, window and cutoff, unit of analysis, eligible population and completeness. Never relabel synthetic or test evidence as real. Report missing fields, duplicates, invalid ordering and exclusions.
2. Apply the metric grain, calculation or aggregation method, business rules and follow-up window declared in the Intent or project contract. Do not substitute a convenient proxy or combine incompatible populations.
3. Calculate results with units and show the inputs needed to reproduce them. For ratios, zero denominators are N/A. When comparing rates, report percentage-point and relative change separately; a zero baseline makes relative change undefined.
4. Evaluate the target and every guardrail separately. Meeting a target while breaching a guardrail is not overall success. Keep technical correctness, outcome signal and causal confidence distinct.
5. Explain evidence limits. Synthetic data tests reasoning only; repeated observations from one actor do not create independent actors; uncontrolled comparisons do not prove causality. If evidence is absent or immature, report insufficient evidence without manufacturing values.
6. State what the signal supports, what remains unknown and which options deserve human judgment. Hand the completed evidence to Govern. Do not choose Resolved, Iterate or Stop, and do not create the next Intent automatically.

## Completion
The project-defined observation record includes source, cutoff, population, formulas, counts, exclusions, target and guardrail verdicts, confidence and limitations. Keep simulated, test and real evidence separate. Govern records the later human resolution.
