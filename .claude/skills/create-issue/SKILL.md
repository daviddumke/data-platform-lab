---
name: create-issue
description: Create a new Jira issue, prompting for project, summary, type, parent (optional), and labels/tags
---

Interactively create a new Jira issue via MCP.

**Usage:** `/create-issue` or `/create-issue "Fix extraction bug in dbt"`

## Steps

### 1. Gather required information

**Ask the user one question per message — wait for their reply before asking the next.** Never bundle multiple questions in a single message. If the user pre-answers several at once (e.g. `"summary text" project=DA type=Bug parent=DA-315`), accept the answers and skip the questions already covered.

Collect each field below, **one at a time, in this order**, asking only for fields not already provided:

1. **Summary** — if `$ARGUMENTS` is non-empty, use it as the summary and skip this question. Otherwise ask: "What's the issue about?".
2. **Project** — list available projects using `mcp__jira__jira_get_projects` (or reuse cached results from earlier in the session). Default: `MCP_JIRA_DEFAULT_PROJECT_KEY` when the user presses enter without an answer.
3. **Issue type** — use `mcp__jira__jira_get_issue_types` for the chosen project. Common types: `Task` (default), `Story`, `Bug`, `Epic`.
4. **Parent issue** (optional) — leave blank if none. If a bare number is given, prepend the project key (`123` → `DA-123`).
5. **Labels/tags** (optional) — comma-separated; leave blank for none. Split on comma and trim whitespace.
6. **Description** (optional) — leave blank to skip.

### 2. Get current user

Use `mcp__jira__jira_get_user_profile` with the current user's email (from `MCP_JIRA_USERNAME`) to retrieve their account identifier.

### 3. Create the issue

Call `mcp__jira__jira_create_issue` with:
```json
{
  "project_key": "<PROJECT>",
  "summary": "<SUMMARY>",
  "issue_type": "<TYPE>",
  "assignee": "<current user email>",
  "description": "<DESCRIPTION if provided>",
  "labels": ["<label1>", "<label2>"],
  "parent": "<PARENT_ISSUE_ID if provided>"
}
```

Omit optional fields (`description`, `labels`, `parent`) if the user left them blank.

### 4. Confirm

Print:
```
✔ Created:  <PROJECT-NNN> — <summary>
  Type:     <issue type>
  Assignee: <current user display name>
  Parent:   <parent issue ID> (if set)
  Labels:   <label1>, <label2> (if set)
  URL:      <MCP_JIRA_URL>/browse/<PROJECT-NNN>
```

Ask the user: "Start working on this issue now? (y/N)". If yes, run the `/start-issue <PROJECT-NNN>` skill.
