# Git Basics

## Creating a Repository

To turn any folder into a Git repository:

```bash
git init
```

This command converts a normal folder into a **Git repository**.

---

# What Happens When You Run `git init`

Git creates a hidden `.git` folder inside your project.

```
my-project/
├── .git/          ← Git's internal database
│   ├── objects/   ← Stores commits and file snapshots
│   ├── refs/      ← Stores branch references
│   └── HEAD       ← Points to the current branch
├── index.html
├── style.css
└── app.js
```

### What `.git` Contains

| Component | Purpose |
|---|---|
| objects | Stores commits and snapshots |
| refs | Tracks branches and tags |
| HEAD | Points to the current branch |

The `.git` folder is basically **Git’s brain**.

---

# Working Directory

The **working directory** is your project folder **excluding the `.git` folder**.

This is where you:

- Write code
- Edit files
- Delete files

Git monitors this directory to detect **changes since the last commit**.

---

# File States in Git

Files in Git can be in these states.

| State | Meaning |
|---|---|
| Untracked | Git doesn't know about the file yet |
| Tracked | Git is monitoring the file |
| Modified | File changed since last commit |
| Staged | File ready for next commit |

---

# The Three Areas of Git

Git organizes your work into three areas.

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│ Working         │     │ Staging         │     │ Repository      │
│ Directory       │ ──► │ Area            │ ──► │ (Commits)       │
│                 │     │                 │     │                 │
│ Edit files      │     │ Prepare files   │     │ Save snapshot   │
│ here            │     │ for commit      │     │ permanently     │
└─────────────────┘     └─────────────────┘     └─────────────────┘
        │                       │                       │
     git add                git commit              git log
```

### Workflow

1. Edit files in **Working Directory**
2. Stage files using **git add**
3. Save snapshot using **git commit**

---

# Commits

A **commit** is a snapshot of your project at a specific moment.

Think of it like **saving a version of your project**.

---

## Creating a Commit

```bash
git commit -m "Your message here"
```

Example:

```bash
git commit -m "Add user authentication"
```

The `-m` flag lets you add a **description of the changes**.

---

# Commit Hash

Every commit has a **unique SHA hash**.

Example:

```
a1b2c3d4e5f6789...
```

Usually only the **first 7 characters** are used.

```
a1b2c3d
```

---

# What a Commit Contains

| Component | Description |
|---|---|
| Tree | Snapshot of all files |
| Parent | Previous commit |
| Author | Who created the commit |
| Message | Description of change |
| Timestamp | When commit was made |
| Hash | Unique commit identifier |

---

# Viewing Commit History

To see all commits:

```bash
git log
```

This shows:

- commit hash
- author
- date
- commit message

---

## Compact History

```bash
git log --oneline
```

Example:

```
a1b2c3d Add authentication feature
f4e5d6c Create project structure
```

---

# Understanding HEAD

Example log entry:

```
commit a1b2c3d (HEAD -> main)
Author: You
Date: Mon Jan 15

Add authentication feature
```

Meaning:

```
HEAD is currently pointing to the main branch
```

---

# Comparing Changes with Diff

### Changes in working directory

```bash
git diff
```

### Changes staged for commit

```bash
git diff --staged
```

### Compare two commits

```bash
git diff a1b2c3d f4e5d6c
```

---

# Diff Output

```
- line removed
+ line added
  unchanged line
```

| Symbol | Meaning |
|---|---|
| - | Removed line |
| + | Added line |
| space | Context line |

---

# Undoing Changes in Git

## Quick Cheat Sheet

| Situation | Command |
|---|---|
| Undo `git add .` | `git restore --staged .` |
| Undo last commit (keep changes staged) | `git reset --soft HEAD~1` |
| Undo last commit (keep changes unstaged) | `git reset --mixed HEAD~1` |
| Delete commit and changes | `git reset --hard HEAD~1` |
| Undo pushed commit safely | `git revert HEAD` |
| Remove pushed commit completely | `git reset --hard HEAD~1` + `git push --force` |

---

# Git Restore vs Reset

```
Working Directory     Staging Area        Repository
      │                    │                  │
      │◄── restore ────────┤                  │
      │                    │◄── restore ──────┤
      │                    │    --staged      │
      │◄───────────────────┼── reset --hard ──┤
```

---

# When to Use Each Command

| Command | When to Use |
|---|---|
| git restore | Restore a modified file |
| git restore --staged | Unstage a file |
| git reset --soft | Undo commit but keep staged changes |
| git reset --hard | Completely revert to previous commit (dangerous) |
| git revert | Safely undo a commit already pushed |

---

# Common Git Workflow

```
Edit files
   ↓
git add .
   ↓
git commit -m "message"
   ↓
git push
```

---

# Most Used Git Commands

```bash
git init
git status
git add .
git commit -m "message"
git log --oneline
git diff
git restore
git reset
git push
git pull
```

///////////////////

# Branching 
| Scenario                          | Git Command                     |
| --------------------------------- | ------------------------------- |
| See current branch                | `git branch`                    |
| See all branches (local)          | `git branch`                    |
| See remote branches               | `git branch -r`                 |
| See all branches (local + remote) | `git branch -a`                 |
| Create a new branch               | `git branch feature-login`      |
| Switch to another branch          | `git checkout feature-login`    |
| Create + switch branch (modern)   | `git checkout -b feature-login` |
| Modern switch command             | `git switch feature-login`      |
| Create + switch using new syntax  | `git switch -c feature-login`   |
| Delete a branch                   | `git branch -d feature-login`   |
| Force delete branch               | `git branch -D feature-login`   |

# example
| Situation              | Command                               |
| ---------------------- | ------------------------------------- |
| Start from main branch | `git checkout main`                   |
| Create feature branch  | `git checkout -b login-feature`       |
| Work on code           | *(edit files)*                        |
| Stage changes          | `git add .`                           |
| Commit changes         | `git commit -m "login feature added"` |
| Go back to main        | `git checkout main`                   |
| Merge feature branch   | `git merge login-feature`             |
| Situation              | Command                            |
| ---------------------- | ---------------------------------- |
| Push branch first time | `git push -u origin login-feature` |
| Push updates later     | `git push`                         |

///// This shows branch history visually.
git log --oneline --graph --all

| Situation              | Command                           |
| ---------------------- | --------------------------------- |
| Rename current branch  | `git branch -m new-name`          |
| Rename specific branch | `git branch -m old-name new-name` |

# example 2 MERGING

| Scenario        | Command                       |
| --------------- | ----------------------------- |
| Create branch   | `git switch -c login-feature` |
| Work and commit | `git add .`                   |
|                 | `git commit -m "login added"` |
| Merge into main | `git checkout main`           |
|                 | `git merge login-feature`     |


# Fresh Empty Repo → Start Coding → Push (ONLY SCENARIOS + CMDS)
| Scenario              | Command                            |
| --------------------- | ---------------------------------- |
| Initialize git repo   | `git init`                         |
| Check repo status     | `git status`                       |
| Add all files         | `git add .`                        |
| Commit code           | `git commit -m "first commit"`     |
| Add remote repo       | `git remote add origin <repo-url>` |
| Rename branch to main | `git branch -M main`               |
| Push code to remote   | `git push -u origin main`          |


#Clone Existing Repo → Start Coding

| Scenario               | Command                         |
| ---------------------- | ------------------------------- |
| Clone repo from GitHub | `git clone <repo-url>`          |
| Go into project folder | `cd repo-name`                  |
| Check branches         | `git branch`                    |
| Start coding           | *(edit files)*                  |
| Add changes            | `git add .`                     |
| Commit changes         | `git commit -m "feature added"` |
| Push changes           | `git push`                      |

# Feature Branch Workflow (Used in Companies)

| Scenario              | Command                            |
| --------------------- | ---------------------------------- |
| Create feature branch | `git switch -c login-feature`      |
| Code changes          | *(edit files)*                     |
| Stage changes         | `git add .`                        |
| Commit changes        | `git commit -m "login feature"`    |
| Push branch           | `git push -u origin login-feature` |
| Merge later           | `git switch main`                  |
|                       | `git merge login-feature`          |


# UPDATE UR BRANCH WITH LATEST MAIN

| Scenario                 | Command                    |
| ------------------------ | -------------------------- |
| Get latest remote code   | `git fetch origin`         |
| Switch to feature branch | `git switch login-feature` |
| Rebase with main         | `git rebase origin/main`   |



