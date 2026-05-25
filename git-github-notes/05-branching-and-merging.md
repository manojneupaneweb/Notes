# 05 — Branching and Merging

---

## 📌 Why Branches?

Branches let you work on **new features or fixes in isolation** without affecting the stable `main` branch.

```
main:       A ─── B ─── C                  ─── G (merge)
                         \                /
feature:                  ─── D ─── E ─── F
```

- `main` stays stable while you develop on `feature`.
- When the feature is done, you **merge** it back into `main`.

---

## 🌿 Branch Commands

### Creating and Switching Branches

```bash
# List all branches (current branch has * and is highlighted)
git branch

# List all branches including remote branches
git branch -a

# Create a new branch (stays on current branch)
git branch feature/login

# Create AND switch to a new branch (modern way ✅)
git switch -c feature/login

# Create AND switch (older way — still works)
git checkout -b feature/login

# Switch to an existing branch
git switch main

# Switch (older way)
git checkout main

# Switch back to the previous branch
git switch -
```

> 💡 **Naming convention:** Use descriptive names like:
> - `feature/user-authentication`
> - `fix/navbar-overflow`
> - `docs/update-readme`
> - `refactor/api-calls`

---

### Renaming and Deleting Branches

```bash
# Rename the current branch
git branch -m new-name

# Rename any branch
git branch -m old-name new-name

# Delete a branch (safe — only if fully merged)
git branch -d feature/login

# Force delete (even if not merged — be careful!)
git branch -D feature/login

# Delete a remote branch
git push origin --delete feature/login
```

---

## 🔀 `git merge` — Combine Branches

Once your feature is complete, merge it into `main`.

```bash
# Step 1: Switch to the branch you want to merge INTO
git switch main

# Step 2: Merge the feature branch into main
git merge feature/login

# Merge with a commit message (no fast-forward — keeps history clean)
git merge --no-ff feature/login -m "Merge feature/login into main"
```

### Types of Merges

#### 1. Fast-Forward Merge
When `main` hasn't had new commits since the branch was created — Git just moves the pointer forward.

```
Before:
main:    A ─── B
                \
feature:         C ─── D

After (fast-forward):
main:    A ─── B ─── C ─── D
```

```bash
git merge feature/login
# Output: Fast-forward
```

#### 2. Three-Way Merge (Merge Commit)
When `main` has new commits since the branch was created — Git creates a new "merge commit".

```
Before:
main:    A ─── B ─── C
                \
feature:         D ─── E

After (merge commit):
main:    A ─── B ─── C ─── M  (M = merge commit)
                \           /
feature:         D ─── E ──
```

```bash
git merge --no-ff feature/login
# Output: Merge made by the 'ort' strategy.
```

---

## ⚡ Merge Conflicts

A **merge conflict** happens when two branches have changed the **same lines** of the same file. Git can't decide which change to keep — you must resolve it manually.

### When do conflicts happen?

```bash
git merge feature/login

# Output when conflict occurs:
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

### What a conflict looks like in the file:

```html
<<<<<<< HEAD              ← Your current branch (main)
<h1>Welcome to My Site</h1>
=======                   ← Divider between the two versions
<h1>Hello World!</h1>
>>>>>>> feature/login     ← The branch being merged in
```

### How to resolve it:

**Step 1:** Open the conflicted file in VS Code (it highlights conflicts).

**Step 2:** Choose what to keep. You can:
- Keep YOUR version (delete the `feature/login` lines)
- Keep THEIR version (delete the `HEAD` lines)
- Keep BOTH (combine them)
- Write something completely new

```html
<!-- After resolution: -->
<h1>Welcome to My Site</h1>
```

**Step 3:** Remove ALL conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).

**Step 4:** Stage and commit the resolution.
```bash
git add index.html
git commit -m "Resolve merge conflict in index.html"
```

### VS Code makes conflict resolution easy:
- Click **"Accept Current Change"** — keep HEAD version
- Click **"Accept Incoming Change"** — keep feature branch version
- Click **"Accept Both Changes"** — keep both
- Click **"Compare Changes"** — see a side-by-side diff

---

## 📋 Real-World Branching Example

```bash
# You're on main — stable code
git switch main

# Pull latest changes from GitHub
git pull origin main

# Create a new feature branch
git switch -c feature/dark-mode

# Work on your feature
# ... edit files ...

# Stage and commit your work
git add .
git commit -m "feat: add dark mode toggle and CSS variables"

# Make more commits as needed
git add .
git commit -m "feat: persist dark mode preference in localStorage"

# Switch back to main
git switch main

# Merge your feature
git merge --no-ff feature/dark-mode -m "Merge feature/dark-mode"

# Delete the feature branch (no longer needed)
git branch -d feature/dark-mode

# Push updated main to GitHub
git push origin main
```

---

## 📊 Branch Commands Quick Reference

| Command | What it does |
|---------|-------------|
| `git branch` | List local branches |
| `git branch -a` | List all branches (local + remote) |
| `git switch -c <name>` | Create and switch to new branch |
| `git switch <name>` | Switch to existing branch |
| `git switch -` | Switch to previous branch |
| `git branch -d <name>` | Delete branch (safe) |
| `git branch -D <name>` | Force delete branch |
| `git merge <name>` | Merge branch into current branch |
| `git merge --no-ff <name>` | Merge with a merge commit |
| `git merge --abort` | Cancel a merge in progress |

---

> ➡️ **Next:** `06-remote-repositories.md` — Connect to GitHub and share your code.
