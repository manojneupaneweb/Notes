# 06 — Remote Repositories

---

## 📌 What is a Remote Repository?

A **remote repository** is a version of your repo hosted on the internet (usually GitHub). It allows you to:

- Back up your code online
- Share code with other developers
- Collaborate on the same project from different machines

```
Your Machine                    GitHub (Remote)
────────────                    ───────────────
Local Repo  ──── git push ────► Remote Repo (origin)
            ◄─── git pull ─────
            ◄─── git fetch ────
```

The default name for your remote is **`origin`** — it's just an alias for the GitHub URL.

---

## 🌐 Connecting to GitHub

### Option A: Create a new repo on GitHub and push local code

```bash
# Step 1: Create the repo on GitHub (github.com → New Repository)

# Step 2: In your local project, add the remote
git remote add origin https://github.com/manojneupane/my-project.git
# or with SSH (if you've set up SSH keys):
git remote add origin git@github.com:manojneupane/my-project.git

# Step 3: Rename default branch to 'main' (if needed)
git branch -M main

# Step 4: Push your code to GitHub
git push -u origin main
# The -u flag sets "origin main" as the default upstream
# From now on you can just type: git push
```

### Option B: Clone an existing repo from GitHub

```bash
# Copy the repo URL from GitHub (Code → Clone)
git clone https://github.com/manojneupane/my-project.git

# Clone into a specific folder name
git clone https://github.com/manojneupane/my-project.git my-folder

# Cloning automatically:
# ✅ Downloads all files
# ✅ Sets up 'origin' remote
# ✅ Checks out the default branch
```

---

## 🔌 Managing Remotes

```bash
# List all remotes
git remote -v

# Output:
# origin  https://github.com/manojneupane/my-project.git (fetch)
# origin  https://github.com/manojneupane/my-project.git (push)

# Add a new remote
git remote add upstream https://github.com/original-author/my-project.git

# Rename a remote
git remote rename origin github

# Remove a remote
git remote remove upstream

# Change a remote's URL (e.g., switch from HTTPS to SSH)
git remote set-url origin git@github.com:manojneupane/my-project.git

# Check remote URL
git remote get-url origin
```

---

## ⬆️ `git push` — Upload to GitHub

```bash
# Push current branch to origin
git push

# Push a specific branch to origin
git push origin main
git push origin feature/login

# Push and set upstream tracking (-u flag)
git push -u origin feature/login
# After this, you can just type: git push

# Force push (DANGEROUS — rewrites remote history)
git push --force
git push --force-with-lease  # Safer: fails if remote has new commits

# Push all branches at once
git push --all origin

# Push tags
git push --tags
```

> ⚠️ **Never force push to `main`!** It can destroy your team's work. Use it only on personal feature branches where you're the only developer.

---

## ⬇️ `git pull` — Download from GitHub

`git pull` = `git fetch` + `git merge` in one command.

```bash
# Pull latest changes from origin/main into your current branch
git pull

# Pull from a specific remote and branch
git pull origin main

# Pull and rebase instead of merge (cleaner history)
git pull --rebase origin main

# Pull all branches
git pull --all
```

---

## 📥 `git fetch` — Download Without Merging

`git fetch` downloads changes from the remote but **does NOT merge them** into your local branch. It's safe to run anytime.

```bash
# Fetch all changes from origin
git fetch origin

# Fetch a specific branch
git fetch origin main

# Fetch from all remotes
git fetch --all

# After fetching, see what changed:
git log HEAD..origin/main --oneline  # Commits on remote not yet in local
git diff main origin/main            # Diff between local and remote
```

> 💡 **`fetch` vs `pull`:**
> - `fetch`: "Let me check what's new on GitHub" (safe, no changes to your code)
> - `pull`: "Download changes and merge them into my branch" (changes your code)
> 
> Use `fetch` first to see what's coming, then decide to `merge` or `rebase`.

---

## 🔗 Tracking Branches

A **tracking branch** is a local branch that "knows about" a remote branch.

```bash
# See tracking info for all branches
git branch -vv

# Output:
# * main          a3f5b2c [origin/main] Add contact form
#   feature/login 9d1e4f7 [origin/feature/login] Add login page

# Set upstream manually
git branch --set-upstream-to=origin/main main

# Unset upstream
git branch --unset-upstream
```

---

## 🔄 Real-World Remote Workflow

### Everyday solo workflow:
```bash
# Start your day — get the latest code
git pull origin main

# Create a feature branch
git switch -c feature/profile-page

# Work on your feature...
git add .
git commit -m "feat: add user profile page"
git add .
git commit -m "feat: add profile picture upload"

# Push your branch to GitHub
git push -u origin feature/profile-page

# When done, create a Pull Request on GitHub
# After PR is merged, clean up:
git switch main
git pull origin main
git branch -d feature/profile-page
```

### Team workflow with multiple developers:
```bash
# Pull regularly to stay up to date
git pull origin main

# If someone pushed to main while you were working:
git fetch origin
git rebase origin/main    # Rebase your work on top of the new commits

# Resolve any conflicts from the rebase
git add .
git rebase --continue

# Push your rebased branch
git push --force-with-lease origin feature/my-feature
```

---

## 📊 Remote Commands Quick Reference

| Command | What it does |
|---------|-------------|
| `git remote -v` | List all remotes with URLs |
| `git remote add origin <url>` | Connect local repo to GitHub |
| `git clone <url>` | Download a repo from GitHub |
| `git push` | Upload current branch to remote |
| `git push -u origin main` | Push and set upstream |
| `git push --force-with-lease` | Force push (safer) |
| `git pull` | Fetch + merge from remote |
| `git pull --rebase` | Fetch + rebase from remote |
| `git fetch` | Download changes (no merge) |
| `git fetch --all` | Fetch from all remotes |

---

> ➡️ **Next:** `07-github-workflow.md` — Forking, Pull Requests, Issues, and team collaboration.
