# GitHub Practical Examples & Use Cases 💡

Real-world scenarios and practical examples to help you master GitHub workflows.

## Table of Contents
1. [Starting Your First Project](#starting-your-first-project)
2. [Contributing to Open Source](#contributing-to-open-source)
3. [Team Collaboration](#team-collaboration)
4. [Common Workflows](#common-workflows)
5. [Problem Solving](#problem-solving)
6. [Best Practices in Action](#best-practices-in-action)

---

## Starting Your First Project

### Example 1: Create a Personal Website Repository

```bash
# Create local directory
mkdir my-portfolio
cd my-portfolio

# Initialize git
git init

# Create basic files
echo "# My Portfolio" > README.md
cat > index.html << 'EOF'
<!DOCTYPE html>
<html>
<head>
    <title>My Portfolio</title>
</head>
<body>
    <h1>Welcome to My Portfolio</h1>
</body>
</html>
EOF

cat > style.css << 'EOF'
body {
    font-family: Arial, sans-serif;
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
}
EOF

# Create .gitignore
cat > .gitignore << 'EOF'
.DS_Store
node_modules/
*.log
EOF

# Initial commit
git add .
git commit -m "Initial commit: Basic portfolio structure"

# Create repo on GitHub (using gh CLI)
gh repo create my-portfolio --public --source=. --push

# Or manually connect to GitHub
# Create repo on GitHub.com first, then:
git remote add origin https://github.com/yourusername/my-portfolio.git
git branch -M main
git push -u origin main
```

### Example 2: Start a Node.js Project

```bash
# Create project
mkdir awesome-app
cd awesome-app

# Initialize npm and git
npm init -y
git init

# Install dependencies
npm install express

# Create .gitignore
cat > .gitignore << 'EOF'
node_modules/
.env
*.log
dist/
.DS_Store
EOF

# Create basic app
cat > app.js << 'EOF'
const express = require('express');
const app = express();

app.get('/', (req, res) => {
    res.send('Hello World!');
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
EOF

# Create README
cat > README.md << 'EOF'
# Awesome App

A simple Express.js application.

## Installation

```bash
npm install
```

## Usage

```bash
node app.js
```
EOF

# Commit and push
git add .
git commit -m "Initial setup: Express app with basic route"
git remote add origin https://github.com/yourusername/awesome-app.git
git push -u origin main
```

---

## Contributing to Open Source

### Example 3: Making Your First Contribution

**Step-by-step real example:**

```bash
# 1. Find a project to contribute to
# Let's say: https://github.com/firstcontributions/first-contributions

# 2. Fork the repository (click Fork button on GitHub)

# 3. Clone YOUR fork
git clone https://github.com/YOURUSERNAME/first-contributions.git
cd first-contributions

# 4. Add upstream remote (original repo)
git remote add upstream https://github.com/firstcontributions/first-contributions.git

# 5. Create a branch for your contribution
git checkout -b add-your-name

# 6. Make your changes
# For example, add your name to Contributors.md
echo "- [Your Name](https://github.com/yourusername)" >> Contributors.md

# 7. Commit your changes
git add Contributors.md
git commit -m "Add Your Name to contributors list"

# 8. Push to your fork
git push origin add-your-name

# 9. Go to GitHub and create a Pull Request
# Navigate to your fork and click "Compare & pull request"

# 10. Wait for review and feedback

# 11. If changes are requested, make them:
# Edit the file
git add Contributors.md
git commit -m "Update contributor entry format"
git push origin add-your-name

# 12. After merge, sync your fork:
git checkout main
git fetch upstream
git merge upstream/main
git push origin main

# 13. Delete your feature branch
git branch -d add-your-name
git push origin --delete add-your-name
```

### Example 4: Fixing a Bug in Open Source Project

```bash
# 1. Find an issue labeled "good first issue" or "bug"

# 2. Comment on the issue saying you want to work on it

# 3. Fork and clone the repository
git clone https://github.com/yourusername/project.git
cd project

# 4. Install dependencies and run tests
npm install
npm test

# 5. Create a branch
git checkout -b fix-issue-123

# 6. Reproduce the bug
# Read the issue, write a test that fails

# 7. Fix the bug
# Edit the relevant files

# 8. Verify the fix
npm test
npm run lint

# 9. Commit with reference to issue
git add .
git commit -m "Fix memory leak in data processor

- Close file handles properly
- Add test for resource cleanup
- Fixes #123"

# 10. Push and create PR
git push origin fix-issue-123
# Create PR on GitHub, reference the issue in description
```

---

## Team Collaboration

### Example 5: Feature Branch Workflow

**Scenario**: You're working on a team building an e-commerce site. You need to add a shopping cart feature.

```bash
# 1. Start with updated main
git checkout main
git pull origin main

# 2. Create feature branch
git checkout -b feature/shopping-cart

# 3. Work on feature - make multiple commits
# Day 1: Basic structure
git add src/cart.js
git commit -m "Add shopping cart component structure"

# Day 2: Add functionality
git add src/cart.js src/cart.test.js
git commit -m "Implement add to cart functionality with tests"

# Day 3: Integrate with UI
git add src/CartView.js src/cart.css
git commit -m "Add shopping cart UI and styling"

# 4. Keep your branch updated with main
git fetch origin
git rebase origin/main
# If conflicts occur, resolve them:
# - Edit conflicted files
# - git add <resolved-files>
# - git rebase --continue

# 5. Push your branch
git push origin feature/shopping-cart

# 6. Create Pull Request on GitHub
gh pr create --title "Add shopping cart feature" \
  --body "Implements shopping cart with add/remove items and checkout flow.

- Add cart component
- Implement local storage persistence
- Add unit tests (95% coverage)
- Update documentation

Closes #45"

# 7. Request reviews from teammates
gh pr view --web  # Opens in browser to add reviewers

# 8. Address review comments
# Make changes based on feedback
git add .
git commit -m "Address PR feedback: Add error handling"
git push origin feature/shopping-cart

# 9. After approval, merge via GitHub interface

# 10. Clean up
git checkout main
git pull origin main
git branch -d feature/shopping-cart
```

### Example 6: Hotfix Workflow

**Scenario**: Critical bug in production needs immediate fix.

```bash
# 1. Create hotfix branch from main
git checkout main
git pull origin main
git checkout -b hotfix/payment-processing

# 2. Fix the critical bug
git add src/payment.js
git commit -m "Fix payment processing timeout issue"

# 3. Add test to prevent regression
git add tests/payment.test.js
git commit -m "Add test for payment timeout handling"

# 4. Push and create PR with high priority
git push origin hotfix/payment-processing
gh pr create --title "HOTFIX: Fix payment processing timeout" \
  --body "Critical fix for payment timeout issue affecting users.

- Increase timeout from 5s to 30s
- Add retry logic
- Add comprehensive error handling

This needs urgent review and deployment." \
  --label "critical,hotfix"

# 5. After fast-track review and merge
git checkout main
git pull origin main
git tag -a v1.2.1 -m "Hotfix: Payment processing timeout"
git push origin v1.2.1
```

### Example 7: Collaborative Development with Multiple Developers

**Scenario**: Three developers working on related features.

```bash
# Developer A: Working on user authentication
git checkout -b feature/user-auth
# Make changes...
git commit -m "Add user login functionality"
git push origin feature/user-auth
# Create PR

# Developer B: Working on user profile (depends on auth)
git checkout -b feature/user-profile
# Wait for Developer A's PR to be merged, then:
git fetch origin
git merge origin/main  # Get the merged auth feature
# Make changes...
git commit -m "Add user profile page"
git push origin feature/user-profile
# Create PR

# Developer C: Working on admin panel (separate feature)
git checkout -b feature/admin-panel
# Can work independently
git commit -m "Add admin dashboard"
git push origin feature/admin-panel
# Create PR

# Integration: After all PRs are reviewed
# All features merge into main through separate PRs
# Each developer updates their local main:
git checkout main
git pull origin main
```

---

## Common Workflows

### Example 8: Fixing Merge Conflicts

```bash
# Scenario: Your feature branch has conflicts with main

# 1. Update main and try to merge
git checkout main
git pull origin main
git checkout feature/my-feature
git merge main

# Output: CONFLICT (content): Merge conflict in src/app.js

# 2. Check which files have conflicts
git status

# 3. Open conflicted file
# You'll see something like:
# <<<<<<< HEAD
# Your changes
# =======
# Changes from main
# >>>>>>> main

# 4. Edit to resolve (example in src/app.js):
# Before:
# <<<<<<< HEAD
# const PORT = 3000;
# =======
# const PORT = process.env.PORT || 8080;
# >>>>>>> main

# After resolution:
const PORT = process.env.PORT || 3000;

# 5. Mark as resolved
git add src/app.js

# 6. Complete the merge
git commit -m "Merge main into feature/my-feature, resolve conflicts"

# 7. Push updated branch
git push origin feature/my-feature
```

### Example 9: Squashing Commits Before Merge

```bash
# Scenario: You made many small commits and want to clean history

# 1. Check your commits
git log --oneline
# a1b2c3d Fix typo
# b2c3d4e Update tests
# c3d4e5f Add feature
# d4e5f6g WIP
# e5f6g7h Start feature

# 2. Interactive rebase (last 5 commits)
git rebase -i HEAD~5

# 3. In the editor, change 'pick' to 'squash' or 's' for commits to combine:
# pick e5f6g7h Start feature
# squash d4e5f6g WIP
# squash c3d4e5f Add feature
# squash b2c3d4e Update tests
# squash a1b2c3d Fix typo

# 4. Save and close editor. Another editor opens for commit message:
# Combine messages or write a new one:
"Add shopping cart feature

- Implement cart component
- Add tests and documentation
- Fix styling issues"

# 5. Force push (your branch only!)
git push --force-with-lease origin feature/shopping-cart
```

### Example 10: Cherry-picking Commits

```bash
# Scenario: Need specific commit from one branch in another

# 1. Find the commit hash you need
git log feature/old-feature --oneline
# a1b2c3d Add useful utility function

# 2. Switch to target branch
git checkout feature/new-feature

# 3. Cherry-pick the commit
git cherry-pick a1b2c3d

# 4. If conflicts occur:
# - Resolve conflicts
git add .
git cherry-pick --continue

# 5. Push the change
git push origin feature/new-feature
```

---

## Problem Solving

### Example 11: Accidentally Committed to Wrong Branch

```bash
# Oh no! You committed to main instead of a feature branch

# 1. Create a new branch with your current changes
git branch feature/my-work

# 2. Reset main to remote state
git reset --hard origin/main

# 3. Switch to your feature branch
git checkout feature/my-work

# 4. Your changes are safe! Push the feature branch
git push origin feature/my-work
```

### Example 12: Committed Sensitive Data

```bash
# You accidentally committed a password or API key

# 1. Remove the file immediately
git rm config/secrets.json
git commit -m "Remove sensitive data"

# 2. Rewrite history to remove it entirely
# Install BFG Repo-Cleaner or use filter-branch
git filter-branch --force --index-filter \
  "git rm --cached --ignore-unmatch config/secrets.json" \
  --prune-empty --tag-name-filter cat -- --all

# 3. Force push to update remote
git push origin --force --all

# 4. Tell collaborators to rebase their work

# 5. IMPORTANT: Rotate the compromised credentials!
# The secret is still in GitHub's history cache

# 6. Add to .gitignore to prevent future accidents
echo "config/secrets.json" >> .gitignore
git add .gitignore
git commit -m "Add secrets file to gitignore"
```

### Example 13: Lost Commits (Recover from Detached HEAD)

```bash
# You made commits in detached HEAD state and need to recover them

# 1. Find lost commits in reflog
git reflog
# Shows all HEAD movements:
# a1b2c3d HEAD@{0}: checkout: moving to main
# b2c3d4e HEAD@{1}: commit: Important feature
# c3d4e5f HEAD@{2}: commit: More work

# 2. Create branch from lost commit
git branch recovered-work b2c3d4e

# 3. Verify the recovered work
git checkout recovered-work
git log

# 4. Merge into appropriate branch
git checkout main
git merge recovered-work
```

---

## Best Practices in Action

### Example 14: Setting Up a New Team Repository

```bash
# 1. Create repository with proper structure
mkdir awesome-project
cd awesome-project
git init

# 2. Add comprehensive .gitignore
curl https://www.toptal.com/developers/gitignore/api/node,macos,linux,windows,visualstudiocode > .gitignore

# 3. Add LICENSE
cat > LICENSE << 'EOF'
MIT License

Copyright (c) 2026 Your Organization
[Full MIT license text]
EOF

# 4. Create comprehensive README
cat > README.md << 'EOF'
# Awesome Project

## Description
Brief project description

## Getting Started
### Prerequisites
- Node.js 16+
- npm or yarn

### Installation
```bash
npm install
```

### Development
```bash
npm run dev
```

### Testing
```bash
npm test
```

## Contributing
See [CONTRIBUTING.md](CONTRIBUTING.md)

## License
MIT - see [LICENSE](LICENSE)
EOF

# 5. Add contributing guidelines
cat > CONTRIBUTING.md << 'EOF'
# Contributing

## Process
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Write tests
5. Submit a pull request

## Code Style
- Follow ESLint rules
- Write meaningful commit messages
- Add tests for new features
EOF

# 6. Set up GitHub Actions for CI
mkdir -p .github/workflows
cat > .github/workflows/ci.yml << 'EOF'
name: CI

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
        with:
          node-version: '16'
      - run: npm install
      - run: npm test
      - run: npm run lint
EOF

# 7. Initial commit
git add .
git commit -m "Initial project setup

- Add project structure
- Configure CI/CD
- Add documentation"

# 8. Push to GitHub
git remote add origin https://github.com/org/awesome-project.git
git push -u origin main

# 9. Set up branch protection on GitHub
# Settings → Branches → Add rule for main:
# - Require pull request reviews
# - Require status checks to pass
# - Require branches to be up to date
```

### Example 15: Code Review Process

```bash
# Reviewer workflow:

# 1. Fetch PR branch
git fetch origin pull/123/head:pr-123
git checkout pr-123

# 2. Run tests locally
npm install
npm test

# 3. Review code and test functionality
npm start  # Test the feature

# 4. Leave comments on GitHub or:
gh pr review 123 --comment -b "Good work! Please add tests for edge cases."

# 5. Request changes if needed:
gh pr review 123 --request-changes -b "Please address the following..."

# 6. Approve when ready:
gh pr review 123 --approve -b "LGTM! Great work!"

# Author addressing feedback:
git checkout feature/branch
# Make requested changes
git add .
git commit -m "Address review feedback: Add edge case tests"
git push origin feature/branch
```

---

## GitHub-Specific Features

### Example 16: Using GitHub Issues Effectively

```bash
# Create issue from command line
gh issue create --title "Add dark mode support" \
  --body "Users have requested dark mode.

Tasks:
- [ ] Design dark theme
- [ ] Implement CSS variables
- [ ] Add theme toggle
- [ ] Persist user preference
- [ ] Update documentation

Estimated: 2 days" \
  --label "enhancement,good-first-issue" \
  --assignee yourusername

# Link commit to issue
git commit -m "Add dark mode CSS variables

Relates to #42"

# Close issue with commit
git commit -m "Implement dark mode theme toggle

Closes #42"
```

### Example 17: Release Management

```bash
# Create a release version

# 1. Update version number
npm version minor  # Updates package.json and creates tag

# 2. Update CHANGELOG
cat >> CHANGELOG.md << 'EOF'
## [1.1.0] - 2026-01-02
### Added
- Dark mode support
- User preferences
### Fixed
- Memory leak in data processor
EOF

# 3. Commit changes
git add .
git commit -m "Bump version to 1.1.0"

# 4. Tag the release
git tag -a v1.1.0 -m "Release version 1.1.0

New features:
- Dark mode
- User preferences

Bug fixes:
- Memory leak fixed"

# 5. Push commits and tags
git push origin main
git push origin v1.1.0

# 6. Create GitHub release
gh release create v1.1.0 \
  --title "Version 1.1.0 - Dark Mode" \
  --notes "See CHANGELOG.md for details" \
  dist/app.zip
```

---

## Conclusion

These practical examples cover the most common scenarios you'll encounter when using GitHub. Remember:

- **Practice** these workflows in a test repository first
- **Ask questions** when unsure - the GitHub community is helpful
- **Document** your team's specific workflows
- **Automate** repetitive tasks with aliases and scripts
- **Learn from mistakes** - that's what version control is for!

Happy coding! 🚀

---

*Pro Tip: Keep this guide bookmarked and refer to it when you encounter similar situations in your work.*
