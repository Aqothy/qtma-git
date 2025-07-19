# Git Essentials for Junior Engineers

## Table of Contents

1. [What is Git?](#what-is-git)
2. [Setup & Configuration](#setup--configuration)
3. [Basic Workflow](#basic-workflow)
4. [Branching & Merging](#branching--merging)
5. [Remote Repositories](#remote-repositories)
6. [Utilities & Troubleshooting](#utilities--troubleshooting)
7. [Tools](#tools)

---

## What is Git?
asdlfkjsa

Git is a distributed version control system created by Linus Torvalds in 2005. It:

- Tracks complete history of changes
- Enables multiple people to collaborate
- Allows safe experimentation with branches
- Provides easy rollback to previous versions

### Key Terminology

**Repository**: Project folder with `.git/` directory containing Git data  
**Commit**: Snapshot with unique hash (SHA-1), metadata, and parent links  
**HEAD**: Current commit pointer  
**Working Directory**: Files you're editing  
**Staging Area**: Files prepared for next commit

```
Working Directory → Staging Area → Repository
     (edit)           (add)        (commit)
```

---

## Setup & Configuration

```bash
# Required setup
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Useful configs
git config --global core.editor "code --wait"
git config --global --type bool push.autoSetupRemote true

# Check settings
git config --list
git config user.name

# Initialize repo
git init
git init my-project
```

**Tip**: See [Git config best practices](https://blog.gitbutler.com/how-git-core-devs-configure-git/)

---

## Basic Workflow

Use `git help <command>` for detailed help on any command.

### Status & Changes

```bash
git status                    # Show file states
git status -s                # Short format

git diff                     # Unstaged changes
git diff --staged            # Staged changes
git diff abc123..def456      # Compare commits
git diff main...feature      # Compare branches
```

### Staging & Committing

```bash
git add file.js              # Stage specific file
git add .                    # Stage all changes
git add -A                   # Stage all (including deletions)
git add -p                   # Interactive staging

git commit -m "feat: Add login"              # Commit with message
git commit -am "fix: Typo"                   # Stage + commit tracked files
git commit --amend                           # Modify last commit
```

**Commit Messages**: Use [Conventional Commits](https://www.conventionalcommits.org/) format

### Viewing History

```bash
git log                      # Full history
git log --oneline           # Compact format
git log --graph --all       # Visual branch graph
git log -5                  # Last 5 commits
git log --stat              # Show file changes
git log -p                  # Show diffs
git log --since="2 weeks ago" --author="John"
```

---

## Branching & Merging

Branches enable parallel development without affecting main code.

### Branch Operations

```bash
git branch                   # List branches
git branch feature-login     # Create branch
git checkout feature-login   # Switch branch
git checkout -b feature-login # Create + switch
git switch feature-login     # Modern switch (Git 2.23+)
git switch -c feature-login  # Modern create + switch
```

### Merging

```bash
git checkout main            # Switch to target
git merge feature-login      # Merge branch
git branch -d feature-login  # Delete merged branch
git branch -D feature-login  # Force delete
```

### Merge Conflicts

When conflicts occur:

1. Edit files to resolve conflicts between `<<<<<<< HEAD` and `>>>>>>> branch`
2. Remove conflict markers
3. Stage and commit:

```bash
git add conflicted-file.js
git commit -m "Resolve merge conflict"
```

---

## Remote Repositories

### Clone & Setup

```bash
git clone https://github.com/user/repo.git
git clone https://github.com/user/repo.git my-folder
git clone -b develop https://github.com/user/repo.git

git remote -v                # View remotes
git remote add origin https://github.com/user/repo.git
```

### Sync Operations

```bash
git fetch origin             # Download (no merge)
git pull origin main         # Download + merge
git push origin main         # Upload changes
git push -u origin main      # Set upstream
git push                     # After upstream set
```

**Key Difference**: `fetch` downloads, `pull` downloads + merges

---

## Utilities & Troubleshooting

### Undo Operations

```bash
git restore file.js          # Discard working changes
git restore --staged file.js # Unstage file
git reset --soft HEAD~1      # Undo commit (keep changes)
git reset --hard HEAD~1      # Undo commit (lose changes)
git revert abc123            # Create commit undoing another
```

### Stashing

```bash
git stash                    # Save work temporarily
git stash push -m "WIP"      # Stash with message
git stash list               # List stashes
git stash pop                # Apply + delete latest
git stash apply stash@{1}    # Apply specific stash
```

### Useful Commands

```bash
git blame file.js            # Who changed each line
git show abc123              # Show commit details
git log --grep="bug"         # Search commit messages
```

### .gitignore

```gitignore
node_modules/
*.log
dist/
.env
.DS_Store
.vscode/
```

---

Some other ones that I didn't get time to cover but you can explore yourself since they will be useful:

- Git rebase
- Revert merge commit, rebase interactive
- Cherry pick
- Git reflog
- Git bisect

## Tools

- [Lazygit](https://github.com/jesseduffield/lazygit)
- Vscode Git ui
