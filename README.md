# Claude Code Skills

A collection of reusable [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skills for git workflows and issue tracking.

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

## Public vs. Private Skills

Claude Code discovers skills from two independent locations:

- **Project-level**: `{repo}/.claude/skills/` — committed to the project, shared with collaborators
- **User-level**: `~/.claude/skills/` — personal to the user, not committed to any repo

This provides a natural public/private separation:

- **Public skills** — Use this repo as a submodule at `.claude/skills/` in your projects. These skills are version-controlled and shared with anyone who clones the project.
- **Private skills** — Place personal skills in `~/.claude/skills/`. These are only available to you and never appear in project repos.

Both locations are active simultaneously, so you get the union of project-level and user-level skills in every session.

## User-Level Installation

To install all skills from this repo as user-level skills (available in all your projects):

```bash
makers link
```

This symlinks each skill directory into `~/.claude/skills/`. To remove the symlinks:

```bash
makers unlink
```

This approach requires [cargo-make](https://github.com/sagiegurari/cargo-make) (`makers` command).
