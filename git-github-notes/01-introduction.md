# 01 — Introduction to Git & GitHub

---

## 📌 What is Version Control?

**Version control** is a system that tracks changes to files over time so you can:

- See the **history** of every change ever made
- **Revert** to any previous version if something breaks
- **Collaborate** with other developers without overwriting each other's work
- **Experiment** safely by creating branches

> 💡 **Simple Analogy:** Imagine writing an essay and saving it as `essay_v1.docx`, `essay_v2.docx`, `essay_FINAL.docx`, `essay_FINAL_v2.docx`...
> Git does all of this automatically and much smarter!

---

## 🔧 What is Git?

**Git** is the world's most popular **version control system**.

- Created by **Linus Torvalds** (the creator of Linux) in **2005**.
- Git is **free, open-source, and runs locally** on your computer.
- It tracks changes to your files and allows you to manage your project history.
- Git works **without the internet** — it stores all history on your machine.

### Key Facts:
| Property | Detail |
|---------|--------|
| Created | 2005 by Linus Torvalds |
| Type | Distributed Version Control System (DVCS) |
| Works | Locally on your machine |
| Internet | Not required (except for pushing to GitHub) |
| Cost | 100% free and open source |

---

## 🌐 What is GitHub?

**GitHub** is a **cloud-based hosting platform** for Git repositories.

- GitHub stores your Git repositories **online** so you can access them from anywhere.
- It adds collaboration features: Pull Requests, Issues, Code Reviews, Actions.
- GitHub is where millions of developers share open-source code.
- GitHub ≠ Git. **Git is the tool. GitHub is the website that hosts Git repos.**

> 💡 **Analogy:**
> - **Git** is like Microsoft Word (the software you write with)
> - **GitHub** is like Google Drive (the cloud where you store and share your files)

### Other similar platforms:
| Platform | URL |
|---------|-----|
| **GitHub** | github.com (most popular) |
| **GitLab** | gitlab.com |
| **Bitbucket** | bitbucket.org |

---

## 🔄 Git vs GitHub

| Git | GitHub |
|-----|--------|
| Software on your computer | Website / cloud service |
| Tracks file changes locally | Stores repos online |
| Works offline | Needs internet |
| Command-line tool | Has a web UI, CLI, and desktop app |
| Free & open-source | Free (with paid plans) |
| Created 2005 | Created 2008 |

---

## 🗂️ How Git Works (The Big Picture)

```
Your Computer                    GitHub (Cloud)
─────────────                    ──────────────
                                 
┌─────────────────┐              ┌──────────────────┐
│  Working Tree   │              │  Remote Repo     │
│  (your files)   │              │  (github.com)    │
│                 │  ─── push ──►│                  │
│  Stage/Index    │  ◄── pull ── │                  │
│  (ready to save)│              │                  │
│                 │              │                  │
│  Local Repo     │              │                  │
│  (saved history)│              │                  │
└─────────────────┘              └──────────────────┘
```

The typical workflow:
```
1. Modify files in your Working Tree
      ↓
2. Stage the changes (git add)
      ↓
3. Commit the changes (git commit) → saves to Local Repo
      ↓
4. Push to GitHub (git push) → uploads to Remote Repo
```

---

## 🏗️ Key Terms (Glossary)

| Term | Meaning |
|------|---------|
| **Repository (repo)** | A folder tracked by Git. Contains all your files + their history. |
| **Commit** | A saved snapshot of your files at a specific point in time. |
| **Branch** | A separate line of development. Like a parallel version of your project. |
| **Merge** | Combining changes from one branch into another. |
| **Clone** | Copying a remote repo (from GitHub) to your local machine. |
| **Push** | Uploading your local commits to GitHub. |
| **Pull** | Downloading changes from GitHub to your local machine. |
| **Fork** | Copying someone else's GitHub repo to your own GitHub account. |
| **Pull Request (PR)** | A request to merge your changes into another branch. |
| **Staging Area** | A "waiting room" where you choose what to include in the next commit. |
| **HEAD** | A pointer to the current branch/commit you are on. |
| **Origin** | The default name for the remote repo on GitHub. |

---

## ✅ Key Takeaways

- **Git** = local version control tool. **GitHub** = cloud hosting for Git repos.
- Git tracks the **history** of your project so you can always go back.
- The basic flow: **modify → stage → commit → push**.
- Git lets multiple developers work on the same project without conflict.

---

> ➡️ **Next:** `02-installation-and-setup.md` — Install Git and configure it.
