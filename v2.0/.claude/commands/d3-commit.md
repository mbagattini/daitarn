# /d3-commit

Explicit commit for assistant work. Same logic used internally by /d3-4-build at phase end.

## Behavior

1. Inspect the working tree for staged and unstaged changes.
2. If nothing to commit, tell the pilot and stop.
3. Stage all changes the assistant has made (and only those — do not include unrelated pilot-only edits unless the pilot explicitly says so).
4. Compose a commit message in the language declared in Commits in CLAUDE.md, prefixed [claude]. Keep it concise and descriptive.
5. Show the pilot the proposed message and the list of files. Ask for confirmation before committing.
6. On confirmation, commit.

## Notes

- All commits via Daitarn slash commands carry the [claude] prefix. Pilot-only commits outside the flow are made directly with git, without prefix.
- /d3-4-build invokes this same logic automatically at the end of build phase, with no separate confirmation (the pilot already authorized by running the phase).
- Respect Commits and Interactions languages in CLAUDE.md.
