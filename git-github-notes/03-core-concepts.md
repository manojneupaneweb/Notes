# 03 — Core Concepts

---

## 📌 The Three Areas of Git

Understanding these three areas is the **most important** concept in Git. Every Git operation moves files between them.

```
┌──────────────────────────────────────────────────────────────┐
│                        Your Computer                         │
│                                                              │
│  ┌────────────────┐    git add    ┌────────────────────────┐ │
│  │  Working Tree  │ ───────────► │   Staging Area (Index) │ │
│  │                │              │                        │ │
│  │  (your actual  │ ◄─────────── │  (files ready to       │ │
│  │   files on     │   git restore│   be committed)        │ │
│  │   disk)        │              │                        │ │
│  └────────────────┘              └────────────┬───────────┘ │
│                                               │             │
│                                    git commit │             │
│                                               ▼             │
│                                  ┌────────────────────────┐ │
│                                  │   Local Repository     │ │
│                                  │                        │ │
│                                  │  (saved history of     │ │
│                                  │   all your commits)    │ │
│                                  └────────────────────────┘ │
└──────────────────────────────────────────────────────────────┘
```

### 1. Working Tree (Working Directory)
- The actual files you see in your project folder.
- Any file you create, edit, or delete happens here.
- Git knows about changes, but they are **not yet saved** (not committed).

### 2. Staging Area (Index)
- A "waiting room" or "preparation zone".
- You choose **which changes** you want to include in the next commit.
- Think of it as a **shopping cart** — you pick items before checkout.

### 3. Local Repository (.git folder)
- Where Git stores all committed snapshots (history).
- A hidden `.git` folder inside your project directory.
- `git commit` moves staged changes here permanently.

> 💡 **Why staging?** It lets you commit only SOME of your changes at a time. For example, if you fixed a bug AND added a feature, you can commit them separately.

---

## 📦 What is a Repository?

A **repository (repo)** is a project folder tracked by Git.

```
my-project/              ← This is the Working Tree
├── .git/                ← This is the Local Repository (hidden!)
│   ├── HEAD
│   ├── config
│   ├── objects/         ← All your commits stored here
│   └── refs/            ← Branch and tag references
├── index.html
├── style.css
└── README.md
```

> ⚠️ **Never manually edit or delete the `.git` folder!** Doing so destroys your entire project history.

---

## 📸 What is a Commit?

A **commit** is a **permanent snapshot** of your staged files at a specific moment in time.

Each commit contains:
- **A unique ID (SHA hash):** e.g., `a3f5b2c` — a 40-character fingerprint
- **Author:** Who made the commit (name + email)
- **Timestamp:** When the commit was made
- **Message:** A description of what changed
- **Parent commit:** A pointer to the previous commit

```
Commit History (most recent at top):

  HEAD → main
   │
   ▼
commit a3f5b2c  ← most recent commit
│  Author: Manoj Neupane
│  Date:   Sun May 25 2026
│  Message: "Add contact form to homepage"
│
└── parent → commit 9d1e4f7
              │  Author: Manoj Neupane
              │  Date:   Sat May 24 2026
              │  Message: "Fix navbar mobile bug"
              │
              └── parent → commit 2b8c3a1
                            Message: "Initial commit"
```

> 💡 Git doesn't save full copies of files each time — it saves **differences (diffs)** and reconstructs files from them. This makes repos very space-efficient.

---

## 🌿 What is a Branch?

A **branch** is an independent line of development. It's a lightweight, movable pointer to a commit.

```
main branch:
A ─── B ─── C ─── D    ← main (production code)
              │
              └─── E ─── F   ← feature/login (your new feature)
```

- `main` (or `master`) is the default branch — usually holds stable/production code.
- When you create a new branch, Git creates a new pointer — no files are copied!
- You can switch between branches instantly.
- Changes on one branch **do not affect** other branches.

### Why use branches?
| Reason | Explanation |
|--------|-------------|
| **Safe experiments** | Try things without breaking `main` |
| **Parallel work** | Multiple developers work independently |
| **Feature isolation** | Each feature/bugfix gets its own branch |
| **Code review** | Merge only after review and approval |

---

## 🏷️ What is HEAD?

`HEAD` is a special pointer that tells Git **which branch/commit you are currently on**.

```bash
# HEAD → main → latest commit on main
# When you switch branches:
git switch feature/login
# HEAD → feature/login → latest commit on that branch
```

> 💡 Think of HEAD as the "You are here" pin on a map.

---

## 📊 File Status Lifecycle

Files in Git move through these states:

```
Untracked ──git add──► Staged ──git commit──► Committed (Unmodified)
                                                     │
                         ◄───────────────── edit ────┘
                              (becomes Modified)
                                    │
                         ◄──git add─┘ (back to Staged)
```

| Status | Meaning |
|--------|---------|
| **Untracked** | New file that Git has never seen before |
| **Staged** | Added to staging area, will be in the next commit |
| **Modified** | Tracked file that has been changed but not yet staged |
| **Unmodified** | Tracked file with no new changes since last commit |

---

## ✅ Key Takeaways

- Git has **3 areas**: Working Tree → Staging Area → Local Repository.
- A **commit** is a permanent, timestamped snapshot with a unique ID.
- A **branch** is a pointer to a commit — lightweight and fast to create.
- **HEAD** points to your current location in the repo.
- Files cycle through: **Untracked → Staged → Committed → Modified → Staged...**

---

> ➡️ **Next:** `04-basic-commands.md` — Start using Git commands: init, add, commit, status, log.
