---
name: issues-plan
description: Create a plan for an issue using its title and comments, and add it as a multi-line comment.
disable-model-invocation: true
argument-hint: "[issue-id]"
allowed-tools: Bash(git *), Read, Edit, Glob
---

## Arguments

The argument is the issue ID, e.g. `0001` or `1`. If the ID is not zero-padded, pad it to 4 digits (e.g. `1` becomes `0001`).

## Steps

1. Parse the argument as an issue ID. Zero-pad it to 4 digits.
2. Use the Glob tool to verify `.issues/{id}.toml` exists.
3. If the file does not exist, inform the user and stop.
4. Read the issue file using the Read tool.
5. Display the issue title and any existing comments so the user has context.
6. Use the text to create a plan for how the work described in the issue could be done.
7. The plan should be enough to save planning tokens in the future. Concise but helpful. Include and design decisions. and try to come up with a determination of the complexity of the change.
8. Append a new `[[comments]]` entry to the end of the issue file using the Edit tool. Use the current date in `YYYY-MM-DD` format. Use a description of the claude agent as the author. Format:

```toml

[[comments]]
author = "{email}"
date = "{today}"
message = """
{markdown comment text}
"""
```

9. Change the status to "planned"
10. Run `git add .issues/{id}.toml` using the Bash tool.
11. Display the added comment back to the user confirming it was saved.

## Allowed tools

- `Bash(git *)` - for git config and git add
- `Read` - for reading the issue file
- `Edit` - for appending the comment to the issue file
- `Glob` - for verifying the issue file exists
