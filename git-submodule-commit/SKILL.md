---
name: git-submodule-commit
description: Commit changes in a submodule and update the parent repo reference
argument-hint: "<submodule-path>"
---

Steps:

1. Parse `$ARGUMENTS` as the submodule path. If not provided, default to `.claude/skills`.
2. Verify the path is a valid submodule by checking `.gitmodules`.
3. Check for changes in the submodule (`git -C <path> status`). If clean, inform user and stop.
4. Show the submodule diff to the user for review.
5. Stage all changes in the submodule (`git -C <path> add -A`).
6. Commit in the submodule with a descriptive message and `[skip ci]` (`git -C <path> commit`).
7. Push the submodule to its remote (`git -C <path> push`).
8. Stage the submodule reference update in the parent repo (`git add <path>`).
9. Commit the parent repo with message referencing the submodule update and `[skip ci]`.
10. Push the parent repo to its remote (`git push`).
