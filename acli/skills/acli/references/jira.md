# acli Jira — Full Flag Reference

## workitem search

Search issues with JQL.

```
acli jira workitem search --jql "..." [flags]
```

| Flag | Short | Description |
|------|-------|-------------|
| `--jql` | `-j` | JQL query |
| `--filter` | | Filter ID |
| `--fields` | `-f` | Comma-separated field list (default: `issuetype,key,assignee,priority,status,summary`) |
| `--json` | | JSON output |
| `--csv` | | CSV output |
| `--count` | | Return count only |
| `--limit` | `-l` | Max results |
| `--paginate` | | Fetch all pages |
| `--web` | `-w` | Open in browser |

## workitem view

View issue details.

```
acli jira workitem view KEY-123 [flags]
```

| Flag | Short | Description |
|------|-------|-------------|
| `--fields` | `-f` | Field list (default: `key,issuetype,summary,status,assignee,description`). Special: `*all`, `*navigable`. Prefix `-` to exclude. |
| `--json` | | JSON output |
| `--web` | `-w` | Open in browser |

## workitem create

Create an issue.

```
acli jira workitem create --project KEY --type Type --summary "..." [flags]
```

| Flag | Short | Description |
|------|-------|-------------|
| `--project` | `-p` | Project key (required) |
| `--type` | `-t` | Issue type: Epic, Story, Task, Bug (required) |
| `--summary` | `-s` | Summary (required unless `--from-file`/`--from-json`) |
| `--description` | `-d` | Description (plain text or ADF) |
| `--description-file` | | Read description from file |
| `--assignee` | `-a` | Email, account ID, `@me`, or `default` |
| `--label` | `-l` | Comma-separated labels |
| `--parent` | | Parent work item ID (for subtasks) |
| `--from-file` | `-f` | Read summary+description from file |
| `--from-json` | | Read from JSON file |
| `--generate-json` | | Print example JSON structure |
| `--editor` | `-e` | Open text editor |
| `--json` | | JSON output |

## workitem create-bulk

Bulk create issues from file.

```
acli jira workitem create-bulk --from-json issues.json [flags]
```

| Flag | Description |
|------|-------------|
| `--from-json` | JSON file with array of issue objects |
| `--from-csv` | CSV file (columns: summary, projectKey, issueType, description, label, parentIssueId, assignee) |
| `--generate-json` | Print example JSON structure |
| `--ignore-errors` | Skip failures |
| `--yes` | No prompt |

## workitem edit

Edit issues.

```
acli jira workitem edit --key "KEY-1" --summary "..." [flags]
```

| Flag | Short | Description |
|------|-------|-------------|
| `--key` | `-k` | Comma-separated issue keys |
| `--jql` | | JQL to select issues |
| `--filter` | | Filter ID to select issues |
| `--summary` | `-s` | New summary |
| `--description` | `-d` | New description |
| `--description-file` | | Read description from file |
| `--assignee` | `-a` | New assignee |
| `--remove-assignee` | | Unassign |
| `--type` | `-t` | Change issue type |
| `--labels` | `-l` | Set labels |
| `--remove-labels` | | Remove labels |
| `--from-json` | | Read from JSON |
| `--ignore-errors` | | Skip failures |
| `--yes` | `-y` | No prompt |
| `--json` | | JSON output |

## workitem transition

Change issue status.

```
acli jira workitem transition --key "KEY-1" --status "Done" [flags]
```

| Flag | Short | Description |
|------|-------|-------------|
| `--key` | `-k` | Comma-separated issue keys |
| `--jql` | | JQL to select issues |
| `--filter` | | Filter ID |
| `--status` | `-s` | Target status name |
| `--ignore-errors` | | Skip failures |
| `--yes` | `-y` | No prompt |
| `--json` | | JSON output |

## workitem assign

Assign issues.

```
acli jira workitem assign --key "KEY-1" --assignee "@me" [flags]
```

| Flag | Short | Description |
|------|-------|-------------|
| `--key` | `-k` | Comma-separated issue keys |
| `--jql` | | JQL to select issues |
| `--filter` | | Filter ID |
| `--from-file` | `-f` | Read issue keys from file |
| `--assignee` | `-a` | Email, account ID, `@me`, `default` |
| `--remove-assignee` | | Unassign |
| `--ignore-errors` | | Skip failures |
| `--yes` | `-y` | No prompt |
| `--json` | | JSON output |

## workitem comment create

Add a comment.

```
acli jira workitem comment create --key "KEY-1" --body "..." [flags]
```

| Flag | Short | Description |
|------|-------|-------------|
| `--key` | `-k` | Issue keys |
| `--jql` | | JQL to select issues |
| `--filter` | | Filter ID |
| `--body` | `-b` | Comment text (plain or ADF) |
| `--body-file` | `-F` | Read body from file |
| `--editor` | | Open text editor |
| `--edit-last` | `-e` | Edit last comment from same author |
| `--ignore-errors` | | Skip failures |
| `--json` | | JSON output |

## workitem comment list

List comments on an issue.

```
acli jira workitem comment list --key KEY-123 [flags]
```

| Flag | Description |
|------|-------------|
| `--key` | Issue key |
| `--json` | JSON output |
| `--limit` | Max comments (default 50) |
| `--order` | Sort: `+created`, `+updated` (default `+created`) |
| `--paginate` | Fetch all |

## workitem link create

Link two issues.

```
acli jira workitem link create --out KEY-1 --in KEY-2 --type Blocks
```

| Flag | Description |
|------|-------------|
| `--out` | Outward issue key |
| `--in` | Inward issue key |
| `--type` | Link type (outward description) |
| `--from-json` / `--from-csv` | Bulk from file |
| `--yes` | No prompt |

## workitem link list / type

```
acli jira workitem link list --key KEY-123 [--json]
acli jira workitem link type [--json]
```

## workitem attachment list / delete

```
acli jira workitem attachment list --key KEY-123 [--json]
acli jira workitem attachment delete --id ATTACHMENT_ID [--yes]
```

## board search

Find boards.

```
acli jira board search [flags]
```

| Flag | Description |
|------|-------------|
| `--project` | Filter by project key |
| `--name` | Filter by name (partial match) |
| `--type` | `scrum`, `kanban`, `simple` |
| `--json` / `--csv` | Output format |
| `--limit` | Max results (default 50) |
| `--paginate` | Fetch all |

## board get / list-projects / list-sprints

```
acli jira board get --id 123 [--json]
acli jira board list-projects --id 123 [--json] [--csv] [--limit N] [--paginate]
acli jira board list-sprints --id 123 [--state active,closed] [--json] [--csv] [--limit N] [--paginate]
```

## sprint view / list-workitems

```
acli jira sprint view --id 42 [--json]
acli jira sprint list-workitems --board 3707 --sprint 42 [--jql "..."] [--fields "..."] [--json] [--csv] [--limit N] [--paginate]
```

## project list / view

```
acli jira project list [--json] [--limit N] [--paginate] [--recent]
acli jira project view --key ZR05 [--json]
```

## filter get / list / search

```
acli jira filter get --id 10001 [--json]
acli jira filter list [--favourite] [--json]
acli jira filter search [--name "..."] [--json]
```
