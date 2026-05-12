---
name: finish-issue
description: Transition a Jira issue to Done and optionally push the branch and open an MR
---

Mark a Jira issue as Done.

**Usage:** `/finish-issue <MCP_JIRA_DEFAULT_PROJECT_KEY>-851` or `/finish-issue 851`

## Steps

### 1. Parse issue ID

Take `$ARGUMENTS` as the issue ID. If it contains no hyphen (e.g., `851`), prepend `<MCP_JIRA_DEFAULT_PROJECT_KEY>-` to get `<MCP_JIRA_DEFAULT_PROJECT_KEY>-851`.

If no argument is given, infer the issue ID from the current git branch name:
```bash
git rev-parse --abbrev-ref HEAD
```
The branch is expected to follow the `<MCP_JIRA_DEFAULT_PROJECT_KEY>-NNN-*` convention. Extract `<MCP_JIRA_DEFAULT_PROJECT_KEY>-NNN` from it.

### 2. Fetch issue details

Use `mcp__jira__jira_get_issue` to confirm the issue exists and retrieve its summary and current status. Show the user:
```
Issue: <MCP_JIRA_DEFAULT_PROJECT_KEY>-NNN — <summary>
Status: <current status>
```

If the issue is already in a Done-like status (`Done`, `Fechado`, `Concluído`), inform the user and stop.

### 3. Get available transitions

Use `mcp__jira__jira_get_transitions` for the issue.

Find the transition whose name matches `Done`, `Fechado`, `Concluído`, or `Closed` (case-insensitive).

If no matching transition is found, list all available transitions and ask the user to pick one.

### 4. Update due date and transition to Done

Get today's date: `TODAY=$(date +%Y-%m-%d)`.

Use `mcp__jira__jira_update_issue` to set `duedate` to `$TODAY`.

Then use `mcp__jira__jira_transition_issue` with the matching transition ID.

Confirm success:
```
✔ <MCP_JIRA_DEFAULT_PROJECT_KEY>-NNN transitioned → Done
✔ Due Date: <TODAY>
```

### 5. Offer to push branch and open MR (optional)

Ask: "Push branch and open a Merge Request? (y/N)".

If yes, run the `/mr` skill to create the MR.
