# issues-start

Start working on an issue by updating its status, committing to main, creating a feature branch, and entering plan mode with the issue context.

## Arguments

The argument is the issue ID, e.g. `0001` or `1`. If the ID is not zero-padded, pad it to 4 digits (e.g. `1` becomes `0001`).

## Steps

1. Parse the argument as an issue ID. Zero-pad it to 4 digits.
2. Use the Glob tool to verify `.issues/{id}.toml` exists.
3. If the file does not exist, inform the user and stop.
4. Read the issue file using the Read tool and display all fields to the user.
5. Verify the working tree is clean by running `git status --porcelain` using the Bash tool. If there is any output (dirty tree), list the uncommitted files and stop — tell the user to commit or stash first.
6. Verify we are on the `main` branch by running `git branch --show-current` using the Bash tool. If the current branch is not `main`, inform the user and stop.
7. Update the issue file: set `status = "in_progress"` using the Edit tool.
8. Run `git config user.email` using the Bash tool to get the current user's email.
9. Append a `[[comments]]` entry to the end of the issue file using the Edit tool to log that work has started. Use the current date in `YYYY-MM-DD` format. Format:

```toml

[[comments]]
author = "{email}"
date = "{today}"
message = "Started work on this issue"
```

10. Stage the issue file: run `git add .issues/{id}.toml` using the Bash tool.
11. Commit with message: `"Start issue {id}: {title} [skip-ci]"` using the Bash tool.
12. Push to main: run `git push` using the Bash tool.
13. Invoke `/git-feature-start issue-{id}` using the Skill tool to create the `feature/issue-{id}` branch.
14. Enter plan mode using `EnterPlanMode`. In the plan context, include the issue's title, description, and all comments as the requirements to plan against.

## Allowed tools

- `Bash(git *)` - for git status, git config, git add, git commit, git push
- `Read` - for reading the issue file
- `Edit` - for updating status and appending comments
- `Glob` - for verifying the issue file exists
- `Skill(git-feature-start)` - for creating the feature branch
- `EnterPlanMode` - for entering plan mode with issue context
