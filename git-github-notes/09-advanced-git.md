# 09 — Advanced Git

---

## 🔁 `git rebase` — Rewrite Commit History

**Rebase** replays your commits on top of another branch, creating a **linear, clean history**.

```
Before rebase:
main:    A ─── B ─── C
                \
feature:         D ─── E

After rebase (feature onto main):
main:    A ─── B ─── C
                          \
feature (rebased):         D' ─── E'   ← New commits (D and E replayed on top of C)
```

The commits D and E are replayed as new commits D' and E' with new hashes.

### Basic Rebase:
```bash
# You're on feature/login, want to bring in latest main commits
git switch feature/login
git rebase main

# Or in one line:
git rebase main feature/login
```

### Interactive Rebase — The Power Tool:
`git rebase -i` lets you edit, reorder, squash, and drop commits.

```bash
# Interactively rebase the last 3 commits
git rebase -i HEAD~3

# Interactively rebase since a specific commit
git rebase -i 9d1e4f7
```

This opens your editor with:
```
pick a3f5b2c Add login form HTML
pick 7b1c3d4 Add login form CSS
pick e9f2a1b Fix typo in login form

# Commands:
# p, pick   = use commit as-is
# r, reword = use commit, but edit the message
# e, edit   = use commit, but stop to amend it
# s, squash = combine with previous commit
# f, fixup  = like squash, but discard this commit's message
# d, drop   = remove this commit entirely
# Commits are in oldest-to-newest order
```

#### Common interactive rebase operations:

```bash
# Squash 3 commits into 1
pick a3f5b2c Add login form HTML
squash 7b1c3d4 Add login form CSS
squash e9f2a1b Fix typo in login form
# → Results in 1 commit with a combined message

# Rename a commit message
reword a3f5b2c Add login form HTML
# → Opens editor to type a new message

# Remove a commit entirely
drop e9f2a1b Fix typo in login form
# → That commit is gone

# Reorder commits (just change the order in the file)
pick 7b1c3d4 Add login form CSS
pick a3f5b2c Add login form HTML
# → CSS commit now comes before HTML commit
```

### Rebase vs Merge:

| | Merge | Rebase |
|-|-------|--------|
| **History** | Preserves exact history (merge commits) | Creates linear, clean history |
| **Safety** | Safe on shared branches | ⚠️ Rewrites history |
| **Use when** | Merging feature → main | Updating a feature branch with main's changes |
| **Result** | Branching visible in graph | Looks like work was always on one line |

> ⚠️ **Golden Rule of Rebase:** Never rebase commits that have been pushed to a shared/public branch.

---

## 🍒 `git cherry-pick` — Pick a Specific Commit

**Cherry-pick** applies the changes from a specific commit to your current branch.

```
main:    A ─── B ─── C ─── D
                \
hotfix:          E ─── F ← We only want commit F on main!
```

```bash
# Apply commit F (e9f2a1b) to main
git switch main
git cherry-pick e9f2a1b

# Cherry-pick a range of commits
git cherry-pick 9d1e4f7..a3f5b2c

# Cherry-pick without committing (stage only)
git cherry-pick --no-commit e9f2a1b

# Cherry-pick with a custom commit message
git cherry-pick e9f2a1b --edit
```

### Common use case:
```bash
# You fixed a critical bug on feature/login but need it on main NOW
git log feature/login --oneline
# f8a2b1c (feature/login) fix: resolve null pointer in auth middleware

# Apply just that fix to main
git switch main
git cherry-pick f8a2b1c
git push origin main
```

---

## 🏷️ Tags — Mark Important Points in History

**Tags** mark specific commits as important — usually used for version releases.

```bash
# Create a lightweight tag (just a pointer to a commit)
git tag v1.0.0

# Create an annotated tag (RECOMMENDED — includes message, author, date)
git tag -a v1.0.0 -m "Release version 1.0.0"

# Tag a specific commit
git tag -a v0.9.0 -m "Beta release" 9d1e4f7

# List all tags
git tag

# List tags matching a pattern
git tag -l "v1.*"

# Show tag details
git show v1.0.0

# Push tags to GitHub (tags are NOT pushed with regular git push)
git push origin v1.0.0    # Push a specific tag
git push origin --tags     # Push all tags

# Delete a tag locally
git tag -d v1.0.0

# Delete a tag on GitHub
git push origin --delete v1.0.0
```

### Semantic Versioning (SemVer):
```
v MAJOR . MINOR . PATCH
v  1   .   2   .   3

MAJOR: Breaking changes (incompatible with previous version)
MINOR: New features (backward compatible)
PATCH: Bug fixes (backward compatible)
```

---

## 📂 `git stash` — Advanced Usage

_(Basic stash covered in 08-undoing-changes.md — here are advanced patterns)_

```bash
# Stash only specific files
git stash push -m "Save only CSS changes" -- style.css

# Stash and create a branch from it
git stash branch feature/experiment stash@{0}
# Creates a new branch at the commit where stash was created,
# applies the stash, and drops it if successful

# Show all stashes with their diffs
git stash list --stat
```

---

## 📝 Git Aliases — Your Own Shortcuts

Add shortcuts for long commands in your Git config.

```bash
# Add aliases via command line
git config --global alias.st status
git config --global alias.co switch
git config --global alias.lg "log --oneline --graph --all"
git config --global alias.unstage "restore --staged"
git config --global alias.last "log -1 HEAD"

# Usage:
git st        # → git status
git co main   # → git switch main
git lg        # → pretty git log graph
git unstage index.html  # → git restore --staged index.html
git last      # → shows last commit
```

**Or edit `~/.gitconfig` directly:**
```ini
[alias]
    st     = status
    co     = switch
    br     = branch
    lg     = log --oneline --graph --all --decorate
    last   = log -1 HEAD --stat
    undo   = reset --soft HEAD~1
    unstage = restore --staged
    aliases = config --get-regexp alias
```

---

## 🔎 `git bisect` — Find the Commit That Introduced a Bug

Binary search through your history to find exactly which commit broke something.

```bash
# Start bisect
git bisect start

# Tell Git the current state is bad (has the bug)
git bisect bad

# Tell Git a known good commit (no bug)
git bisect good v1.0.0

# Git will checkout a commit halfway between — test your code
# If it still has the bug:
git bisect bad
# If the bug is gone:
git bisect good

# Git keeps narrowing it down until it finds the exact commit
# "First bad commit: a3f5b2c — introduced broken auth middleware"

# Exit bisect mode
git bisect reset
```

---

## 🔗 `git submodule` — Repos Inside Repos

Submodules let you include one Git repo inside another — for shared libraries or dependencies.

```bash
# Add a submodule
git submodule add https://github.com/author/shared-lib.git libs/shared

# Clone a repo that has submodules
git clone --recurse-submodules https://github.com/you/project.git

# Update all submodules
git submodule update --remote

# Remove a submodule
git submodule deinit libs/shared
git rm libs/shared
```

---

## 🔒 Git Hooks — Automate Actions

Git hooks are scripts that run automatically at specific Git events.

```
.git/hooks/
├── pre-commit      ← Runs before every commit
├── commit-msg      ← Validates commit message format
├── pre-push        ← Runs before git push
├── post-merge      ← Runs after a merge
└── post-checkout   ← Runs after switching branches
```

### Example: Prevent commits with "TODO" left in code
```bash
# .git/hooks/pre-commit
#!/bin/sh
if grep -r "TODO" --include="*.js" .; then
    echo "❌ Commit rejected: Remove all TODOs before committing!"
    exit 1
fi
```

### Example: Enforce commit message format
```bash
# .git/hooks/commit-msg
#!/bin/sh
MSG=$(cat "$1")
PATTERN="^(feat|fix|docs|style|refactor|test|chore): .+"

if ! echo "$MSG" | grep -qE "$PATTERN"; then
    echo "❌ Invalid commit message!"
    echo "   Use format: <type>: <description>"
    echo "   Types: feat, fix, docs, style, refactor, test, chore"
    exit 1
fi
```

```bash
# Make the hook executable
chmod +x .git/hooks/pre-commit
chmod +x .git/hooks/commit-msg
```

> 💡 Use [Husky](https://typicode.github.io/husky/) (npm package) to share hooks with your team — `.git/hooks` is not tracked by Git.

---

## 🌐 Advanced GitHub Features

### GitHub CLI (`gh`)

```bash
# Install: https://cli.github.com

# Authenticate
gh auth login

# Create a repo from the terminal
gh repo create my-project --public

# Create a PR from the current branch
gh pr create --title "feat: add dark mode" --body "Closes #42"

# List open PRs
gh pr list

# Review a PR in the terminal
gh pr review 15 --approve
gh pr review 15 --request-changes --body "Please add tests"

# Merge a PR
gh pr merge 15 --squash

# View issues
gh issue list
gh issue create --title "Bug: login fails" --body "Steps..."
gh issue close 42
```

### GitHub Pages — Free Static Hosting

```bash
# In your repo: Settings → Pages → Source: Deploy from a branch
# Select branch: main / folder: / (root) or /docs

# After saving, your site is at:
# https://YOUR-USERNAME.github.io/REPO-NAME/
```

For project pages, add to your repo:
```bash
# If using a framework (like Vite), set the base URL in config:
# vite.config.js
export default { base: '/repo-name/' }

# Build and deploy
npm run build
# Then commit the 'dist' folder to the gh-pages branch
```

---

## 📊 Advanced Git Quick Reference

| Command | What it does |
|---------|-------------|
| `git rebase main` | Replay feature branch commits on top of main |
| `git rebase -i HEAD~3` | Interactively edit/squash last 3 commits |
| `git cherry-pick <hash>` | Apply a specific commit to current branch |
| `git tag -a v1.0.0 -m "..."` | Create an annotated release tag |
| `git push origin --tags` | Push all tags to GitHub |
| `git bisect start/bad/good` | Binary search for a buggy commit |
| `git stash push -m "name"` | Save work with a description |
| `git stash branch <name>` | Create a branch from a stash |
| `git config --global alias.lg "..."` | Create a custom alias |

---

> 🎉 **You've completed all Git & GitHub Notes!**
> 
> **Now practice by:**
> 1. Creating your own GitHub repos for all your projects
> 2. Contributing to an open-source project (find issues labelled `good first issue`)
> 3. Using Git for every project — even solo work!
