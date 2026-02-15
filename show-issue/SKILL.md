# show-issue

Show the full details of a specific issue.

## Arguments

The argument is the issue ID, e.g. `0001` or `1`. If the ID is not zero-padded, pad it to 4 digits (e.g. `1` becomes `0001`).

## Steps

1. Parse the argument as an issue ID. Zero-pad it to 4 digits.
2. Use the Glob tool to verify `.issues/{id}.toml` exists.
3. If the file does not exist, inform the user and stop.
4. Read the issue file using the Read tool.
5. Display all fields in a nicely formatted output:

```
Issue {id}: {title}
─────────────────────────
Status:      {status}
Priority:    {priority}
Assigned to: {assigned_to}
Labels:      {labels}
Created:     {created_at}

{description}
```

If description is empty, omit the description section. If labels is empty, show "none". If assigned_to is empty, show "unassigned".

## Allowed tools

- `Read` - for reading the issue file
- `Glob` - for verifying the issue file exists
