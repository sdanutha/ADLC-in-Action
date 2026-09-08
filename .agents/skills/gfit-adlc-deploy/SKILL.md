---
name: gfit-adlc-deploy
description: Use when a validated revision has human approval and is ready for a controlled, recoverable release to a defined target.
metadata:
  author: "GFIT ADLC"
  version: "1.0.0"
---

# Deploy

Move an approved revision into its defined target with verifiable health and recovery steps. Read project instructions, the decision record and current validation evidence. The project binding supplies the target, commands, access policy and observability. Use [the release template](assets/release-template.md) when no project format exists.

1. Verify that the decision records human approval and matches the current revision, target and rollout scope. A material difference returns to Govern.
2. Establish a recoverable snapshot or version. Record deployment, stop and rollback instructions before changing the target. Preserve unrelated state.
3. Execute only the approved project-defined deployment commands. Record revision, target, timestamp and actual command results. If execution is unavailable, provide the commands and record status as `not-executed`.
4. Run the project-defined health and smoke checks. Verify release identity and evidence labels before outcome observation. Keep test, synthetic and real observations distinguishable.
5. If a conflict or failure occurs, identify ownership before changing shared resources. Apply the documented recovery plan when its trigger is met, and record the actual result.

## Completion

The release record uses `planned`, `not-executed`, `executed`, `verified`, `failed` or `rolled-back`, and states the approved revision and scope, actual checks, recovery path and current target state. A verified release establishes technical reachability or health; product outcome remains for Observe.
