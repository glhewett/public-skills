---
name: git-feature-complete
description: Create a new feature branch from the main branch
disable-model-invocation: true
argument-hint: "[branch-name]"
allowed-tools: Bash(git *)
---

Completing the current feature will result in merge the feature branch into main and removing the feature branch.

Before doing anything.
* Stop if there are any unstaged or uncommitted changes.
* Stop if there are any errors or warning when running tests and linting.
* Stop if the current branch does not begins with "feature/*"

Steps:
1. Check that $ARGUMENTS is provided. If not, we will merge into the `main` branch.  If so, replace the use of the main branch with the `$ARGUMENTS` branch.
2. Always confirm with the user that we will be merging the current branch into the main branch. 
3. Check out the main (hint: `git co main`)
4. Sync the current branch with a pull from the remote. (hint: `git pull`)
5. Merge the feature branch into the current branch. (hint: `git merge --no-ff -` replace `-` with the feature branch name to be more precise)
6. If the merge is successful, then push the main branch to the remote (hint: git push)
7. If the push to the remote is successful, Remove the local feature branch.
