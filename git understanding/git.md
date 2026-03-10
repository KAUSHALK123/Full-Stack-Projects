# Creating a Repository
To turn any folder into a Git repository, you use:

git init
That's it! This single command transforms an ordinary folder into a version-controlled project.

What Happens When You Run git init?
When you initialize a repository, Git creates a hidden .git folder inside your project. This folder contains:

All your project history - every snapshot you've ever taken
Branch information - which timelines exist
Configuration - settings for this repository
my-project/
├── .git/          ← Git's brain (hidden folder)
│   ├── objects/   ← Stores all your snapshots
│   ├── refs/      ← Tracks branches
│   └── HEAD       ← Points to current branch
├── index.html
├── style.css
└── app.js
The Working Directory
Your working directory is everything in your project folder except the .git folder. This is where you actually edit files.

Git constantly watches your working directory to see what's changed since your last snapshot.

Repository States
Files in a Git repository can be in one of these states:

State	Meaning
Untracked	Git doesn't know about this file yet
Tracked	Git is watching this file for changes
Modified	You've changed the file since last snapshot
Staged	Ready to be included in next snapshot


////
The Three Areas of Git
Git organizes your work into three areas:
                                                                    
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│    Working      │     │    Staging      │     │   Repository    │
│   Directory     │ ──► │     Area        │ ──► │   (Commits)     │
│                 │     │                 │     │                 │
│  Edit files     │     │  Prepare files  │     │  Save snapshot  │
│  here           │     │  for commit     │     │  permanently    │
└─────────────────┘     └─────────────────┘     └─────────────────┘
        │                       │                       │
     git add                git commit              git log
    

/////A commit is a snapshot of your project at a specific moment in time. It's like taking a photo and labeling it so you can find it later.

Creating a Commit
Once you've staged your files, create a commit with:

git commit -m "Your message here"
The -m flag lets you add a message describing what changed.

Understanding Commit Hashes
Every commit gets a unique identifier called a SHA hash:

a1b2c3d4e5f6789...
This 40-character string is like a fingerprint - no two commits will ever have the same hash. Usually, you only need the first 7 characters to identify a commit.

What's Inside a Commit?
Each commit stores:

Component	Description
Tree	Snapshot of all your files
Parent	Link to the previous commit
Author	Who made the commit
Message	Your description
Timestamp	When it was created
Hash	Unique identifier

/////
# Viewing Commit History
To see all your commits:

git log
This shows each commit with:

The full commit hash
Author name and email
Date and time
Commit message
Compact View
For a shorter view, use:

git log --oneline
This shows one commit per line with just the short hash and message.

Reading the Log
commit a1b2c3d (HEAD -> main)
Author: You <you@email.com>
Date:   Mon Jan 15 10:30:00 2024

    Add user authentication feature

commit f4e5d6c
Author: You <you@email.com>
Date:   Sun Jan 14 15:20:00 2024

    Create initial project structure
The HEAD -> main tells you which commit you're currently on.

Comparing Changes with Diff
To see what changed between versions:

# Changes in working directory (not yet staged)
git diff

# Changes that are staged
git diff --staged

# Compare two commits
git diff a1b2c3d f4e5d6c
Understanding Diff Output
- This line was removed
+ This line was added
  This line is unchanged
Red (-) lines were removed
Green (+) lines were added
White lines provide context

///////////////
# RESTORE AND UNDO ING THINGS / FILES

🔁 Quick cheat sheet
Situation	Command
Undo git add .	git restore --staged .
Undo last commit (keep changes staged)	git reset --soft HEAD~1
Undo last commit (keep changes unstaged)	git reset --mixed HEAD~1
Delete commit + code	git reset --hard HEAD~1
Undo pushed commit safely	git revert HEAD
Remove pushed commit completely	git reset --hard HEAD~1 + git push --force

Working Directory     Staging Area        Repository
      │                    │                  │
      │◄── restore ────────┤                  │
      │                    │◄── restore ──────┤
      │                    │    --staged      │
      │◄───────────────────┼── reset --hard ──┤



When to Use Each
git restore - "I messed up this file, bring it back"
git restore --staged - "I didn't mean to stage this"
git reset --soft - "I want to redo my last commit"
git reset --hard - "Delete everything and go back" (careful!)

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


