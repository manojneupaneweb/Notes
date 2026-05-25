# 08 — Undoing Changes

---

## 📌 The Safety Net

One of Git's superpowers is being able to **undo almost anything**. This is a key reason to use Git — you can experiment fearlessly knowing you can always go back.

> 💡 **Key Rule:** Commits that exist only on your local machine can be rewritten freely. Commits pushed to a shared remote should be undone using `git revert` (which adds a new commit) instead of rewriting history.

---

## 🗂️ Undoing in the Working Tree (Before `git add`)

```bash
# Discard changes to a single file (restore to last commit state)
git restore index.html
# or (older syntax)
git checkout -- index.html

# Discard ALL changes in working tree (reset everything to last commit)
git restore .

# ⚠️ WARNING: These commands permanently delete your unsaved changes!
# There is NO undo for this — the changes are gone.
```

---

## 🎭 Unstaging Files (After `git add`, Before `git commit`)

```bash
# Unstage a single file (keep changes in working tree)
git restore --staged index.html

# Unstage all files
git restore --staged .

# Older syntax (also works)
git reset HEAD index.html
```

---

## 🔄 Undoing Commits

### `git commit --amend` — Fix the Last Commit

Use this to fix a mistake in the most recent commit **before pushing**.

```bash
# Fix the commit message only
git commit --amend -m "Correct commit message"

# Add a forgotten file to the last commit
git add forgotten-file.js
git commit --amend --no-edit   # Keeps the same message

# ⚠️ Never amend commits that have been pushed to a shared branch!
```

---

### `git reset` — Move HEAD Backward

`git reset` moves the current branch pointer back to a previous commit.

```
Before:  A ─── B ─── C   (HEAD)
After:   A ─── B         (HEAD) ← C is removed from the branch
```

```bash
# View commit history to find the commit hash
git log --oneline

# Example output:
# a3f5b2c (HEAD → main) Bad commit
# 9d1e4f7 Good commit
# 2b8c3a1 Initial commit
```

#### Three modes of `git reset`:

```bash
# 1. --soft: Move HEAD back, keep changes STAGED
git reset --soft 9d1e4f7
# Your files are untouched, changes from "Bad commit" are staged
# → Useful: when you want to redo the commit with a better message

# 2. --mixed (DEFAULT): Move HEAD back, keep changes in working tree (unstaged)
git reset 9d1e4f7
git reset --mixed 9d1e4f7
# Your files are untouched, changes from "Bad commit" are unstaged
# → Useful: when you want to re-stage and re-commit differently

# 3. --hard: Move HEAD back, DELETE all changes (DANGEROUS!)
git reset --hard 9d1e4f7
# ALL changes from "Bad commit" are permanently destroyed
# → Useful: when you want to completely undo the commit and changes

# Reset to last commit (undo uncommitted changes + staging)
git reset --hard HEAD
```

> ⚠️ **`git reset` rewrites history** — only use it on commits that haven't been pushed to a shared remote.

---

### `git revert` — Undo a Commit Safely (For Pushed Commits)

`git revert` creates a **new commit** that undoes the changes of a previous commit. It does NOT rewrite history.

```
Before:  A ─── B ─── C   (HEAD)
After:   A ─── B ─── C ─── R   (HEAD)  R = revert commit that undoes C
```

```bash
# Revert the most recent commit
git revert HEAD

# Revert a specific commit
git revert a3f5b2c

# Revert without opening the commit message editor
git revert HEAD --no-edit

# Revert multiple commits
git revert HEAD~2..HEAD   # Reverts last 2 commits

# Stage the revert but don't commit yet (so you can edit the message)
git revert --no-commit a3f5b2c
git commit -m "revert: undo broken login changes from a3f5b2c"
```

> ✅ **`git revert` is safe to use on pushed commits.** It doesn't rewrite history.

---

## 📦 `git stash` — Temporarily Save Unfinished Work

`git stash` saves your uncommitted work temporarily so you can switch branches or pull without losing changes.

```bash
# Save all changes (tracked files) to the stash
git stash

# Save with a descriptive name
git stash push -m "WIP: half-finished login form"

# Stash including untracked files
git stash push --include-untracked -m "WIP: including new files"

# List all stashes
git stash list
# Output:
# stash@{0}: WIP: half-finished login form  ← most recent
# stash@{1}: WIP: quick fix attempt

# Apply the most recent stash (keeps it in the stash list)
git stash apply

# Apply a specific stash
git stash apply stash@{1}

# Apply and REMOVE the most recent stash from the list
git stash pop

# Remove a specific stash
git stash drop stash@{0}

# Remove all stashes
git stash clear

# See what's in a stash
git stash show stash@{0}
git stash show -p stash@{0}  # With full diff
```

### Common stash workflow:
```bash
# You're working on a feature when an urgent bug is reported

# Step 1: Stash your current work
git stash push -m "WIP: new search feature"

# Step 2: Switch to main and fix the bug
git switch main
git pull origin main
git switch -c fix/critical-bug
# ... fix the bug ...
git commit -m "fix: resolve checkout crash on empty cart"
git push origin fix/critical-bug
# (Create PR and merge it)

# Step 3: Go back to your feature
git switch feature/search
git stash pop  # Restore your stashed work

# Continue where you left off! 🎉
```

---

## 🔍 `git reflog` — The Ultimate Safety Net

`reflog` records every action that moved HEAD, even `git reset --hard`. It's your **undo button for undos**.

```bash
# View all HEAD movements in the last 90 days
git reflog

# Output:
# a3f5b2c (HEAD → main) HEAD@{0}: commit: Add contact form
# 9d1e4f7 HEAD@{1}: reset: moving to HEAD~1
# a3f5b2c HEAD@{2}: commit: Add contact form (ORIGINAL — before reset!)
# 2b8c3a1 HEAD@{3}: checkout: moving from feature to main

# Restore a commit you accidentally deleted with reset --hard
git reset --hard HEAD@{2}
# or
git reset --hard a3f5b2c
```

> 💡 **Rule:** Almost nothing is truly gone in Git within 90 days. `git reflog` can usually recover it.

---

## 🏷️ Comparison: Which Undo Command to Use?

| Situation | Command | Rewrites History? | Safe on Remote? |
|-----------|---------|:-----------------:|:---------------:|
| Discard working tree changes | `git restore <file>` | ❌ | ✅ |
| Unstage a file | `git restore --staged <file>` | ❌ | ✅ |
| Fix last commit message | `git commit --amend` | ✅ | ⚠️ Only if not pushed |
| Undo last N commits (keep changes) | `git reset --soft HEAD~N` | ✅ | ⚠️ Only if not pushed |
| Undo last N commits (discard changes) | `git reset --hard HEAD~N` | ✅ | ⚠️ Only if not pushed |
| Undo a pushed commit safely | `git revert <hash>` | ❌ | ✅ |
| Save unfinished work temporarily | `git stash` | ❌ | ✅ |
| Recover from accidental reset | `git reflog` | ❌ | ✅ |

---

## 🧪 Practice Scenario

```bash
# Simulate making mistakes and fixing them

# Create some commits
git commit -m "commit A"
git commit -m "commit B — this was a mistake"
git commit -m "commit C — this was also a mistake"

git log --oneline
# c (HEAD) commit C
# b        commit B
# a        commit A

# Undo last 2 commits, keep changes staged
git reset --soft HEAD~2

git log --oneline
# a (HEAD) commit A

git status
# Changes to be committed: (all changes from B and C are staged)

# Recommit as one clean commit
git commit -m "feat: add complete auth system"
```

---

> ➡️ **Next:** `09-advanced-git.md` — Rebase, cherry-pick, tags, hooks, and power-user commands.
