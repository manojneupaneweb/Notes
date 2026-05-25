# 07 — GitHub Workflow

---

## 📌 What is the GitHub Workflow?

The **GitHub Workflow** (also called Feature Branch Workflow or GitHub Flow) is the standard process teams use to collaborate on code safely.

```
main (protected)
  │
  ├── feature/login          → Developer A
  ├── feature/dark-mode      → Developer B
  └── fix/mobile-nav-bug     → Developer C
          │
          └── Pull Request
                │
                ├── Code Review (teammates review)
                ├── CI/CD Tests (automated)
                └── Merge into main ✅
```

---

## 🍴 Forking

**Forking** creates a personal copy of someone else's repository on your GitHub account. Used for:

- Contributing to open-source projects
- Using someone's repo as a starting point for your own project

```
Original Repo (owner's GitHub)
    │
    └── Fork → Your GitHub Account
                    │
                    └── Clone → Your Computer
```

### Fork Workflow:
```bash
# Step 1: Click "Fork" on the original repo on GitHub
#         This creates:  github.com/YOUR-USERNAME/repo-name

# Step 2: Clone YOUR fork to your machine
git clone git@github.com:YOUR-USERNAME/repo-name.git
cd repo-name

# Step 3: Add the original repo as "upstream"
git remote add upstream git@github.com:ORIGINAL-AUTHOR/repo-name.git

# Verify remotes:
git remote -v
# origin    git@github.com:YOUR-USERNAME/repo-name.git (fetch)
# origin    git@github.com:YOUR-USERNAME/repo-name.git (push)
# upstream  git@github.com:ORIGINAL-AUTHOR/repo-name.git (fetch)
# upstream  git@github.com:ORIGINAL-AUTHOR/repo-name.git (push)

# Step 4: Create a branch and make changes
git switch -c fix/typo-in-readme

# Step 5: Push to YOUR fork
git push origin fix/typo-in-readme

# Step 6: Create a Pull Request from YOUR fork to the original repo

# Step 7: Keep your fork up to date with the original
git fetch upstream
git switch main
git merge upstream/main
git push origin main
```

---

## 🔃 Pull Requests (PRs)

A **Pull Request** is a request to merge changes from your branch into another branch (usually `main`). It's the core of code collaboration on GitHub.

### Creating a Pull Request:

```bash
# 1. Push your feature branch to GitHub
git push -u origin feature/user-profile

# 2. GitHub will show a banner: "Compare & pull request" — click it
#    Or go to: Repo → Pull Requests → New Pull Request
```

### A good Pull Request includes:
1. **A clear title:** `feat: add user profile page`
2. **A description explaining:**
   - What was changed and why
   - Screenshots (for UI changes)
   - How to test it
3. **Links to related Issues:** `Closes #42`
4. **Labels:** `bug`, `enhancement`, `documentation`
5. **Reviewers assigned**

### PR Description Template:
```markdown
## What changed?
Added a user profile page with avatar upload, bio, and social links.

## Why?
Resolves #42 — users requested profile customization.

## How to test?
1. Log in to the app
2. Navigate to /profile
3. Try editing the bio and uploading an avatar

## Screenshots
[Before] | [After]

## Checklist
- [x] Tests pass
- [x] No console errors
- [x] Responsive on mobile
```

---

## 👀 Code Review

Code review is the process of teammates reading and checking each other's code before it gets merged.

### As a Reviewer, look for:
- **Correctness:** Does the code do what it claims?
- **Bugs:** Are there edge cases not handled?
- **Readability:** Is the code easy to understand?
- **Performance:** Are there any obvious inefficiencies?
- **Security:** Any potential vulnerabilities?
- **Standards:** Does it follow the project's code style?

### Leaving Review Comments:
On GitHub you can:
- **Comment** — Leave a note without approving or rejecting
- **Approve** ✅ — Looks good, ready to merge
- **Request Changes** ❌ — Needs fixes before merging

```markdown
# Good review comment examples:

"This function is doing two things — consider splitting it into
`fetchUser()` and `renderUserCard()` for better separation of concerns."

"This will throw an error if `data.user` is null. Consider adding
a null check: `if (!data.user) return;`"

"Love the approach here! One small suggestion: using `const` instead
of `let` would make it clearer this value doesn't change."
```

---

## 🐛 Issues

**Issues** are GitHub's built-in task tracker. Use them to report bugs, request features, or track work.

### Creating a Good Issue:

**Bug Report:**
```markdown
## Bug: Login button not working on mobile

**Steps to reproduce:**
1. Open the site on a phone (Chrome/iOS)
2. Go to the login page
3. Tap the "Login" button

**Expected behavior:** User gets logged in

**Actual behavior:** Nothing happens — button appears unresponsive

**Environment:**
- Device: iPhone 14
- Browser: Safari 16
- OS: iOS 16.4

**Screenshots:** [attach screenshot here]
```

**Feature Request:**
```markdown
## Feature: Add dark mode

**Is your feature request related to a problem?**
The site is too bright at night.

**Describe the solution you'd like:**
A toggle button in the navbar to switch between light and dark themes.
The preference should be saved in localStorage.

**Additional context:**
Other sites like GitHub and VS Code already do this.
```

### Closing Issues with Commits/PRs:
```bash
# In your commit message or PR description, use:
git commit -m "fix: resolve login button touch event — closes #28"

# Keywords that auto-close issues on merge:
# closes, fixes, resolves
# Example: "fixes #42", "closes #15, #16"
```

---

## 🏷️ Labels, Milestones & Projects

### Labels (tag issues and PRs):
| Label | Meaning |
|-------|---------|
| `bug` | Something isn't working |
| `enhancement` | New feature or request |
| `documentation` | Improvements to docs |
| `good first issue` | Good for newcomers |
| `help wanted` | Extra attention needed |
| `wontfix` | Won't be worked on |
| `duplicate` | Already reported |

### Milestones:
Group issues/PRs under a goal with a deadline.
- Example: **"v2.0 Launch"** milestone with all related issues

### Projects (GitHub Project Boards):
Kanban-style boards to track work visually:
```
To Do → In Progress → Review → Done
```

---

## 🤖 GitHub Actions (CI/CD Basics)

**GitHub Actions** automates tasks like testing and deployment.

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

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test

      - name: Build project
        run: npm run build
```

This runs automatically on every push and PR — showing ✅ or ❌ on each PR.

---

## 🔒 Branch Protection Rules

Set up in GitHub: **Settings → Branches → Add rule**

Common rules for `main`:
- ✅ Require pull request before merging
- ✅ Require at least 1 approval
- ✅ Require status checks to pass (CI tests)
- ✅ Do not allow force pushes
- ✅ Do not allow direct pushes to main

This ensures code only gets to `main` through reviewed, tested PRs.

---

## 📊 GitHub Workflow — The Full Picture

```
1. git switch -c feature/my-feature     ← Create branch
2. (make commits)                        ← Do the work
3. git push -u origin feature/my-feature ← Push to GitHub
4. Open Pull Request on GitHub           ← Request review
5. Teammates review and comment          ← Code review
6. Fix issues, push more commits         ← Iterate
7. CI tests pass ✅                      ← Automated checks
8. PR approved ✅                        ← Human approval
9. Merge PR into main                    ← Code ships!
10. git branch -d feature/my-feature     ← Clean up locally
11. git pull origin main                 ← Stay up to date
```

---

> ➡️ **Next:** `08-undoing-changes.md` — How to fix mistakes and undo changes in Git.
