# 🐙 Git & GitHub — Complete Reference Notes
### Version Control · Collaboration · Open Source — Beginner to Advanced

> **Author:** Manoj Neupane  
> **Last Updated:** May 2026  
> **Goal:** A complete, detailed reference for Git and GitHub — from basics to advanced techniques.

---

## 📑 Table of Contents

- [01 — Introduction](#01--introduction-to-git--github)
- [02 — Installation & Setup](#02--installation--setup)
- [03 — Core Concepts](#03--core-concepts)
- [04 — Basic Commands](#04--basic-commands)
- [05 — Branching & Merging](#05--branching--merging)
- [06 — Remote Repositories](#06--remote-repositories)
- [07 — GitHub Workflow](#07--github-workflow)
- [08 — Undoing Changes](#08--undoing-changes)
- [09 — Advanced Git](#09--advanced-git)
- [⚡ Quick Reference Cheat Sheet](#-quick-reference-cheat-sheet)

---

## 01 — Introduction to Git & GitHub

### 📌 What is Version Control?

**Version control** is a system that records changes to files over time so you can:

- See the **full history** of every change ever made
- **Revert** to any previous version if something breaks
- **Collaborate** with other developers without overwriting each other's work
- **Experiment** safely by creating isolated branches

> 💡 **Analogy:** Like saving `essay_v1.docx`, `essay_v2.docx`, `essay_FINAL.docx`... but Git does this automatically and much smarter.

---

### 🔧 What is Git?

**Git** is the world's most popular **version control system**.

- Created by **Linus Torvalds** (creator of Linux) in **2005**.
- Free, open-source, runs **locally** on your computer.
- Tracks changes to files and manages project history.
- Works **without the internet** — all history is on your machine.

---

### 🌐 What is GitHub?

**GitHub** is a **cloud-based hosting platform** for Git repositories.

- Stores your Git repositories **online** — accessible from anywhere.
- Adds collaboration features: Pull Requests, Issues, Code Reviews, GitHub Actions.
- Home to millions of open-source projects.

> 💡 **Key Difference:**
> - **Git** is like Microsoft Word (the software you write with)
> - **GitHub** is like Google Drive (the cloud where you store and share)

---

### 🔄 Git vs GitHub

| Git | GitHub |
|-----|--------|
| Software on your computer | Website / cloud service |
| Tracks file changes locally | Stores repos online |
| Works offline | Needs internet |
| Command-line tool | Web UI + Desktop App + CLI |
| Free & open-source | Free (with paid plans) |
| Created 2005 | Created 2008 |

---

### 🗂️ How Git Works (The Big Picture)

```
Your Computer                    GitHub (Cloud)
─────────────                    ──────────────
                                 
┌─────────────────┐              ┌──────────────────┐
│  Working Tree   │              │  Remote Repo     │
│  (your files)   │ ─── push ──► │  (github.com)    │
│                 │ ◄── pull ─── │                  │
│  Staging Area   │              │                  │
│  (ready to save)│              │                  │
│                 │              │                  │
│  Local Repo     │              │                  │
│  (saved history)│              │                  │
└─────────────────┘              └──────────────────┘
```

**Typical workflow:**
```
1. Modify files in Working Tree
        ↓
2. Stage the changes (git add)
        ↓
3. Commit the changes (git commit) → saves to Local Repo
        ↓
4. Push to GitHub (git push) → uploads to Remote Repo
```

---

### 🏷️ Key Terms Glossary

| Term | Meaning |
|------|---------|
| **Repository (repo)** | A folder tracked by Git. Contains all files + their history. |
| **Commit** | A saved snapshot of your files at a specific point in time. |
| **Branch** | A separate line of development — a parallel version of your project. |
| **Merge** | Combining changes from one branch into another. |
| **Clone** | Copying a remote repo (from GitHub) to your local machine. |
| **Push** | Uploading your local commits to GitHub. |
| **Pull** | Downloading changes from GitHub to your local machine. |
| **Fork** | Copying someone else's GitHub repo to your own GitHub account. |
| **Pull Request (PR)** | A request to merge your changes into another branch. |
| **Staging Area** | A "waiting room" — you choose what goes into the next commit. |
| **HEAD** | A pointer to the current branch/commit you are on. |
| **Origin** | The default name for the remote repo (usually on GitHub). |

---

## 02 — Installation & Setup

### 📥 Installing Git

```bash
# Windows: Download from git-scm.com/download/win

# macOS (via Homebrew)
brew install git

# Linux (Ubuntu/Debian)
sudo apt update && sudo apt install git

# Verify installation
git --version
# Output: git version 2.43.0
```

---

### ⚙️ First-Time Configuration

```bash
# Set your identity (attached to every commit)
git config --global user.name "Manoj Neupane"
git config --global user.email "manoj@example.com"

# Set default branch name
git config --global init.defaultBranch main

# Set VS Code as the default editor
git config --global core.editor "code --wait"

# Windows: fix line endings for cross-platform collaboration
git config --global core.autocrlf true

# Verify your settings
git config --global --list
```

> ⚠️ Use the `--global` flag to apply settings to ALL repos.

---

### 🔐 Setting Up SSH Keys

SSH keys let you connect to GitHub **without typing your password every time**.

```bash
# Step 1: Generate SSH key
ssh-keygen -t ed25519 -C "manoj@example.com"
# Press Enter 3 times (accept defaults)

# Step 2: Copy your public key
cat ~/.ssh/id_ed25519.pub
# Copy the output

# Step 3: Add to GitHub
# github.com → Settings → SSH and GPG keys → New SSH key → Paste

# Step 4: Test the connection
ssh -T git@github.com
# Output: Hi Manoj! You've successfully authenticated...
```

---

## 03 — Core Concepts

### 📌 The Three Areas of Git

```
┌──────────────────────────────────────────────────────────────┐
│                        Your Computer                         │
│                                                              │
│  ┌────────────────┐    git add    ┌────────────────────────┐ │
│  │  Working Tree  │ ───────────► │   Staging Area (Index) │ │
│  │  (your files)  │              │  (ready to commit)     │ │
│  └────────────────┘              └────────────┬───────────┘ │
│                                               │             │
│                                    git commit ▼             │
│                                  ┌────────────────────────┐ │
│                                  │   Local Repository     │ │
│                                  │   (saved history)      │ │
│                                  └────────────────────────┘ │
└──────────────────────────────────────────────────────────────┘
```

| Area | Description |
|------|-------------|
| **Working Tree** | Your actual files on disk — where you edit code |
| **Staging Area** | "Shopping cart" — pick which changes go in the next commit |
| **Local Repository** | `.git` folder — permanent history of all commits |

---

### 📸 What is a Commit?

A commit is a **permanent snapshot** with:
- **Unique ID (SHA hash):** `a3f5b2c`
- **Author:** Name + email
- **Timestamp:** When it was made
- **Message:** What changed
- **Parent:** Pointer to the previous commit

```
HEAD → main
   │
   ▼
commit a3f5b2c  "Add contact form" ← most recent
   │
   └── parent → commit 9d1e4f7  "Fix navbar bug"
                   │
                   └── parent → commit 2b8c3a1  "Initial commit"
```

---

### 🌿 What is a Branch?

A branch is a **lightweight pointer to a commit** — not a copy of files.

```
main:    A ─── B ─── C ─── D    ← production code
                   │
                   └─── E ─── F   ← feature/login (your new feature)
```

- Creating a branch is instant — Git just creates a new pointer.
- Changes on one branch do NOT affect other branches.

---

### 📊 File Status Lifecycle

```
Untracked ──git add──► Staged ──git commit──► Committed/Unmodified
                                                      │
                        ◄──────── edit ───────────────┘
                           (becomes Modified)
                                │
                        ◄──git add─┘ (back to Staged)
```

---

## 04 — Basic Commands

### The Essential Workflow

```bash
git init          # Create a new repo
git status        # Check what changed
git add .         # Stage all changes
git commit -m ""  # Save a snapshot
git log           # View history
```

---

### `git init` — Create a Repository

```bash
cd my-project
git init
# Output: Initialized empty Git repository in /my-project/.git/
```

---

### `git status` — Check Repo State

```bash
git status

# All clean:
# nothing to commit, working tree clean

# Untracked new file:
# Untracked files:  index.html

# Staged and ready to commit:
# Changes to be committed:  new file: index.html

# Modified but not staged:
# Changes not staged for commit:  modified: style.css
```

---

### `git add` — Stage Changes

```bash
git add index.html           # Stage a specific file
git add index.html style.css # Stage multiple files
git add .                    # Stage ALL changes
git add -u                   # Stage only tracked (modified) files
git add -p index.html        # Interactively stage parts of a file
```

---

### `git commit` — Save a Snapshot

```bash
git commit -m "Add homepage HTML structure"
git commit -am "Fix typo in navbar"   # Stage + commit (tracked files only)
git commit --amend -m "Better message" # Fix the last commit message
```

### ✍️ Good Commit Messages

**Bad:** `"fix"`, `"changes"`, `"update"`, `"asdfgh"`

**Good:** `"fix: resolve image overflow on mobile screens"`

**Conventional Commits Format (Recommended):**
```
feat:     New feature
fix:      Bug fix
docs:     Documentation changes
style:    Formatting (no logic change)
refactor: Code improvement (not feat or fix)
test:     Adding/updating tests
chore:    Build process or tooling
```

Examples:
```
feat: add dark mode toggle to settings page
fix: resolve null pointer in auth middleware
docs: add API usage examples to README
```

---

### `git log` — View History

```bash
git log                          # Full log
git log --oneline                # One line per commit
git log --oneline --graph --all  # Visual branch graph
git log -5                       # Last 5 commits
git log --author="Manoj"         # Filter by author
git log --stat                   # Show files changed per commit
```

---

### `git diff` — See Changes

```bash
git diff               # Unstaged changes (Working Tree vs Staging)
git diff --staged      # Staged changes (Staging vs last commit)
git diff main feature  # Compare two branches
```

---

### `.gitignore` — Exclude Files

```gitignore
# Dependencies
node_modules/

# Build outputs
dist/
build/

# Environment files (NEVER commit these!)
.env
.env.local

# OS files
.DS_Store
Thumbs.db

# Editor files
.vscode/
.idea/

# Logs
*.log
```

> 💡 Generate `.gitignore` at [gitignore.io](https://www.toptal.com/developers/gitignore)

---

## 05 — Branching & Merging

### Branch Commands

```bash
git branch              # List local branches (* = current)
git branch -a           # List all branches (including remote)
git switch -c feature/login   # Create + switch to new branch ✅
git switch main               # Switch to existing branch
git switch -                  # Switch to previous branch
git branch -d feature/login   # Delete branch (safe)
git branch -D feature/login   # Force delete
git branch -m new-name        # Rename current branch
```

> 💡 **Naming convention:** `feature/user-auth`, `fix/mobile-nav`, `docs/update-readme`

---

### `git merge` — Combine Branches

```bash
git switch main                   # Switch to the branch you merge INTO
git merge feature/login           # Fast-forward merge
git merge --no-ff feature/login   # Always create a merge commit
git merge --abort                 # Cancel a merge in progress
```

**Types of merges:**

| Type | When | Result |
|------|------|--------|
| **Fast-forward** | main has no new commits since branch | Pointer moves forward, no merge commit |
| **Three-way merge** | main has new commits | New merge commit created |

---

### Resolving Merge Conflicts

```bash
# Conflict marker in file:
<<<<<<< HEAD              ← Your branch
<h1>Welcome to My Site</h1>
=======                   ← Divider
<h1>Hello World!</h1>
>>>>>>> feature/login     ← Incoming branch

# Steps to resolve:
# 1. Edit the file — remove markers, keep what you want
# 2. git add <file>
# 3. git commit -m "Resolve merge conflict"
```

VS Code shows **"Accept Current | Accept Incoming | Accept Both"** buttons for easy resolution.

---

## 06 — Remote Repositories

### Connect Local Repo to GitHub

```bash
# Add remote (after creating repo on github.com)
git remote add origin git@github.com:manojneupane/my-project.git

# Push for the first time
git push -u origin main   # -u sets default upstream
# After this, just type: git push
```

### Clone from GitHub

```bash
git clone https://github.com/manojneupane/my-project.git
git clone git@github.com:manojneupane/my-project.git  # SSH (no password)
```

---

### `git push` — Upload to GitHub

```bash
git push                    # Push current branch (if upstream is set)
git push origin main        # Push specific branch
git push -u origin feature  # Push + set upstream
git push --force-with-lease # Force push (safer version of --force)
git push --tags             # Push all tags
```

> ⚠️ Never `--force` push to `main` on a shared repo!

---

### `git pull` — Download from GitHub

```bash
git pull                    # Fetch + merge (shortcut)
git pull origin main        # From specific remote and branch
git pull --rebase           # Fetch + rebase (cleaner history)
```

---

### `git fetch` — Download Without Merging

```bash
git fetch origin   # Download all changes, don't merge yet
git fetch --all    # Fetch from all remotes

# After fetching — see what changed before merging:
git log HEAD..origin/main --oneline
git diff main origin/main
```

> 💡 `fetch` = check what's new | `pull` = download AND apply

---

### Managing Remotes

```bash
git remote -v                              # List remotes
git remote add upstream <url>             # Add a second remote
git remote set-url origin <new-url>       # Change remote URL
git remote remove upstream                # Remove a remote
```

---

## 07 — GitHub Workflow

### 🍴 Forking (Contributing to Open Source)

```bash
# 1. Click "Fork" on GitHub → creates your copy
# 2. Clone YOUR fork
git clone git@github.com:YOU/repo.git
# 3. Add original as "upstream"
git remote add upstream git@github.com:ORIGINAL/repo.git
# 4. Create a branch, make changes, push to YOUR fork
git switch -c fix/typo
git push origin fix/typo
# 5. Create a Pull Request from your fork to the original
# 6. Keep your fork updated:
git fetch upstream && git merge upstream/main
```

---

### 🔃 Pull Requests

A PR is a request to merge your branch into another (usually `main`).

**Good PR checklist:**
- ✅ Clear, descriptive title using Conventional Commits format
- ✅ Description: what changed, why, how to test
- ✅ Screenshots for UI changes
- ✅ Links to related issues: `Closes #42`
- ✅ Reviewer assigned
- ✅ Tests passing

**PR Description Template:**
```markdown
## What changed?
Brief description of the changes.

## Why?
The reason or issue this resolves. `Closes #42`

## How to test?
1. Step one
2. Step two
3. Expected result

## Screenshots
Before | After

## Checklist
- [ ] Tests pass
- [ ] Responsive on mobile
- [ ] No console errors
```

---

### 🐛 Issues

**Bug Report:**
```markdown
## Bug: Login button not working on mobile

**Steps to reproduce:**
1. Open on iPhone (Safari)
2. Go to login page
3. Tap "Login" button

**Expected:** User logged in
**Actual:** Nothing happens

**Environment:** iPhone 14, Safari 16, iOS 16.4
```

**Close issues automatically with keywords in commits/PRs:**
```
closes #28    fixes #15    resolves #42
```

---

### 🤖 GitHub Actions (CI/CD)

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
      - run: npm install
      - run: npm test
      - run: npm run build
```

---

### 🔒 Branch Protection Rules

Go to: **Settings → Branches → Add rule** for `main`:
- ✅ Require pull request before merging
- ✅ Require at least 1 approval
- ✅ Require status checks (CI) to pass
- ✅ No force pushes
- ✅ No direct pushes to main

---

### The Full GitHub Flow

```
1. git switch -c feature/my-feature
2. Make commits
3. git push -u origin feature/my-feature
4. Open Pull Request on GitHub
5. Code review by teammates
6. Fix issues, push more commits
7. CI tests pass ✅ + PR approved ✅
8. Merge PR into main
9. git branch -d feature/my-feature
10. git pull origin main
```

---

## 08 — Undoing Changes

### When to Use What?

| Situation | Command | Safe on Remote? |
|-----------|---------|:---:|
| Discard working tree changes | `git restore <file>` | ✅ |
| Unstage a file | `git restore --staged <file>` | ✅ |
| Fix last commit (not pushed) | `git commit --amend` | ⚠️ |
| Undo commits (keep changes staged) | `git reset --soft HEAD~N` | ⚠️ |
| Undo commits (discard changes) | `git reset --hard HEAD~N` | ⚠️ |
| **Undo a pushed commit safely** | `git revert <hash>` | ✅ |
| Save unfinished work temporarily | `git stash` | ✅ |
| Recover anything lost | `git reflog` | ✅ |

---

### Undoing in Working Tree

```bash
# Discard changes to one file
git restore index.html

# Discard ALL changes (⚠️ permanent!)
git restore .
```

---

### Unstaging

```bash
git restore --staged index.html  # Unstage one file
git restore --staged .           # Unstage everything
```

---

### `git reset` — Move HEAD Backward

```bash
# --soft: undo commit, keep changes STAGED
git reset --soft HEAD~1

# --mixed (default): undo commit, keep changes unstaged
git reset HEAD~1

# --hard: undo commit, DELETE changes (⚠️ permanent!)
git reset --hard HEAD~1

# Go back to a specific commit
git reset --hard 9d1e4f7

# ⚠️ Never reset commits that have been pushed to shared branches!
```

---

### `git revert` — Undo Pushed Commits Safely

```bash
# Creates a NEW commit that undoes the target commit
git revert HEAD           # Undo the last commit
git revert a3f5b2c        # Undo a specific commit
git revert HEAD --no-edit # No editor prompt
```

---

### `git stash` — Save Work Temporarily

```bash
git stash                              # Save all changes
git stash push -m "WIP: login form"   # Save with a description
git stash push --include-untracked -m "includes new files"

git stash list          # See all stashes
git stash pop           # Apply + remove latest stash
git stash apply         # Apply (keep in stash list)
git stash drop stash@{0} # Remove a specific stash
git stash clear         # Remove all stashes
```

**Stash workflow:**
```bash
git stash push -m "WIP: search feature"   # Save your work
git switch main && git pull               # Handle urgent task
# ...fix urgent bug, push it...
git switch feature/search
git stash pop                             # Restore your work!
```

---

### `git reflog` — The Ultimate Safety Net

```bash
# See ALL HEAD movements (including reset --hard)
git reflog

# Recover a "deleted" commit
git reset --hard HEAD@{2}   # Go back 2 HEAD movements
git reset --hard a3f5b2c    # Or by commit hash from reflog
```

> 💡 Almost nothing is truly gone in Git within 90 days. `reflog` can recover it!

---

## 09 — Advanced Git

### `git rebase` — Rewrite History for Clean Log

```bash
# Update feature branch with main's new commits
git switch feature/login
git rebase main

# Interactive rebase — edit last 3 commits
git rebase -i HEAD~3
```

**Interactive rebase commands:**
```
pick   a3f5b2c  Add login HTML      → use as-is
reword 7b1c3d4  Add login CSS       → rename message
squash e9f2a1b  Fix typo            → combine with previous
fixup  d1a2b3c  Another fix         → combine (discard message)
drop   f4e5d6c  Bad commit          → delete entirely
```

**Rebase vs Merge:**
| | Merge | Rebase |
|-|-------|--------|
| History | Branching visible | Linear / clean |
| Safety | Safe on shared | ⚠️ Rewrites history |
| Use for | Merging features | Updating feature with main |

> ⚠️ Never rebase commits that have been pushed to a shared branch.

---

### `git cherry-pick` — Apply a Specific Commit

```bash
git switch main
git cherry-pick e9f2a1b        # Apply one commit
git cherry-pick 9d1e..a3f5    # Apply a range of commits
git cherry-pick --no-commit e9f # Stage only, don't commit
```

---

### Tags — Mark Releases

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"  # Annotated tag (recommended)
git tag v1.0.0                                   # Lightweight tag
git tag                                          # List all tags
git show v1.0.0                                  # Show tag details
git push origin --tags                           # Push ALL tags to GitHub
git tag -d v1.0.0                               # Delete tag locally
git push origin --delete v1.0.0                # Delete tag on GitHub
```

**Semantic Versioning:**
```
v MAJOR . MINOR . PATCH
  Breaking  New    Bug
  changes features fixes
```

---

### Git Aliases — Custom Shortcuts

```bash
git config --global alias.st status
git config --global alias.co switch
git config --global alias.lg "log --oneline --graph --all"
git config --global alias.undo "reset --soft HEAD~1"
git config --global alias.unstage "restore --staged"

# Usage:
git st    # git status
git co main  # git switch main
git lg    # pretty graph
git undo  # undo last commit (keep changes)
```

---

### `git bisect` — Find the Buggy Commit

```bash
git bisect start
git bisect bad                # Current commit has the bug
git bisect good v1.0.0        # This commit was working fine
# Test code → git bisect good or git bisect bad
# Git narrows it down until it finds the exact commit
git bisect reset              # Exit bisect mode
```

---

### GitHub CLI (`gh`)

```bash
gh auth login                                     # Authenticate
gh repo create my-project --public               # Create repo
gh pr create --title "feat: dark mode"           # Create PR
gh pr list                                        # List PRs
gh pr review 15 --approve                        # Approve PR
gh pr merge 15 --squash                          # Merge PR
gh issue list                                     # List issues
gh issue create --title "Bug: login fails"       # Create issue
gh issue close 42                                 # Close issue
```

---

## ⚡ Quick Reference Cheat Sheet

### Setup
```bash
git config --global user.name "Name"
git config --global user.email "email"
git config --global init.defaultBranch main
```

### Basics
```bash
git init                 # New repo
git clone <url>          # Copy remote repo
git status               # What changed?
git add .                # Stage everything
git add <file>           # Stage specific file
git commit -m "message"  # Save snapshot
git log --oneline        # View history
git diff                 # Unstaged changes
git diff --staged        # Staged changes
```

### Branches
```bash
git branch               # List branches
git switch -c <name>     # Create + switch
git switch <name>        # Switch branch
git switch -             # Previous branch
git merge <name>         # Merge into current
git branch -d <name>     # Delete branch
```

### Remote
```bash
git remote add origin <url>  # Connect to GitHub
git push -u origin main      # First push
git push                     # Push (after upstream set)
git pull                     # Fetch + merge
git fetch                    # Download only
git clone <url>              # Clone repo
```

### Undoing
```bash
git restore <file>           # Discard working tree changes
git restore --staged <file>  # Unstage
git commit --amend           # Fix last commit
git reset --soft HEAD~1      # Undo commit (keep staged)
git reset --hard HEAD~1      # Undo commit (delete changes)
git revert <hash>            # Undo pushed commit (safe)
git stash                    # Save work temporarily
git stash pop                # Restore stash
git reflog                   # See all HEAD movements
```

### Advanced
```bash
git rebase main              # Replay commits on main
git rebase -i HEAD~3         # Interactive rebase
git cherry-pick <hash>       # Apply specific commit
git tag -a v1.0.0 -m "..."   # Create release tag
git push origin --tags       # Push all tags
git bisect start/bad/good    # Find buggy commit
```

---

## 💡 Study Tips

1. **Use Git on every project** — even solo work. It builds the habit.
2. **Commit often, commit small** — each commit should do one thing.
3. **Write meaningful commit messages** — your future self will thank you.
4. **Never commit `.env` files** — add them to `.gitignore` immediately.
5. **Practice branching** — always work on feature branches, never directly on `main`.
6. **Contribute to open source** — find issues labelled `good first issue` on GitHub.

---

## 🛠️ Tools

| Tool | Purpose | Link |
|------|---------|------|
| **Git** | Version control | [git-scm.com](https://git-scm.com) |
| **GitHub Desktop** | GUI for Git | [desktop.github.com](https://desktop.github.com) |
| **GitHub CLI** | GitHub from terminal | [cli.github.com](https://cli.github.com) |
| **GitLens** (VS Code) | Enhanced Git UI in VS Code | VS Code Extensions |
| **gitignore.io** | Generate `.gitignore` files | [gitignore.io](https://www.toptal.com/developers/gitignore) |

---

*Happy Coding & Collaborating! 🎉 — Built by Antigravity AI*
