# issues-create

Create a new issue in the git-native issue tracker.

## Arguments

The argument string is parsed as follows:
- If no flags are provided, the entire argument is used as the issue title.
- Supported flags: `--title`, `--description`, `--labels` (comma-separated), `--priority` (low/medium/high), `--assigned-to`, `--status` (open/closed).
- Defaults: description="", labels=[], priority="medium", assigned_to="", status="open", closed=false.

## Steps

1. Ensure the `.issues/` directory exists at the repo root. If not, create it.
2. Use the Glob tool to scan `.issues/*.toml` for existing issue files.
3. Determine the next ID by finding the highest numeric ID among existing files and adding 1. If no issues exist, start at `0001`. Zero-pad the ID to 4 digits.
4. Parse the arguments:
   - If the argument contains flags like `--title "something"`, parse each flag.
   - Otherwise, treat the entire argument string as the title.
5. Create the TOML file at `.issues/{id}.toml` using the Write tool with this exact format:

```toml
id = "{id}"
title = "{title}"
description = "{description}"
labels = [{labels}]
priority = "{priority}"
assigned_to = "{assigned_to}"
status = "{status}"
closed = false
created_at = "{today's date in YYYY-MM-DD format}"
```

For the labels array, format each label as a quoted string, e.g. `labels = ["bug", "urgent"]`.

6. Run `git add .issues/{id}.toml` using the Bash tool.
7. Display the created issue to the user, showing the ID and title.

## Allowed tools

- `Bash(git *)` - for git add
- `Read` - for reading existing issues if needed
- `Write` - for creating the TOML file
- `Glob` - for scanning existing issue files
