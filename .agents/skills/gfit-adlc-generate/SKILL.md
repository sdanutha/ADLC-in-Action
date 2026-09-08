---
name: gfit-adlc-generate
description: Use when producing or revising artifacts for a confirmed Intent, including specifications, plans, implementation, tests, documentation, or configuration.
metadata:
  author: "GFIT ADLC"
  version: "1.0.0"
---

# Generate

Produce the smallest coherent artifacts that test a confirmed Intent. Read project instructions, the Intent and current evidence. Use `gfit-adlc-validate` as a feedback loop: Validate defines checks and returns gaps while Generate creates or revises artifacts. Project bindings supply paths, stack, commands and policies.

1. When design artifacts are needed, use [the document templates](assets/spec-plan-templates.md) or the project's format. Translate the Intent into behavior, boundaries, interfaces, state, observability, risks and small deliverable slices. Do not implement while the project requires design approval.
2. Present design artifacts at the applicable human checkpoint. Record approval only from an actual reply.
3. During implementation, work one accepted behavior at a time. Start from the proof supplied by Validate, observe the expected gap or failure, create the smallest implementation, then return evidence to Validate.
4. Apply Validate feedback without weakening the Intent, acceptance criteria or guardrails. A corrected test requires documented spec evidence. Preserve earlier Intent evidence and keep generated files within the approved scope.
5. Produce only artifacts required by the approved plan and project contract. Never claim that generated checks prove their own correctness; validation evidence belongs to `gfit-adlc-validate`.

## Completion
Each requirement has planned proof, and every implementation change traces to the approved Intent or design. Report outputs, evidence status and the next human or ADLC handoff.
