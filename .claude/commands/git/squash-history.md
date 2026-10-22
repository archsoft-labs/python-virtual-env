---
description: Rewrites the entire repository history into a single commit (full squash of the main branch) and force pushes
allowed-tools: Bash(git *)
---

# git-squash-history

⚠️ **Destructive and irreversible operation**: the entire commit history will be replaced by a single commit, followed by a force push to `origin/main`. Before running, confirm with the user that they want to proceed.

Run the commands below via **Bash (Git Bash)**, sequentially, checking the output of each one. If any step fails, **stop immediately** and report the error to the user — do not continue the sequence in an intermediate state.

```bash
git checkout --orphan temp_branch
git add -A
git commit -am "Last commit"
git branch -D main
git branch -m main
git push -f origin main
```

## Notes

- `git checkout --orphan temp_branch` creates an orphan branch (no history) while keeping the working tree files.
- If there are uncommitted changes, they will be included in the single commit by `git add -A`.
- `git branch -D main` deletes the old `main` branch (we are already off it, on the orphan branch).
- `git branch -m main` renames the current branch to `main`.
- `git push -f` overwrites the remote history. Anyone with a clone of the repository will need to re-clone or hard reset.
- When finished, show the user the output of `git log --oneline` to confirm only one commit remains.
