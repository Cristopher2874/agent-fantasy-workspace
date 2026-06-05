# Agent Container Workspace

This folder documents the files available inside the container where the agent runs. The container includes the main workspace data plus any team-provided skills the agent should inspect and follow before preparing a submission.

## Purpose

The workspace is organized around a matchday task. It contains:

- Game-board data used to understand the current matchday, teams, players, standings, matches, and valid claims.
- Rule documents for the supported play modes.
- Output-format requirements for the final JSON response.
- Optional team package material, including participant skills that should be read and executed first.

## Agent Workflow

1. Read the team package first, when present.
2. Inspect every relevant `SKILL.md` under `/workspace/team/**/`.
3. Load the game-board data needed for the task.
4. Apply the appropriate rules from `/workspace/rules/`.
5. Validate the final answer against `/workspace/output-format/daily-submission.schema.json`.
6. Use `/workspace/output-format/examples/daily-submission.json` as a shape reference, not as a source of truth over the schema.

## File Reference

| File | Description |
| --- | --- |
| `/workspace/game-board/matchday.json` | Describes the matchday ID and the locked time zones. |
| `/workspace/game-board/matches.json` | Current matches for the day, including general match data and match IDs. |
| `/workspace/game-board/players.json` | Official player pool. Fantasy XI submissions must use these `player_id` values. |
| `/workspace/game-board/teams.json` | Team IDs and metadata used by matches and players. |
| `/workspace/game-board/standings-before.json` | Team standings and points before this matchday. |
| `/workspace/game-board/claim-catalog.json` | Valid Risk Play claims and the fields required for each claim. |
| `/workspace/rules/fantasy-xi.md` | Fantasy XI rules. |
| `/workspace/rules/risk-play.md` | Risk Play rules. |
| `/workspace/rules/bracket-play.md` | Bracket Play rules, when bracket play is open. |
| `/workspace/output-format/daily-submission.schema.json` | Required final JSON schema. |
| `/workspace/output-format/examples/daily-submission.json` | Example final answer shape. |
| `/workspace/team/README.md` | Team package overview, when present. |
| `/workspace/team/**/SKILL.md` | Participant skills. Read and execute these first. |

## Important Notes

- Treat IDs from the JSON data as authoritative.
- For Fantasy XI, only use player IDs from `/workspace/game-board/players.json`.
- For Risk Play, only use claims defined in `/workspace/game-board/claim-catalog.json`, including all required fields.
- For Bracket Play, consult `/workspace/rules/bracket-play.md` only when bracket play is open.
- The final submission must match `/workspace/output-format/daily-submission.schema.json`.

