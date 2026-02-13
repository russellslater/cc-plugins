---
name: acli
description: Use the Atlassian CLI (acli) to interact with Jira from the command line. Covers searching, viewing, creating, editing, and transitioning Jira issues; managing sprints and boards. Use whenever the user asks about Jira issues, boards, or sprints and prefers CLI over the MCP server. Always refer to this skill doc for syntax — do not use --help.
---

# Atlassian CLI (acli)

Binary: `/opt/homebrew/bin/acli`

## Auth

Auth is interactive (requires arrow keys and user input) — **you cannot run it**. If a command returns `unauthorized` or `use 'acli jira auth login' to authenticate`, ask the user to run the following in their terminal:

```
acli jira auth login
```

## General Flags

**Output formats** — prefer `--csv` where supported. JSON bloats output ~30x with nested avatars, URLs, and metadata. Only use `--json` when you need nested data or the command doesn't support `--csv`.

| Flag | Supported on |
|------|-------------|
| `--csv` | `workitem search`, `board search`, `board list-sprints`, `board list-projects`, `sprint list-workitems`, `workitem comment list` |
| `--json` | All of the above **plus** `workitem view`, `workitem create`, `board get`, `sprint view`, `filter get` |

Other common flags:
- `--limit N` — max results (default varies, typically 50)
- `--paginate` — fetch all pages
- `--yes` / `-y` — skip confirmation prompts

## Jira

Full flag reference: [references/jira.md](references/jira.md)

### Quick Reference

**Search issues:**
```bash
acli jira workitem search --jql "project = ZR05 AND status != Done" --fields "key,summary,status,assignee,priority" --csv
```

**View an issue** (no --csv support):
```bash
acli jira workitem view ZR05-123 --json
```

**Create an issue:**
```bash
acli jira workitem create --project ZR05 --type Task --summary "Title" --assignee "user@lego.com"
```

**Edit an issue:**
```bash
acli jira workitem edit --key ZR05-123 --summary "New title" --yes
```

**Transition status:**
```bash
acli jira workitem transition --key ZR05-123 --status "In Progress" --yes
```

**Assign:**
```bash
acli jira workitem assign --key ZR05-123 --assignee "@me" --yes
```

**Add a comment:**
```bash
acli jira workitem comment create --key ZR05-123 --body "Comment text"
```

**Find a board:**
```bash
acli jira board search --project ZR05 --csv
```

**List sprints on a board:**
```bash
acli jira board list-sprints --id 3707 --state active --csv
```

**List items in a sprint:**
```bash
acli jira sprint list-workitems --board 3707 --sprint 42 --csv
```

## Confluence

Not available via acli — auth does not work. If available, suggest using MCP Atlassian tools for Confluence.

## Tips

- Use `--fields` on search/view to control output size — fewer fields = faster + less noise.
- `--count` on search gives just the count without fetching results.
- `--web` / `-w` opens the result in the browser.
- Assignee shortcuts: `@me` (self-assign), `default` (project default).
- Bulk operations: `--jql` and `--filter` flags work on edit, assign, transition, and comment — apply to many issues at once with `--yes`.
