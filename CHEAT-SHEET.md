# Git & GitHub Cheat Sheet

A quick reference for essential Git and GitHub commands.

## Configuration

```bash
# Set your name
git config --global user.name "Your Name"

# Set your email
git config --global user.email "your.email@example.com"

# Check your settings
git config --list
```

## Creating Repositories

```bash
# Initialize a new repository
git init

# Clone an existing repository
git clone <url>

# Clone to a specific folder
git clone <url> <folder-name>
```

## Basic Commands

```bash
# Check status of files
git status

# Add file to staging
git add <file>

# Add all files to staging
git add .

# Commit staged changes
git commit -m "Commit message"

# Add and commit in one command
git commit -am "Commit message"

# Push to remote repository
git push origin <branch>

# Pull from remote repository
git pull origin <branch>
```

## Branching

```bash
# List all branches
git branch

# Create a new branch
git branch <branch-name>

# Switch to a branch
git checkout <branch-name>

# Create and switch to new branch
git checkout -b <branch-name>

# Delete a branch
git branch -d <branch-name>

# Force delete a branch
git branch -D <branch-name>

# Merge branch into current branch
git merge <branch-name>
```

## Viewing Changes

```bash
# View commit history
git log

# View compact history
git log --oneline

# View history with graph
git log --graph --oneline --all

# View changes (not staged)
git diff

# View changes (staged)
git diff --staged

# View changes for a specific file
git diff <file>
```

## Undoing Changes

```bash
# Discard changes in working directory
git checkout -- <file>

# Unstage a file
git reset HEAD <file>

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Revert a commit (create new commit)
git revert <commit-hash>
```

## Remote Repositories

```bash
# List remote repositories
git remote -v

# Add remote repository
git remote add origin <url>

# Change remote URL
git remote set-url origin <new-url>

# Remove remote
git remote remove origin

# Fetch changes from remote
git fetch origin

# Pull changes from remote
git pull origin <branch>

# Push to remote
git push origin <branch>

# Push all branches
git push --all origin
```

## Stashing

```bash
# Stash current changes
git stash

# Stash with a message
git stash save "message"

# List all stashes
git stash list

# Apply most recent stash
git stash apply

# Apply specific stash
git stash apply stash@{n}

# Apply and remove stash
git stash pop

# Delete a stash
git stash drop stash@{n}

# Clear all stashes
git stash clear
```

## Tags

```bash
# List all tags
git tag

# Create a tag
git tag <tag-name>

# Create annotated tag
git tag -a <tag-name> -m "message"

# Push tags to remote
git push origin --tags

# Delete a tag
git tag -d <tag-name>

# Delete remote tag
git push origin :refs/tags/<tag-name>
```

## GitHub CLI (gh)

```bash
# Login to GitHub
gh auth login

# Create a repository
gh repo create

# Clone a repository
gh repo clone <repo>

# View repository
gh repo view

# Create a pull request
gh pr create

# List pull requests
gh pr list

# View a pull request
gh pr view <number>

# Merge a pull request
gh pr merge <number>

# Create an issue
gh issue create

# List issues
gh issue list

# View an issue
gh issue view <number>
```

## Useful Aliases

Add these to your `.gitconfig` or set with `git config --global alias.<name> '<command>'`:

```bash
# Short status
git config --global alias.st status

# Short log
git config --global alias.lg "log --oneline --graph --all"

# Last commit
git config --global alias.last "log -1 HEAD"

# Unstage
git config --global alias.unstage "reset HEAD --"

# Amend last commit
git config --global alias.amend "commit --amend"
```

## Common Workflows

### Starting a New Feature

```bash
git checkout main
git pull origin main
git checkout -b feature/new-feature
# ... make changes ...
git add .
git commit -m "Add new feature"
git push origin feature/new-feature
# Create pull request on GitHub
```

### Fixing a Bug

```bash
git checkout main
git pull origin main
git checkout -b fix/bug-description
# ... fix bug ...
git add .
git commit -m "Fix: bug description"
git push origin fix/bug-description
# Create pull request on GitHub
```

### Updating Your Branch

```bash
git checkout main
git pull origin main
git checkout your-branch
git merge main
# Resolve any conflicts
git push origin your-branch
```

## .gitignore Patterns

```
# Comments start with #

# Ignore specific file
file.txt

# Ignore all files with extension
*.log

# Ignore directory
node_modules/

# Ignore files in directory
build/*

# But keep specific file
!build/.gitkeep

# Ignore files in all directories
**/*.temp
```

## Commit Message Best Practices

### Format
```
Type: Short description (50 chars or less)

Longer description if needed (wrap at 72 characters).
Explain what and why, not how.

- Bullet points are okay
- Use present tense: "Add feature" not "Added feature"
```

### Types
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks

### Examples
```
feat: Add user authentication
fix: Resolve login validation error
docs: Update installation instructions
style: Format code according to style guide
refactor: Simplify data processing logic
test: Add unit tests for user service
chore: Update dependencies
```

## Tips & Tricks

### View File at Specific Commit
```bash
git show <commit>:<file>
```

### Search Commits
```bash
git log --grep="search term"
```

### Find Who Changed a Line
```bash
git blame <file>
```

### List Files in a Commit
```bash
git show --name-only <commit>
```

### Cherry-pick a Commit
```bash
git cherry-pick <commit>
```

### Interactive Rebase
```bash
git rebase -i HEAD~n
```

### Squash Last n Commits
```bash
git rebase -i HEAD~n
# Change "pick" to "squash" for commits to combine
```

## Emergency Commands

### Abort Merge
```bash
git merge --abort
```

### Abort Rebase
```bash
git rebase --abort
```

### Recover Deleted Branch
```bash
git reflog
git checkout -b <branch-name> <commit>
```

### Undo Last Push (if no one pulled)
```bash
git reset --hard HEAD~1
git push --force
```

**⚠️ Warning: Use force push with caution!**

---

## Resources

- [Official Git Documentation](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com)
- [Git Cheat Sheet PDF](https://education.github.com/git-cheat-sheet-education.pdf)
- [Interactive Git Learning](https://learngitbranching.js.org/)

---

**Pro Tip:** Practice these commands in a test repository to build muscle memory! 🚀
