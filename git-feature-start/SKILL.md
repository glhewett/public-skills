---
name: git-feature-start
description: Create a new feature branch from the main branch
argument-hint: "[feature-name]"
allowed-tools: Bash(git *)
---

Create a new feature branch named `feature/$ARGUMENTS` from the `main` branch.

Steps:

1. Ensure that $ARGUMENTS is provided. If not, print usage: `/git-feature <feature-name>` and exit.
2. Ensure there are no uncommitted changes. If there are uncommitted files, list them and recommend committing or stashing them before continuing.
3. Checkout the `main` branch (`git checkout main`).
4. Pull the latest changes from the remote (`git pull`).
5. Create and checkout the new feature branch (`git checkout -b feature/$ARGUMENTS`).
6. Push the new branch to the remote and set up tracking (`git push -u origin feature/$ARGUMENTS`).
7. Confirm the new branch was created and is active.
