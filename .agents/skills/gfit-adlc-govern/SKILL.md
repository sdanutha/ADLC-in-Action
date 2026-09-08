---
name: gfit-adlc-govern
description: Use when a human must decide whether to release a revision or resolve an Intent from observed outcome evidence.
metadata:
  author: "GFIT ADLC"
  version: "1.0.0"
---

# Govern

Keep consequential decisions with the accountable human. Read project instructions and the evidence for the named scope. Before Deploy use [the release decision template](assets/decision-template.md); after Observe use [the outcome resolution template](assets/resolution-template.md), unless the project defines its own records.

1. Before Deploy, compare the actual change with requirements, check risk and tie evidence to the current revision. Give an Approve/Revise/Stop recommendation and leave the human decision pending until the accountable person responds.
2. Record the actual human reply, reason, scope and time. On Revise, return to Generate and Validate. Material changes invalidate approval for that revision. Approval covers only the named target and rollout scope.
3. After Observe, check metric eligibility, target, every guardrail, confidence and missing evidence. Give a Resolved/Iterate/Stop recommendation without treating it as the human decision. A simulated exercise can test reasoning but cannot resolve the real product Intent; keep its scope explicit.
4. Create or update the project-defined resolution record with the human resolution pending, then record only the actual reply and reason. `Iterate` may propose input for a later Intent; it does not create that Intent or authorize implementation.

## Completion
Before Deploy, the decision record names the approved revision, target and scope. After Observe, the resolution record states Resolved, Iterate or Stop. Tests, elapsed time, deployment or an Agent recommendation never substitute for either human decision.
