# 02 — Installation & Setup

---

## 📥 Installing Git

### Windows:
1. Download from [git-scm.com/download/win](https://git-scm.com/download/win)
2. Run the installer — keep all default settings.
3. During install, choose **"Git Bash"** as the terminal.

### macOS:
```bash
# Option 1: Install via Homebrew (recommended)
brew install git

# Option 2: Install Xcode Command Line Tools
xcode-select --install
```

### Linux (Ubuntu/Debian):
```bash
sudo apt update
sudo apt install git
```

### Verify Installation:
```bash
git --version
# Output: git version 2.43.0
```

---

## ⚙️ First-Time Configuration

After installing Git, you must tell it **who you are**. This info is attached to every commit you make.

```bash
# Set your name (use your real name or GitHub username)
git config --global user.name "Manoj Neupane"

# Set your email (use the same email as your GitHub account!)
git config --global user.email "manoj@example.com"

# Set the default branch name to "main" (modern standard)
git config --global init.defaultBranch main

# Set VS Code as the default editor for Git messages
git config --global core.editor "code --wait"

# Set line endings (Windows only — prevents issues when collaborating)
git config --global core.autocrlf true
```

> ⚠️ **Important:** Use the `--global` flag to apply settings to ALL your repos.
> Without `--global`, the setting only applies to the current repo.

---

## 🔍 Verify Your Configuration

```bash
# See all your global config settings
git config --global --list

# Output:
# user.name=Manoj Neupane
# user.email=manoj@example.com
# init.defaultBranch=main
# core.editor=code --wait

# Check a specific setting
git config user.name
```

---

## 🔐 Setting Up SSH Keys (Connect to GitHub Securely)

SSH keys let you connect to GitHub **without typing your password every time**.

### Step 1: Generate an SSH key
```bash
ssh-keygen -t ed25519 -C "manoj@example.com"
# Press Enter 3 times to accept defaults (no passphrase)
```

### Step 2: Copy the public key
```bash
# Windows
cat ~/.ssh/id_ed25519.pub

# macOS/Linux
cat ~/.ssh/id_ed25519.pub

# Example output:
# ssh-ed25519 AAAA...your_key...AAAA manoj@example.com
```

### Step 3: Add to GitHub
1. Go to [github.com](https://github.com) → **Settings** → **SSH and GPG keys**
2. Click **"New SSH key"**
3. Give it a title (e.g., "My Laptop")
4. Paste the key you copied
5. Click **"Add SSH key"**

### Step 4: Test the connection
```bash
ssh -T git@github.com
# Output: Hi Manoj! You've successfully authenticated...
```

> 💡 After this, you can use SSH URLs (`git@github.com:...`) instead of HTTPS (`https://github.com/...`) to avoid password prompts.

---

## 🖥️ Git in VS Code

VS Code has built-in Git support — you can use the GUI instead of the terminal:

- **Source Control** panel (Ctrl+Shift+G) shows changed files
- Click `+` to stage a file (same as `git add`)
- Type a message and click ✓ to commit (same as `git commit`)
- Click `...` → Push to push to GitHub

> 💡 **Tip:** Install the **GitLens** extension in VS Code for even more powerful Git features.

---

## ✅ Key Takeaways

- Install Git from [git-scm.com](https://git-scm.com).
- Always configure `user.name` and `user.email` after installing.
- Set up SSH keys to connect to GitHub without passwords.
- Use `git config --global --list` to verify your settings anytime.

---

> ➡️ **Next:** `03-core-concepts.md` — Understanding repositories, commits, and the staging area.
