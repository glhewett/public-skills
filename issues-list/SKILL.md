# issues-list

List all open issues in a concise table format.

## Arguments

None required. Optional filter arguments may be added later.

## Steps

1. Use the Glob tool to find all `.issues/*.toml` files.
2. If no issues are found, inform the user that there are no open issues.
3. Read each issue file using the Read tool.
4. Parse the TOML fields from each file (id, title, status, priority, assigned_to, closed).
5. Filter out any issues where `closed = true`. Only show open (non-closed) issues.
6. If no open issues remain after filtering, inform the user that there are no open issues.
7. Display the issues in a markdown table with the following columns:

```
| ID   | Status | Priority | Assignee | Title |
|------|--------|----------|----------|-------|
| 0001 | open   | medium   |          | Fix login bug |
| 0002 | open   | high     | dev@co   | Add dark mode |
```

Sort the issues by ID in ascending order.

## Allowed tools

- `Bash(git *)` - for git commands
- `Read` - for reading issue files
- `Glob` - for finding issue files
