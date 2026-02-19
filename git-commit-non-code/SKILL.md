---
name: git-commit-non-code
description: Create a git commit for changes that are affecting code.
disable-model-invocation: true
allowed-tools: Bash(git *)
argument-hint: "[push-commit]"
---

Steps:
1. Ensure that all files are in the current functionality being work on.
2. Ensure that all of the changes in the current functionality do not change the functionality of the project.  This includes documentation and configuration.
3. Create the commit and be sure to include any comments in the commit for skipping CI in circleci or jenkins
3. If the push-commit option is true, then push to the remote

