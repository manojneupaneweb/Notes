# 04 — Basic Git Commands

---

## 📌 The Essential Git Workflow

```
1. git init          → Create a new repo
2. (make changes)    → Edit your files
3. git status        → Check what changed
4. git add           → Stage your changes
5. git commit        → Save a snapshot
6. git log           → View history
```

---

## 🏗️ `git init` — Create a New Repository

Initializes a new Git repo in the current folder.

```bash
# Navigate to your project folder first
cd my-project

# Initialize Git
git init

# Output:
# Initialized empty Git repository in /my-project/.git/
```

This creates a hidden `.git/` folder — your local repository.

> ⚠️ **Only run `git init` once** per project. Never run it inside an existing Git repo.

---

## 📋 `git status` — Check the State of Your Repo

The most useful command — shows what's changed and what's staged.

```bash
git status
```

**Common outputs:**

```bash
# All clean — nothing to commit
On branch main
nothing to commit, working tree clean

# New untracked file
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        index.html

# Modified tracked file
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
        modified:   style.css

# File is staged and ready to commit
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   index.html
        modified:   style.css
```

> 💡 **Run `git status` constantly!** It always shows you what to do next.

---

## ➕ `git add` — Stage Changes

Moves files from the Working Tree to the Staging Area.

```bash
# Stage a single file
git add index.html

# Stage multiple files
git add index.html style.css

# Stage all changes in the current directory
git add .

# Stage all tracked (modified) files — not untracked
git add -u

# Stage parts of a file interactively (pick specific lines)
git add -p index.html
```

> 💡 `git add .` stages everything — great for quick saves. For professional work, stage files individually to keep commits focused.

---

## 💾 `git commit` — Save a Snapshot

Takes everything in the Staging Area and saves it as a commit.

```bash
# Commit with a message (the standard way)
git commit -m "Add homepage HTML structure"

# Open your editor to write a longer message
git commit

# Stage all tracked files AND commit in one step (skips staging)
git commit -am "Fix typo in navbar"
# ⚠️ This doesn't add UNTRACKED (new) files — only modified ones

# Amend the last commit (fix message or add forgot staged files)
git commit --amend -m "Corrected commit message"
# ⚠️ Don't amend commits that have been pushed to GitHub!
```

### ✍️ Writing Good Commit Messages

Bad commit messages:
```
"fix"
"changes"
"update code"
"asdfgh"
```

Good commit messages:
```
"Add user authentication form"
"Fix mobile navigation overflow bug"
"Update README with installation steps"
"Remove deprecated API calls from utils.js"
```

#### Conventional Commits Format (Recommended):
```
<type>: <short description>

Types:
  feat:     A new feature
  fix:      A bug fix
  docs:     Documentation only changes
  style:    Formatting (no logic change)
  refactor: Code change that's not a feature or fix
  test:     Adding or updating tests
  chore:    Build process or tooling changes
```

Examples:
```
feat: add dark mode toggle to settings page
fix: resolve image overflow on mobile screens
docs: add API documentation to README
style: format code with Prettier
refactor: extract auth logic into separate module
```

---

## 📜 `git log` — View Commit History

```bash
# Full log — all commits
git log

# Compact one-line format
git log --oneline

# Compact with branch graph
git log --oneline --graph --all

# Last N commits
git log -5

# Commits by a specific author
git log --author="Manoj"

# Commits in a date range
git log --after="2026-01-01" --before="2026-06-01"

# Show which files were changed in each commit
git log --stat

# Show the actual diff in each commit
git log -p
```

**Example output of `git log --oneline --graph --all`:**
```
* a3f5b2c (HEAD → main) Add contact form
* 9d1e4f7 Fix navbar mobile bug
| * e7a2c1d (feature/dark-mode) Add dark mode styles
|/
* 2b8c3a1 Initial commit
```

---

## 🔍 `git diff` — See Exactly What Changed

```bash
# Show unstaged changes (Working Tree vs Staging Area)
git diff

# Show staged changes (Staging Area vs last commit)
git diff --staged
# or
git diff --cached

# Compare two commits
git diff 9d1e4f7 a3f5b2c

# Compare two branches
git diff main feature/login

# Show only names of changed files
git diff --name-only
```

**Example output:**
```diff
diff --git a/style.css b/style.css
--- a/style.css
+++ b/style.css
@@ -15,7 +15,7 @@ body {
-  color: #333;
+  color: #1a1a2e;
   font-size: 16px;
```

Lines starting with `-` are removed. Lines starting with `+` are added.

---

## 👀 `git show` — Inspect a Commit

```bash
# Show the most recent commit's changes
git show

# Show a specific commit
git show a3f5b2c

# Show just the message of a commit
git show a3f5b2c --stat
```

---

## 📁 `git ls-files` — List Tracked Files

```bash
# Show all files tracked by Git
git ls-files

# Show untracked files
git ls-files --others
```

---

## 🙈 `.gitignore` — Excluding Files from Git

A `.gitignore` file tells Git which files/folders to **completely ignore** — never track them.

```bash
# Create a .gitignore file
touch .gitignore
```

**Common `.gitignore` patterns:**

```gitignore
# Dependencies
node_modules/
vendor/

# Build outputs
dist/
build/
*.min.js
*.min.css

# Environment files with secrets
.env
.env.local
.env.production

# OS files
.DS_Store        # macOS
Thumbs.db        # Windows
desktop.ini      # Windows

# Editor files
.vscode/
.idea/
*.swp

# Logs
*.log
logs/

# Cache
.cache/
*.tmp
```

> ⚠️ **Important:** If a file is already tracked by Git, adding it to `.gitignore` won't stop tracking it. You must untrack it first:
> ```bash
> git rm --cached filename
> ```

> 💡 Use [gitignore.io](https://www.toptal.com/developers/gitignore) to auto-generate `.gitignore` files for any language or framework.

---

## 🗂️ Full Example — From Zero to First Commit

```bash
# 1. Create your project folder
mkdir my-website
cd my-website

# 2. Initialize Git
git init

# 3. Create your first file
echo "# My Website" > README.md

# 4. Check what Git sees
git status
# Output: Untracked files: README.md

# 5. Stage the file
git add README.md

# 6. Check status again
git status
# Output: Changes to be committed: new file: README.md

# 7. Commit it
git commit -m "Initial commit: add README"

# 8. View the history
git log --oneline
# Output: a1b2c3d (HEAD → main) Initial commit: add README
```

---

## ✅ Quick Reference Cheat Sheet

| Command | What it does |
|---------|-------------|
| `git init` | Initialize a new repo |
| `git status` | Show current state (changed/staged files) |
| `git add <file>` | Stage a specific file |
| `git add .` | Stage all changes |
| `git commit -m "msg"` | Commit staged changes with a message |
| `git commit -am "msg"` | Stage tracked files + commit |
| `git log` | View full commit history |
| `git log --oneline` | View compact commit history |
| `git diff` | Show unstaged changes |
| `git diff --staged` | Show staged changes |
| `git show <hash>` | Inspect a specific commit |

---

> ➡️ **Next:** `05-branching-and-merging.md` — Work on features independently with branches.
