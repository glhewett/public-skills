# issues-comment

Add a comment to an existing issue.

## Arguments

The argument is the issue ID, e.g. `0001` or `1`. If the ID is not zero-padded, pad it to 4 digits (e.g. `1` becomes `0001`).

## Steps

1. Parse the argument as an issue ID. Zero-pad it to 4 digits.
2. Use the Glob tool to verify `.issues/{id}.toml` exists.
3. If the file does not exist, inform the user and stop.
4. Read the issue file using the Read tool.
5. Display the issue title and any existing comments so the user has context.
6. Ask the user for their comment text.
7. Run `git config user.email` using the Bash tool to get the current user's email.
8. Append a new `[[comments]]` entry to the end of the issue file using the Edit tool. Use the current date in `YYYY-MM-DD` format. Format:

```toml

[[comments]]
author = "{email}"
date = "{today}"
message = """
{comment text}
"""
```

9. Run `git add .issues/{id}.toml` using the Bash tool.
10. Display the added comment back to the user confirming it was saved.

## Allowed tools

- `Bash(git *)` - for git config and git add
- `Read` - for reading the issue file
- `Edit` - for appending the comment to the issue file
- `Glob` - for verifying the issue file exists
