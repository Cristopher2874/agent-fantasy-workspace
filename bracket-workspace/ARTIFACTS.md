# Bracket Play Runtime Contract

This folder shows the participant-visible workspace and prompt contract for a one-time bracket-only run.

## Mounted Workspace Files

- `workspace/game-board/matchday.json`: submission timing and tournament-day metadata.
- `workspace/game-board/bracket.json`: official knockout board with required `match_id` values and allowed winners.
- `workspace/game-board/matches.json`: knockout matchup context, placeholder seeds, and later-round source edges.
- `workspace/game-board/teams.json`: team ids, names, and current qualification context.
- `workspace/game-board/standings-before.json`: standard fantasy-team leaderboard context kept for workspace compatibility.
- `workspace/game-board/world-cup-standings.json`: World Cup group standings plus the current best-third-place ranking.
- `workspace/game-board/bracket-context.json`: provenance plus provisional-slot details when the official knockout field is not fully locked yet.
- `workspace/rules/bracket-play.md`: bracket-specific rules.
- `workspace/output-format/bracket-submission.schema.json`: required final JSON schema.
- `workspace/output-format/examples/bracket-submission.json`: example final answer shape.
- `workspace/team/README.md` and bracket-relevant `workspace/team/**/SKILL.md`: the participant package the model must read first.

## Prompt-Only Instructions

- The prompt injects the participant `team_id` and tells the model to use it in the final JSON.
- The prompt explicitly says this is a bracket-only run and forbids Fantasy XI or Risk Play fields.
- The prompt tells the model to fail setup if it cannot find a usable team `SKILL.md`.
- The prompt states that network access may be available, but only when the participant skill asks for it.
- The prompt tells the model to ignore Fantasy XI or Risk Play skills even if they are present in the uploaded package.
- The prompt tells the model to use `candidate_team_ids`, `world-cup-standings.json`, and bracket context when a Round of 32 slot is still provisional.

## Compatibility Notes

- `workspace/current-standings/leaderboard.json` and `leaderboard.md` mirror `standings-before.json` in the familiar fantasy-team leaderboard shape.
- Uploaded participant packages may still contain daily-only skills. Bracket-only agents should ignore those and follow only bracket-relevant instructions.

## Output Contract

- Return one JSON object that matches `workspace/output-format/bracket-submission.schema.json`.
- Use one pick for every required knockout match in `bracket.json`.
- Use only official `winner_team_id` values allowed by the bracket board.
- Set `champion_team_id` to the same winner submitted for the final match.
- The organizer stores the accepted bracket submission later at `gameplay-submissions/teams/sample-team-001/brackets/knockout-2026.json` and the scoring workflow reads that same file without rewriting it.
