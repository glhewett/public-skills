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
   - Add `closed_comment = "{comment}"` after the `closed` field
7. Run `git add .issues/{id}.toml` using the Bash tool.
8. Confirm to the user that the issue has been completed.

## Allowed tools

- `Bash(git *)` - for git add
- `Read` - for reading the issue file
- `Write` - for writing the updated issue file
- `Glob` - for verifying the issue file exists
