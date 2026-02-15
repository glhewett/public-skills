# issues-purge

Remove all closed issues from the repository via `git rm` and commit.

## Arguments

None required.

## Steps

1. Use the Glob tool to find all `.issues/*.toml` files.
2. Read each issue file using the Read tool.
3. Identify all issues where `closed = true`.
4. If no closed issues are found, inform the user and stop.
5. Display the list of closed issues that will be purged (ID and title).
6. Ask the user to confirm the purge.
7. For each closed issue, run `git rm .issues/{id}.toml` using the Bash tool.
8. Run `git commit -m "Purge closed issues: {list of IDs}"` using the Bash tool.
9. Confirm to the user how many issues were purged.

## Allowed tools

- `Bash(git *)` - for git rm and git commit
- `Read` - for reading issue files
- `Glob` - for finding issue files
