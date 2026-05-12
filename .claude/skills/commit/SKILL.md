---
name: commit
description: Stage files and commit with an AI-generated structured message
---

Stage and commit changes using the project's structured commit format.

Steps:
1. Run `git status --short` to show current state
2. If $ARGUMENTS is non-empty, run `git add $ARGUMENTS` to stage the specified files
3. If nothing is staged, tell the user and stop
4. Run `git diff --staged` to read the diff (truncate display if large, but read it fully)
5. Generate a commit message with this exact structure:

```
<type>: <summary>

Context: <why this change was needed>
Change: <what was changed>
Data Impact: <effect on data models, pipelines, or BigQuery tables — "none" if N/A>
Risk & Rollback: <operational risk and how to revert>
Deployment: <any deploy steps needed — "none" if N/A>
```

Types: feat, fix, refactor, chore, docs, test, ci

If multiple unrelated changes are staged, warn the user and suggest how to split them before committing.

6. Show the generated commit message to the user and ask: "Commit with this message? (Y/n/edit)"
   - **Y / Enter**: run `git commit -m "<message>"` directly.
   - **n**: abort and tell the user nothing was committed.
   - **edit**: abort, tell the user nothing was committed, and instruct them to run `git commit` in a real terminal outside the Claude CLI — the `prepare-commit-msg` hook will open their editor with an AI-generated message they can edit before committing.

7. Show `git log -1 --format="%h %s%n%n%b"`