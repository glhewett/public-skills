---
name: git-merge-into
description: Merge feature branch into `$BRANCH` branch and push
argument-hint: "[branch]"
allowed-tools: Bash(git *)
---

Merge all changes in the current branch to the `$BRANCH` branch and checkout the feature branch once pushed.

Steps: 0. If the $BRANCH argument is not provided, then use the `develop` branch

1. Ensure that there are not any uncommitted files. If there are files that are uncommitted, then list them and recommend removing them or committting them.
2. Checkout the `$BRANCH` branch (git checkout $BRANCH)
3. Pull the `$BRANCH` branch to ensure that it is in sync
4. Merge the feature branch using the options --no-ff (`git merge --no-ff -`)
5. Ensure there was not a conflict.
6. If there was a conflict stop and print out the details of the conflict.
7. Push `$BRANCH` branch to remote.
8. Upon succeess, check out last branch (`git checkout -`)
