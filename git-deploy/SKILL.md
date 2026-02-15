---
name: git-deploy
description: Merge feature branch into `develop` branch and push
disable-model-invocation: true
allowed-tools: Bash(git *)
---

Merge all changes in the current branch to the `develop` branch and checkout the feature branch once pushed.

Steps:
1. Ensure that there are not any uncommitted files.  If there are files that are uncommitted, then list them and recommend removing them or committting them.
2. Checkout the `develop`  branch (git checkout develop)
3. Pull the `develop`  branch to ensure that it is in sync
4. Merge the feature branch using the options --no-ff  (`git merge --no-ff -`)
5. Ensure there was not a conflict.
6. If there was a conflict stop and print out the details of the conflict.
7. Push `develop`  branch to remote.
8. Upon succeess, check out last branch (`git checkout -`)

