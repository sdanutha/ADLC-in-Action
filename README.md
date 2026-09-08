# GFIT ADLC Skill Core

The `main` branch contains general rules for coding agents and reusable ADLC Skills. The Skills do not require one language, framework, file path, test command, or release target.

```text
Intent → Generate ↔ Validate → Govern → Deploy → Observe
  ↑                                                   |
  └──────────────────── outcome signal ───────────────┘
```

## Files in This Branch

```text
AGENTS.md                         General rules and Skill routing
.agents/skills/gfit-adlc-*/      Six ADLC Skill modes
README.md                         Guide for the Core branch
```

| Mode | Skill | Main job |
|---|---|---|
| Intent | `gfit-adlc-intent` | Turn a wanted outcome into a hypothesis and clear measures |
| Generate | `gfit-adlc-generate` | Create or update specs, plans, code, and other artifacts |
| Validate | `gfit-adlc-validate` | Define proof, check the work, and return feedback |
| Govern | `gfit-adlc-govern` | Prepare evidence for a human decision |
| Deploy | `gfit-adlc-deploy` | Release an approved revision to a target with a recovery plan |
| Observe | `gfit-adlc-observe` | Study outcome signals and guardrails from evidence |

Generate and Validate have different jobs, but they work in one feedback loop. A human confirms the Intent, approves the scope, decides on a release, and resolves the result.

## Use the Core in a Project

1. Copy `AGENTS.md` and `.agents/` to the project root.
2. Add a Project Binding. It must define the domain rules, paths, tools, commands, policies, measures, decision owners, and release targets.
3. Ask the coding agent to read `AGENTS.md`, the Project Binding, and the `SKILL.md` for the current mode.
4. Keep proposed, approved, executed, and observed states separate. Record only real evidence.

If the Project Binding is missing a detail, the agent must first do the work that does not need that detail. The agent must not guess a validation command, target, signal, approval, or result.

## Branches

| Branch | Purpose | Extra content |
|---|---|---|
| `main` | Add the ADLC Skill Core to a project | `AGENTS.md` and `.agents/skills/` |
| `handson` | Learn ADLC by building and changing a game | A step-by-step guide and a Game Project Binding |
| `docs` | Present ADLC in Action | A PowerPoint deck and an HTML visual guide |

Clone the `handson` branch for the workshop:

```bash
git clone --branch handson <repository-url>
```

Clone the `docs` branch for the presentation files:

```bash
git clone --branch docs <repository-url>
```

## Maintain the Skill Core

Update `AGENTS.md` or `.agents/skills/` on `main` first. Then copy these two paths to `handson` and commit the copy on that branch. The `docs` branch does not contain agent rules or Skills. Each branch keeps its own content. Do not merge the branches into each other.
