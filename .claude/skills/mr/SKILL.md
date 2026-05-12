---
name: mr
description: Generate a GitHub PR description and create the PR directly via gh
---

Create a Pull Request for the current branch into main.

Steps:
1. Run `git log origin/main...HEAD --oneline` and `git diff origin/main...HEAD --stat` to understand what's being merged
2. Read the full diff with `git diff origin/main...HEAD` (truncate if > 15000 chars, use stat instead)
3. Generate a concise PR description (max 350 words) with this structure — skip sections with nothing relevant:

```
## Summary
One sentence stating the goal.

## Changes
- Schema changes, affected models/DAGs, data contract impact
- Pipeline & DAG impact

## Risks & Rollout
- Operational risks, rollback approach, deployment notes (only if non-trivial)
```

4. Run `git push -u origin HEAD` to push the branch
5. Run `gh pr create --title "<first line of summary>" --body "<full description>" --base main --assignee @me`
6. Show the PR URL returned by gh

If `gh` is not installed, tell the user to install it:
- Mac: `brew install gh`
- Linux: `sudo apt install gh` or see https://github.com/cli/cli/blob/trunk/docs/install_linux.md
Then authenticate with: `gh auth login`
