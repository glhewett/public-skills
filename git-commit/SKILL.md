---
name: git-commit
description: Create a git commit
disable-model-invocation: true
allowed-tools: Bash(git *)
---

Steps:
1. Ensure that we are not on the main branch or the development branch.
2. Ensure that all files are in the current functionality being work on.
3. Have lint and test scripts run? If not, run them.
4. If there are other files came from other work, then print the files and exit.
5. If all of the change are related to this commit, then create a complete commit message and commit all of the files.
6. If the push option is true, then push to the remote
7. Recommend to deploy with the /deploy skill

