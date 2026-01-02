# Git & GitHub Quick Reference 🚀

A quick reference guide for the most commonly used Git and GitHub commands and workflows.

## Table of Contents
- [Setup & Configuration](#setup--configuration)
- [Creating Repositories](#creating-repositories)
- [Basic Commands](#basic-commands)
- [Branching](#branching)
- [Remote Operations](#remote-operations)
- [Viewing History](#viewing-history)
- [Undoing Changes](#undoing-changes)
- [Collaboration](#collaboration)
- [Useful Tips](#useful-tips)

## Setup & Configuration

### First Time Git Setup
```bash
# Set your name and email
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Set default branch name to main
git config --global init.defaultBranch main

# Enable color output
git config --global color.ui auto

# View all settings
git config --list

# View specific setting
git config user.name
```

### SSH Key Setup
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Start SSH agent
eval "$(ssh-agent -s)"

# Add key to agent
ssh-add ~/.ssh/id_ed25519

# Copy public key to clipboard (macOS)
pbcopy < ~/.ssh/id_ed25519.pub

# Copy public key to clipboard (Linux)
xclip -sel clip < ~/.ssh/id_ed25519.pub

# Copy public key to clipboard (Windows)
cat ~/.ssh/id_ed25519.pub | clip

# Add to GitHub: Settings → SSH and GPG keys → New SSH key
```

## Creating Repositories

### Create New Local Repository
```bash
# Create directory and initialize
mkdir my-project && cd my-project
git init

# Initialize with specific branch name
git init -b main
```

### Clone Existing Repository
```bash
# Clone via HTTPS
git clone https://github.com/username/repository.git

# Clone via SSH
git clone git@github.com:username/repository.git

# Clone to specific directory
git clone https://github.com/username/repository.git my-folder

# Clone specific branch
git clone -b branch-name https://github.com/username/repository.git
```

### Connect Local Repo to GitHub
```bash
# Add remote
git remote add origin https://github.com/username/repository.git

# Verify remote
git remote -v

# Push to remote
git push -u origin main
```

## Basic Commands

### Check Status
```bash
# Show status
git status

# Short status
git status -s

# Show branch
git branch --show-current
```

### Adding Files
```bash
# Add specific file
git add filename.txt

# Add multiple files
git add file1.txt file2.txt

# Add all files
git add .

# Add all files in directory
git add src/

# Add files by pattern
git add *.js

# Interactive add
git add -i

# Add parts of files (patch mode)
git add -p
```

### Committing
```bash
# Commit with message
git commit -m "Your commit message"

# Commit with detailed message
git commit -m "Title" -m "Detailed description"

# Add and commit in one step
git commit -am "Your message"

# Amend last commit
git commit --amend -m "New message"

# Amend without changing message
git commit --amend --no-edit

# Empty commit (useful for triggering CI)
git commit --allow-empty -m "Trigger CI"
```

### Viewing Differences
```bash
# Show unstaged changes
git diff

# Show staged changes
git diff --staged

# Show changes in specific file
git diff filename.txt

# Compare branches
git diff branch1..branch2

# Compare with specific commit
git diff commit-hash

# Show word-level diff
git diff --word-diff
```

## Branching

### Creating Branches
```bash
# Create new branch
git branch feature-name

# Create and switch to branch
git checkout -b feature-name

# Create and switch (newer syntax)
git switch -c feature-name

# Create branch from specific commit
git branch feature-name commit-hash
```

### Switching Branches
```bash
# Switch to branch (old way)
git checkout branch-name

# Switch to branch (new way)
git switch branch-name

# Switch to previous branch
git switch -

# Create and switch if doesn't exist
git switch -C branch-name
```

### Listing Branches
```bash
# List local branches
git branch

# List with last commit
git branch -v

# List all branches (local + remote)
git branch -a

# List remote branches only
git branch -r

# List merged branches
git branch --merged

# List unmerged branches
git branch --no-merged
```

### Deleting Branches
```bash
# Delete local branch (safe)
git branch -d branch-name

# Force delete local branch
git branch -D branch-name

# Delete remote branch
git push origin --delete branch-name

# Delete multiple branches
git branch -d branch1 branch2 branch3
```

### Renaming Branches
```bash
# Rename current branch
git branch -m new-name

# Rename specific branch
git branch -m old-name new-name

# Update remote
git push origin -u new-name
git push origin --delete old-name
```

## Remote Operations

### Managing Remotes
```bash
# List remotes
git remote

# List remotes with URLs
git remote -v

# Add remote
git remote add origin https://github.com/username/repo.git

# Change remote URL
git remote set-url origin https://github.com/username/repo.git

# Remove remote
git remote remove origin

# Rename remote
git remote rename origin upstream

# Show remote info
git remote show origin
```

### Fetching & Pulling
```bash
# Fetch all remotes
git fetch --all

# Fetch specific remote
git fetch origin

# Fetch and prune deleted branches
git fetch -p

# Pull (fetch + merge)
git pull

# Pull from specific remote/branch
git pull origin main

# Pull with rebase
git pull --rebase

# Pull and prune
git pull --prune
```

### Pushing
```bash
# Push to remote
git push

# Push and set upstream
git push -u origin branch-name

# Push all branches
git push --all

# Push tags
git push --tags

# Force push (dangerous!)
git push --force

# Force push with lease (safer)
git push --force-with-lease

# Push to different remote branch
git push origin local-branch:remote-branch
```

## Viewing History

### Log Commands
```bash
# View commit history
git log

# Compact log
git log --oneline

# Show last N commits
git log -5

# Show with graph
git log --graph --oneline --all

# Show with dates
git log --pretty=format:"%h - %an, %ar : %s"

# Show commits by author
git log --author="John Doe"

# Show commits in date range
git log --since="2 weeks ago"
git log --after="2024-01-01" --before="2024-12-31"

# Show commits that modified specific file
git log -- filename.txt

# Show commits with changes
git log -p

# Show stats
git log --stat
```

### Viewing Commits
```bash
# Show specific commit
git show commit-hash

# Show most recent commit
git show HEAD

# Show specific file in commit
git show commit-hash:path/to/file.txt

# Show files changed in commit
git show --name-only commit-hash
```

### Searching History
```bash
# Search for string in code
git log -S "search-string"

# Search in commit messages
git log --grep="search-term"

# Show who changed each line in file
git blame filename.txt

# Show blame for specific lines
git blame -L 10,20 filename.txt
```

## Undoing Changes

### Discard Changes
```bash
# Discard changes in working directory
git restore filename.txt

# Discard all changes (old way)
git checkout -- filename.txt

# Discard all unstaged changes
git restore .

# Discard staged changes
git restore --staged filename.txt

# Discard all staged changes
git restore --staged .
```

### Reset
```bash
# Unstage files (keep changes)
git reset filename.txt

# Reset to specific commit (keep changes)
git reset commit-hash

# Reset and discard changes (dangerous!)
git reset --hard HEAD

# Reset to specific commit and discard
git reset --hard commit-hash

# Reset to remote state
git reset --hard origin/main
```

### Revert
```bash
# Revert specific commit (creates new commit)
git revert commit-hash

# Revert without committing
git revert -n commit-hash

# Revert multiple commits
git revert commit1..commit2

# Revert merge commit
git revert -m 1 commit-hash
```

### Clean
```bash
# Show what would be deleted
git clean -n

# Remove untracked files
git clean -f

# Remove untracked files and directories
git clean -fd

# Remove ignored files too
git clean -fdx
```

## Collaboration

### Forking Workflow
```bash
# 1. Fork repo on GitHub

# 2. Clone your fork
git clone https://github.com/yourusername/repo.git
cd repo

# 3. Add upstream remote
git remote add upstream https://github.com/originalowner/repo.git

# 4. Create feature branch
git checkout -b feature-branch

# 5. Make changes and commit
git add .
git commit -m "Add feature"

# 6. Update from upstream
git fetch upstream
git rebase upstream/main

# 7. Push to your fork
git push origin feature-branch

# 8. Create Pull Request on GitHub
```

### Syncing Fork
```bash
# Fetch upstream changes
git fetch upstream

# Merge upstream main to local main
git checkout main
git merge upstream/main

# Or rebase
git rebase upstream/main

# Push to your fork
git push origin main
```

### Pull Request Workflow
```bash
# Update your branch with main
git checkout feature-branch
git merge main

# Or rebase your branch on main
git rebase main

# Force push if rebased
git push --force-with-lease origin feature-branch

# After PR is merged, clean up
git checkout main
git pull origin main
git branch -d feature-branch
git push origin --delete feature-branch
```

## Useful Tips

### Stashing
```bash
# Stash changes
git stash

# Stash with message
git stash save "Work in progress"

# List stashes
git stash list

# Apply most recent stash
git stash apply

# Apply and remove stash
git stash pop

# Apply specific stash
git stash apply stash@{2}

# Drop stash
git stash drop stash@{0}

# Clear all stashes
git stash clear

# Stash untracked files too
git stash -u
```

### Tags
```bash
# Create lightweight tag
git tag v1.0.0

# Create annotated tag
git tag -a v1.0.0 -m "Version 1.0.0"

# List tags
git tag

# List tags with pattern
git tag -l "v1.*"

# Show tag details
git show v1.0.0

# Push tag to remote
git push origin v1.0.0

# Push all tags
git push --tags

# Delete local tag
git tag -d v1.0.0

# Delete remote tag
git push origin --delete v1.0.0

# Checkout tag
git checkout v1.0.0
```

### Cherry-pick
```bash
# Apply specific commit to current branch
git cherry-pick commit-hash

# Cherry-pick without committing
git cherry-pick -n commit-hash

# Cherry-pick range of commits
git cherry-pick commit1..commit2

# Continue after resolving conflicts
git cherry-pick --continue

# Abort cherry-pick
git cherry-pick --abort
```

### Rebase
```bash
# Rebase on main
git rebase main

# Interactive rebase (last 5 commits)
git rebase -i HEAD~5

# Continue after resolving conflicts
git rebase --continue

# Skip commit
git rebase --skip

# Abort rebase
git rebase --abort

# Rebase onto different branch
git rebase --onto new-base old-base branch
```

### Aliases
```bash
# Create alias
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status

# Use alias
git co main
git st

# Useful aliases to add
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual 'log --graph --oneline --all'
git config --global alias.amend 'commit --amend --no-edit'
```

### .gitignore Patterns
```bash
# Ignore specific file
secrets.txt

# Ignore all files with extension
*.log

# Ignore directory
node_modules/

# Ignore all in directory except specific file
build/*
!build/.gitkeep

# Ignore pattern
**/*.temp

# Comments
# This is a comment
```

### Useful Combinations
```bash
# Stage and commit all changes
git commit -am "Message"

# Pull and rebase
git pull --rebase origin main

# Fetch and reset to remote
git fetch origin && git reset --hard origin/main

# Create branch from tag
git checkout -b branch-name tag-name

# View branches merged into main
git branch --merged main

# Delete all local branches except main
git branch | grep -v "main" | xargs git branch -D

# Find commits that added/removed text
git log -S "search-text" -p

# Show file at specific revision
git show HEAD~3:path/to/file.txt

# List files in last commit
git diff --name-only HEAD HEAD~1
```

## GitHub CLI (gh)

```bash
# Install GitHub CLI
# macOS: brew install gh
# Linux: See https://cli.github.com/manual/installation
# Windows: scoop install gh

# Authenticate
gh auth login

# Create repo
gh repo create my-repo --public

# Clone repo
gh repo clone username/repo

# Create PR
gh pr create --title "Title" --body "Description"

# List PRs
gh pr list

# View PR
gh pr view 123

# Checkout PR
gh pr checkout 123

# Merge PR
gh pr merge 123

# Create issue
gh issue create --title "Bug" --body "Description"

# View issues
gh issue list
```

## Emergency Commands

### Recover Lost Commits
```bash
# View reflog
git reflog

# Recover commit
git checkout commit-hash

# Create branch from recovered commit
git checkout -b recovered-branch
```

### Fix Detached HEAD
```bash
# Create branch from current state
git checkout -b temp-branch

# Or checkout existing branch
git checkout main
```

### Abort Operations
```bash
# Abort merge
git merge --abort

# Abort rebase
git rebase --abort

# Abort cherry-pick
git cherry-pick --abort
```

---

## 📚 Additional Resources

- [Official Git Documentation](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com/)
- [Interactive Git Cheatsheet](https://ndpsoftware.com/git-cheatsheet.html)
- [Git Flight Rules](https://github.com/k88hudson/git-flight-rules)

**Pro Tip**: Use `git help <command>` or `man git-<command>` for detailed information about any Git command!

---

*Keep this guide handy for quick reference. Practice makes perfect!* 🎯
