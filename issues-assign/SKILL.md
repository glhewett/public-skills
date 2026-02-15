# issues-assign

Assign an issue to the current git user.

## Arguments

The argument is the issue ID, e.g. `0001` or `1`. If the ID is not zero-padded, pad it to 4 digits (e.g. `1` becomes `0001`).

## Steps

1. Parse the argument as an issue ID. Zero-pad it to 4 digits.
2. Use the Glob tool to verify `.issues/{id}.toml` exists.
3. If the file does not exist, inform the user and stop.
4. Run `git config user.email` using the Bash tool to get the current user's email.
5. Read the issue file using the Read tool.
6. Update the `assigned_to` field in the TOML content to the git user's email. Use the Edit tool to replace the existing `assigned_to` line.
7. Append a `[[comments]]` entry to the end of the issue file using the Edit tool to log the assignment. Use the current date in `YYYY-MM-DD` format. Format:

```toml

[[comments]]
author = "{email}"
date = "{today}"
message = "Assigned to {email}"
```

8. Run `git add .issues/{id}.toml` using the Bash tool.
9. Display the updated issue to the user, confirming the assignment.

## Allowed tools

- `Bash(git *)` - for git config and git add
- `Read` - for reading the issue file
- `Write` - for writing the updated issue file
- `Glob` - for verifying the issue file exists
