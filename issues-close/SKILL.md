---
name: issues-close
description: Close an issue by marking it as closed with a reason.
disable-model-invocation: true
argument-hint: "[issue-id]"
---

## Arguments

s
The argument is the isue ID, e.g. `0001` or `1`. If the ID is not zero-padded, pad it to 4 digits (e.g. `1` becomes `0001`).

## Steps

1. Parse the argument as an issue ID. Zero-pad it to 4 digits.
2. Use the Glob tool to verify `.issues/{id}.toml` exists.
3. If the file does not exist, inform the user and stop.
4. Read the issue file using the Read tool and display all its fields to the user.
5. Ask the user for a reason why the issue is being closed.
6. Update the issue file:
   - Set `status = "closed"`
   - Set `closed = true`
7. Run `git config user.email` using the Bash tool to get the current user's email.
8. Append a `[[comments]]` entry to the end of the issue file using the Edit tool to log the closure. Use the current date in `YYYY-MM-DD` format. Format:

```toml
[[comments]]
author = "{email}"
date = "{today}"
message = "Issue closed: {reason}"
```

9. Run `git add .issues/{id}.toml` using the Bash tool.
10. Commit the changes using the Bash tool with message: `"Close issue {id}: {title} [skip-ci]"`
11. Push to remote using the Bash tool: `git push`
12. Confirm to the user that the issue has been closed and pushed.

## Allowed tools

- `Bash(git *)` - for git config, git add, git commit, git push
- `Read` - for reading the issue file
- `Edit` - for updating status and appending comments
- `Glob` - for verifying the issue file exists
