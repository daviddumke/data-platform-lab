---
name: start-issue
description: Assign a Jira issue to yourself, set today's dates, transition to In Progress, and create+checkout the branch
---

Start work on a Jira issue: assign it to the current user, set Start date and Due date to today, transition the issue to In Progress, create a branch following the project naming convention, and switch to it.

**Usage:** `/start-issue <MCP_JIRA_DEFAULT_PROJECT_KEY>-851` or `/start-issue 851`

## Steps

### 1. Parse issue ID

Take `$ARGUMENTS` as the issue ID. If it contains no hyphen (e.g., `851`), prepend `<MCP_JIRA_DEFAULT_PROJECT_KEY>-` to get `<MCP_JIRA_DEFAULT_PROJECT_KEY>-851`.

### 2. Fetch issue details via MCP

Use the `mcp__jira__jira_get_issue` tool with the issue ID to retrieve the issue summary. Stop and report an error if the issue is not found.

### 3. Get current user and assign

Use `mcp__jira__jira_get_myself` to get the current user's accountId.

Use `mcp__jira__jira_assign_issue` to assign the issue to yourself.

### 4. Set Start Date and Due Date

Get today's date: `TODAY=$(date +%Y-%m-%d)`.

Use `mcp__jira__jira_update_issue` to set:
- `duedate`: `$TODAY`
- `customfield_10308` (Start date): `$TODAY`

### 5. Transition issue to In Progress

Use `mcp__jira__jira_get_transitions` to list transitions for the issue.

Find the transition whose name contains `Progress`, `Andamento`, or `Em progresso` (case-insensitive).

Use `mcp__jira__jira_transition_issue` with the matching transition ID.

If no matching transition is found, warn the user but continue.

### 6. Generate branch name

Slugify the issue summary directly (no shell command needed):

- Lowercase the summary.
- **Transliterate diacritics to ASCII** (e.g., `ç` → `c`, `ã` → `a`,
  `é` → `e`, `ó` → `o`, `õ` → `o`) so Portuguese text produces clean
  slugs. Without this step, regex strip leaves awkward gaps like
  `configura-es` instead of `configuracoes`.
- Replace any sequence of non-alphanumeric ASCII characters with a
  single `-`.
- Strip leading and trailing `-`.
- If longer than 50 characters, truncate at the last `-` before the
  50-char mark.

Combine: `BRANCH_NAME="$ISSUE_ID-$SLUG"`. Examples:

- `Criar documentos essenciais` →
  `<MCP_JIRA_DEFAULT_PROJECT_KEY>-851-criar-documentos-essenciais`
- `Ajustar configurações e skill` →
  `<MCP_JIRA_DEFAULT_PROJECT_KEY>-978-ajustar-configuracoes-e-skill`

### 7. Create and checkout the branch from remote `main-oci`

New branches must start from the latest **remote** `main-oci`, never from
the current HEAD or a stale local copy.

**7a — Verify the working tree is clean:**

```bash
git status --porcelain
```

If the output is non-empty, stop and ask the user how to proceed (commit,
stash, or discard) before continuing. `git checkout -b` silently carries
uncommitted changes into the new branch, which mixes unrelated work.

**7b — Fetch the latest remote state:**

```bash
git fetch origin main-oci
```

**7c — Check if the branch already exists locally:**

```bash
git branch --list "$BRANCH_NAME"
```

- If it **doesn't exist**:
  ```bash
  git checkout -b "$BRANCH_NAME" --no-track origin/main-oci
  ```
  Branches from the freshly fetched remote, ignoring HEAD. The
  `--no-track` flag prevents the new branch from inheriting
  `origin/main-oci` as its upstream — `/mr` will set the correct
  upstream (`origin/$BRANCH_NAME`) on first push.

- If it **already exists**:
  ```bash
  git checkout "$BRANCH_NAME"
  ```
  Inform the user. Do NOT reset or rebase it onto the new `origin/main-oci`
  automatically — the branch may have ongoing work.

**Why explicit `origin/main-oci`:** without the source ref and the preceding
`git fetch`, `git checkout -b` defaults to `HEAD`. Each new ticket would
inherit whatever was previously checked out (often an unrelated feature
branch or a stale local `main-oci`).

### 8. Confirm

Print a summary:
```
✔ Issue:      <MCP_JIRA_DEFAULT_PROJECT_KEY>-851 — <summary>
✔ Assigned:   <username>
✔ Start Date: <TODAY>
✔ Due Date:   <TODAY>
✔ Status:     → In Progress
✔ Branch:     <BRANCH_NAME> (created and checked out)
```
