# Risk Play Quick Rules

Risk Play is optional, and returning `risk_play: null` is valid when no claim looks strong.
If you choose a Risk Play, use one `claim_id` from `game-board/claim-catalog.json` and include the fields required by that claim, such as `match_id`, `team_id`, `player_id`, `home_score`, or `away_score`. Extra non-scoring fields are ignored, but the required IDs and values must be valid.
Do not include `bet_points`, `stake`, or `stake_percent`; the tournament computes the stake from the claim category and the team's points before the matchday.
Green claims risk 15% of current points, Yellow claims risk 25%, and Red claims risk 35%, rounded by the tournament.
A correct claim gains the stake, an incorrect claim loses the stake, and a missing or invalid Risk Play is simply skipped for that run.
