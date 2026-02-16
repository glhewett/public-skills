# Claude Code Skills

A collection of reusable [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skills for git workflows and issue tracking.

## Issue Tracking

This repo includes an experimental, minimalist issue tracker designed for small projects and solo contributors. All interaction happens through Claude Code skills — there is no separate UI or CLI.

- **Creating** an issue adds a new `.toml` file in the `.issues/` directory and commits it to git.
- **Starting** work on an issue sets it to in-progress, commits to main, and creates a feature branch based on the issue.
- **Completing** an issue closes it with a comment.
- **Purging** removes all closed issues from the repository.

The issue skills are built on top of a small collection of git skills (`git-commit`, `git-feature-start`, `git-feature-complete`).

## Repo Structure

Each skill lives in its own directory with a `SKILL.md` file:

```
<skill-name>/
  SKILL.md
```

Claude Code discovers skills by looking for `SKILL.md` files one level deep in a skills directory. This repo's flat structure maps directly to that convention.

### Included Skills

| Skill | Description |
|-------|-------------|
| `git-commit` | Structured git commits |
| `git-deploy` | Deployment workflow |
| `git-feature-start` | Start a new feature branch |
| `git-feature-complete` | Complete a feature branch |
| `issues-assign` | Assign issues |
| `issues-comment` | Comment on issues |
| `issues-complete` | Complete/close issues |
| `issues-create` | Create new issues |
| `issues-list` | List issues |
| `issues-purge` | Purge closed issues |
| `issues-show` | Show issue details |
| `issues-start` | Start work on an issue |

## Usage as a Git Submodule

Add this repo as a submodule at `.claude/skills/` in any project to share skills with collaborators:

```bash
git submodule add git@github.com:glhewett/public-skills.git .claude/skills
git commit -m "Add skills submodule"
```

When cloning a project that includes this submodule:

```bash
# Clone with submodules in one step
git clone --recurse-submodules <project-url>

# Or initialize submodules after cloning
git submodule update --init
```

### .gitignore Considerations

The `.claude/` directory typically contains other files that shouldn't be version-controlled (like `settings.json` and `CLAUDE.md`). Since the submodule is tracked via `.gitmodules`, you can safely gitignore the sibling files. For example, in your project's `.gitignore`:

```
.claude/*
!.claude/skills
```

This ignores everything in `.claude/` except the `skills` submodule.

### Updating the Submodule

To pull the latest skills into your project:

```bash
git submodule update --remote .claude/skills
git commit -m "Update skills submodule"
```
