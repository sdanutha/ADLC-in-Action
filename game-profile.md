# Game Example Scenario — Project Binding

This file adds game rules to the reusable `gfit-adlc-*` Skills. Use these rules only for this Hands-on workshop. They are not part of the ADLC Skill Core.

## How to Use This Binding

- Read this file before every Step in `README.md`. It defines the stack, paths, acceptance cases, measures, and local release for the game.
- Do only the Step selected by the learner. Stop at its checkpoint. Do not work on two Intents in one turn.
- Keep artifacts and evidence from earlier Intents, including failed results. Do not replace them to make the work look successful.
- Intent confirmation and Spec or Plan approval are small Govern checkpoints. Use the full `gfit-adlc-govern` workflow before Deploy and after Observe.
- A request to start a Step allows only the normal work for that Step. It does not approve an artifact, revision, or release.
- Record a human decision only from the learner's real answer. The agent may give advice, but it must not decide for the human.

## Creation and Execution Rules

- Create application files only during implementation Steps. Stop before code while you create the Spec and Plan.
- Use the Python 3 version on the computer. Create `pyproject.toml` and `uv.lock`. Do not create `.python-version` to lock a minor version. Keep the same dependency lock in later Steps unless you record a reason to change it.
- Keep game logic separate from HTTP rendering so tests can call it. Use controlled random values in tests.
- Use a random opaque session cookie and server-side runtime state. Do not show the secret number in HTML, cookies, telemetry, or a production test endpoint.
- Create and record a `source=test` setting for validation and smoke tests. Use `source=real` for observation without hints. The default is test, and telemetry must stay on the local computer.
- Keep existing event labels. Start a new session when the source or version changes.
- Map automated and manual evidence to the acceptance IDs in this file. Change a test only when a recorded requirement supports the change. Do not skip or weaken a check to get a passing result.
- Generated tests are not independent proof by themselves. Record each real command, result, and related manual check.

## Step Report

End each Step with:

- The current Step and Skills
- Files created or changed
- Real commands and results, or `NOT RUN`
- What the learner must check or decide
- The next Step that is ready

Always keep technical validation separate from outcome observation.

## Environment and Outputs

- Python 3 or later with no fixed minor version, FastAPI, Jinja2, HTML/CSS, pytest, and uv
- Entry point: `app.main:app`
- Test command: `uv run pytest -q`
- Local release: `uv run uvicorn app.main:app --host 127.0.0.1 --port 8000`
- Intent artifacts: `artifacts/intent-001/` and `artifacts/intent-002/`
- Runtime telemetry: `telemetry/events.jsonl`
- Bind only to loopback. Do not use Node, custom JavaScript, a database, an LLM API, a paid service, public hosting, remote deployment, remote push, or global configuration changes.

## Game Contract

- The home page has a short guide and a `Start game` button. All user text is in English.
- Pick a random whole number from 1 to 100. The player gets seven guesses. A repeated valid number uses another guess.
- Show `Too low` for a guess below the secret number. Show `Too high` for a guess above it. Show a win when the guess is correct.
- A correct seventh guess is a win. An incorrect seventh guess is a loss. Show the secret number only after the round ends.
- Reject empty input, non-whole numbers, and numbers outside the range. Invalid input does not use a guess.
- Do not accept another guess after the round ends. Do not change the result or record `round_completed` twice.
- In v1, the end page has no `Play again` button. The player may return to the home page and start a new round. This is the baseline with extra effort.
- In v2, add a `Play again` button after a win or loss. It starts a new round with seven guesses and a new random number. Do not show the button during a round.
- A refresh or redirect must not use a guess or start a round. Use POST and then redirect to GET.
- Do not put the secret number in HTML, cookies, or telemetry during play. Different sessions must not share state.
- Do not add scores, difficulty levels, a leaderboard, sound, login, or a database to the main path.

## Acceptance Cases

| ID | Proof needed |
|---|---|
| G01 | A new round has `playing` status and seven guesses. |
| G02 | `Too low` and `Too high` are correct. One valid guess uses one attempt. |
| G03 | A correct guess wins, including a correct seventh guess. |
| G04 | Seven incorrect guesses lose the round. |
| G05 | Invalid input is rejected. It does not change attempts or guess events. |
| G06 | A finished round accepts no more guesses and has only one `round_completed` event. |
| G07 | Two sessions are separate, and the secret number does not leak before the end. |
| G08 | The web start, guess, and end flows work. A refresh does not repeat an action. |
| G09 | The event schema is correct, uses UTC time, and separates version and source. |
| G10 | The v1 end page has no replay button. The same session can return home and start a new round. |
| R01 | After a v2 win or loss, replay resets attempts, status, and round_id. |
| R02 | Replay keeps session_id, raises round_index, and a refresh does not add a round. |
| R03 | v2 has no replay during a round. G01–G09 still pass. Only the changed part of G10 is updated. |

Tests control the secret number with injected randomness or a fixture. Do not add a secret test endpoint to the real application. A PASS result must come from a real test run.

## Telemetry Contract

Each JSONL event has `event_id`, a UTC ISO 8601 `timestamp`, an opaque `session_id`, `round_id`, `round_index`, `version` (`v1` or `v2`), `source` (`real` or `test`), and `event` (`round_started`, `guess_submitted`, or `round_completed`).

- `guess_submitted` has `attempt` from 1 to 7 and `result` (`low`, `high`, or `correct`).
- `round_completed` has `outcome` (`won` or `lost`) and `attempts_used`.
- For the last guess, record `guess_submitted` before `round_completed`.
- Do not store the secret number or unneeded raw input.
- One browser session in one version keeps the same session_id after a return home or replay.
- Start a new session after a version change or a restart that clears state. Do not combine data from different periods without a clear label.

## Intent Measures

**Intent 1:** A new player can start and finish the first round without help.

- Pilot target: At least 4 of 5 eligible sessions finish the first round within five minutes.
- Guardrails: No observed blocking error, and no secret number shown before the end.

**Intent 2:** Reduce the effort needed for a player to choose a second round.

- Intervention: Add a `Play again` button after the round ends.
- Target: The replay rate rises by at least 15 percentage points from v1.
- Guardrails: The completion rate falls by no more than 5 percentage points, and there is no observed blocking error.

**Completion rate:** Sessions that finish the first round within five minutes ÷ sessions that start the first round and have a full five-minute follow-up window.

**Replay rate:** Sessions that start a second round within five minutes after the first round ends ÷ sessions that finish the first round and have a full five-minute follow-up window.

Count sessions, not events or rounds. Report N/A when the denominator is zero. Keep test data separate from real data. Several self-test sessions from one person are not several independent players. Replay is a proxy. It does not prove that a player had fun. Report `INSUFFICIENT EVIDENCE` when the sample or follow-up window is too small. Do not create data to fill a gap.
