# GFIT ADLC — Agent instructions

## Purpose

Use these instructions with the six technology-neutral ADLC skills under `.agents/skills/gfit-adlc-*/`. The current project's instructions and artifacts provide its bindings: domain rules, paths, tools, commands, policies, metrics, decision owners and deployment targets.

Read the relevant project binding before acting. Explicit user instructions take precedence when they deliberately change that binding; state which assumptions or expected outcomes then change.

## Skill routing

Read the full relevant `SKILL.md` and only the supporting resources needed for the current task.

| ADLC mode | Skill |
|---|---|
| Intent | `.agents/skills/gfit-adlc-intent/SKILL.md` |
| Generate | `.agents/skills/gfit-adlc-generate/SKILL.md` |
| Validate | `.agents/skills/gfit-adlc-validate/SKILL.md` |
| Govern | `.agents/skills/gfit-adlc-govern/SKILL.md` |
| Deploy | `.agents/skills/gfit-adlc-deploy/SKILL.md` |
| Observe | `.agents/skills/gfit-adlc-observe/SKILL.md` |

The six modes can overlap. Generate and Validate are separate responsibilities in one feedback loop: Validate defines and checks evidence before and during generation, then returns gaps to Generate. Observe hands outcome evidence to Govern and may supply evidence for a later Intent.

Each skill must remain useful when copied alone into another project. Keep domain, technology, fixed paths and environment assumptions in the project binding rather than the Skill Core.

## Scope and authority

Work only within the scope currently authorized. A request to perform work does not count as approval of its result or authorization to release it. Stop at a required human checkpoint and record a decision only from the accountable human's actual response.

Preserve existing artifacts and evidence when resuming. Do not overwrite prior outcomes or execute later work merely because its inputs appear predictable.

## Missing project bindings

Search project instructions and existing artifacts before asking for information. Complete work that does not depend on a missing binding. Do not invent validation commands, deployment targets, signals, guardrails, evidence or human decisions. Mark unavailable execution as `NOT RUN` and unavailable outcome evidence as `INSUFFICIENT EVIDENCE`, then identify the exact missing input.

## Evidence and handoff

Keep proposed, approved, executed and observed states distinct. Tie validation and release evidence to a revision or reproducible snapshot. Preserve earlier evidence, including failures. Agent recommendations never substitute for human decisions.

Report the active ADLC mode, files changed, actual evidence, unresolved bindings and next handoff. Never fabricate a passing check, approval, release or observation.
