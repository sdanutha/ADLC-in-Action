---
name: gfit-adlc-validate
description: Use when defining acceptance checks, examining generated artifacts, verifying behavior, or evaluating evidence for a current revision.
metadata:
  author: "GFIT ADLC"
  version: "1.0.0"
---

# Validate

Define credible proof before generation and evaluate evidence against the active Intent. Read project instructions, acceptance criteria and the current revision. Use `gfit-adlc-generate` as a feedback loop and use [the evidence template](assets/validation-template.md) when the project has no report format.

1. Map each applicable requirement to expected behavior and an automated, analytical or manual proof. Distinguish implementation acceptance from outcome metrics.
2. Review generated design artifacts against the Intent, project policies, interfaces, lifecycle, observability and reproducibility. Return concrete gaps to Generate. A human owns approval.
3. Before implementation, establish evidence of the missing behavior. For code, prefer a behavior-derived failing test; setup errors are not behavioral evidence. Use stable public boundaries, controlled inputs, isolated test data and expectations independent of the implementation.
4. On failure, reproduce and localize one cause before requesting a repair. Preserve the acceptance requirement. If a test is wrong, cite the spec evidence and record the correction; never use skips or weaker assertions to manufacture green.
5. Run the project-defined validation commands and applicable manual checks. Map every requirement to actual evidence. Record command or method, result, revision and initial/final evidence. If tooling or data is unavailable, mark `NOT RUN` or `INSUFFICIENT EVIDENCE`.
6. Save the project-defined validation record; default to `validation.md` when no path is specified. Passing checks establish technical evidence only. They do not approve a release or resolve the Intent.

## Completion
The report separates automated results, analytical results, manual checks and outcomes not yet measured. Preserve evidence from earlier revisions. Validation does not authorize Deploy or resolve the Intent.
