# issues-complete

Complete an issue by marking it as closed with a closing comment.

## Arguments

The argument is the issue ID, e.g. `0001` or `1`. If the ID is not zero-padded, pad it to 4 digits (e.g. `1` becomes `0001`).

## Steps

1. Parse the argument as an issue ID. Zero-pad it to 4 digits.
2. Use the Glob tool to verify `.issues/{id}.toml` exists.
3. If the file does not exist, inform the user and stop.
4. Read the issue file using the Read tool and display all its fields to the user.
5. Ask the user for a closing comment explaining why/how the issue was resolved.
6. Update the issue file:
   - Set `status = "complete"`
   - Set `closed = true`
7. Run `git config user.email` using the Bash tool to get the current user's email.
8. Append a `[[comments]]` entry to the end of the issue file using the Edit tool to log the completion. Use the current date in `YYYY-MM-DD` format. Format:

```toml

[[comments]]
author = "{email}"
date = "{today}"
message = "Issue completed: {closing comment}"
```

9. Run `git add .issues/{id}.toml` using the Bash tool.
10. Confirm to the user that the issue has been completed.
11. Invoke `/git-commit` using the Skill tool to commit the changes.
12. Invoke `/git-feature-complete` using the Skill tool to merge to the main branch.


## Allowed tools

- `Bash(git *)` - for git add
- `Read` - for reading the issue file
- `Write` - for writing the updated issue file
- `Glob` - for verifying the issue file exists
- `Skill(git-commit)` - for committing the changes
