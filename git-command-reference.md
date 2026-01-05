# Git Commands Reference Guide
*Complete guide for Web Technology course and beyond*

---

## Table of Contents
1. [Initial Setup](#initial-setup)
2. [Basic Workflow](#basic-workflow)
3. [Viewing History & Changes](#viewing-history--changes)
4. [Undoing Changes](#undoing-changes)
5. [Branching](#branching)
6. [GitHub Collaboration](#github-collaboration)
7. [Handling Conflicts](#handling-conflicts)
8. [Advanced Commands](#advanced-commands)
9. [Common Scenarios](#common-scenarios)

---

## Initial Setup

### Configure Git (First time only)
```bash
# Set your name
git config --global user.name "Mohamed"

# Set your email
git config --global user.email "your.email@vu.nl"

# Set default branch name to 'main'
git config --global init.defaultBranch main

# View all configurations
git config --list

# View specific config
git config user.name
```

### Initialize a Repository
```bash
# Create new repository in current folder
git init

# Check if repository exists
ls -la .git
```

---

## Basic Workflow

### Checking Status
```bash
# See which files are modified, staged, or untracked
git status

# Short format
git status -s
```

### Adding Files (Staging)
```bash
# Add specific file
git add index.html

# Add multiple files
git add index.html style.css

# Add all HTML files
git add *.html

# Add all files in current directory
git add .

# Add all files including deletions
git add -A

# Add files interactively (choose what to stage)
git add -p
```

### Committing Changes
```bash
# Commit staged changes with message
git commit -m "Add navigation menu"

# Commit with detailed message (opens editor)
git commit

# Add and commit in one command (only for tracked files)
git commit -am "Fix header alignment"

# Amend last commit (add forgotten files or fix message)
git add forgotten-file.html
git commit --amend --no-edit

# Amend and change commit message
git commit --amend -m "New commit message"
```

---

## Viewing History & Changes

### View Commit History
```bash
# Full commit history
git log

# One line per commit
git log --oneline

# Last 5 commits
git log -5

# Show files changed in each commit
git log --stat

# Show actual changes in each commit
git log -p

# Visual graph of branches
git log --oneline --graph --all

# Search commits by message
git log --grep="navigation"

# Commits by specific author
git log --author="Mohamed"

# Commits in date range
git log --since="2025-01-01" --until="2025-01-31"
```

### View Changes
```bash
# Show unstaged changes
git diff

# Show staged changes
git diff --staged

# Compare specific file
git diff index.html

# Compare two commits
git diff abc123 def456

# Compare with previous commit
git diff HEAD~1

# Show changes in specific commit
git show abc123
```

### View File History
```bash
# See who changed each line (blame)
git blame index.html

# Show all commits that modified a file
git log -- index.html
```

---

## Undoing Changes

### Discard Changes (Working Directory)
```bash
# Discard changes in specific file
git checkout -- index.html

# Discard all changes
git checkout -- .

# Alternative (newer syntax)
git restore index.html
git restore .
```

### Unstage Files
```bash
# Unstage specific file (keep changes)
git reset HEAD index.html

# Unstage all files
git reset HEAD

# Alternative (newer syntax)
git restore --staged index.html
```

### Undo Commits
```bash
# Undo last commit, keep changes staged
git reset --soft HEAD~1

# Undo last commit, keep changes unstaged
git reset HEAD~1

# Undo last commit, discard changes (DANGEROUS!)
git reset --hard HEAD~1

# Undo last 3 commits
git reset --soft HEAD~3

# Create new commit that undoes previous commit
git revert HEAD

# Revert specific commit
git revert abc123
```

### Clean Untracked Files
```bash
# Show what would be deleted
git clean -n

# Delete untracked files
git clean -f

# Delete untracked files and directories
git clean -fd
```

---

## Branching

### Creating Branches
```bash
# Create new branch
git branch feature-login

# Create and switch to new branch
git checkout -b feature-navigation

# Alternative (newer syntax)
git switch -c feature-navigation
```

### Switching Branches
```bash
# Switch to existing branch
git checkout main

# Alternative (newer syntax)
git switch main

# Switch to previous branch
git checkout -
```

### Viewing Branches
```bash
# List all local branches
git branch

# List all branches (including remote)
git branch -a

# Show last commit on each branch
git branch -v
```

### Merging Branches
```bash
# Merge feature-login into current branch
git merge feature-login

# Merge with custom commit message
git merge feature-login -m "Merge login feature"

# Abort a merge with conflicts
git merge --abort
```

### Deleting Branches
```bash
# Delete merged branch
git branch -d feature-login

# Force delete unmerged branch (CAREFUL!)
git branch -D feature-login

# Delete remote branch
git push origin --delete feature-login
```

---

## GitHub Collaboration

### Connecting to GitHub
```bash
# Add remote repository
git remote add origin https://github.com/mo-dhubai/practice-git.git

# View remote repositories
git remote -v

# Change remote URL
git remote set-url origin https://github.com/mo-dhubai/new-repo.git

# Remove remote
git remote remove origin
```

### Pushing to GitHub
```bash
# Push to main branch (first time)
git push -u origin main

# Push after first time
git push

# Push specific branch
git push origin feature-login

# Push all branches
git push --all

# Force push (DANGEROUS! - overwrites remote)
git push --force
```

### Pulling from GitHub
```bash
# Pull latest changes from main
git pull origin main

# Pull from current branch
git pull

# Pull without merging (safer)
git fetch origin
git merge origin/main
```

### Fetching Updates
```bash
# Download changes without merging
git fetch origin

# See all remote branches
git fetch --all

# View fetched changes
git log origin/main
```

### Cloning Repository
```bash
# Clone repository to current directory
git clone https://github.com/mo-dhubai/practice-git.git

# Clone to specific folder
git clone https://github.com/mo-dhubai/practice-git.git my-project

# Clone specific branch
git clone -b feature-login https://github.com/mo-dhubai/practice-git.git
```

---

## Handling Conflicts

### When Merge Conflicts Occur
```bash
# 1. Check which files have conflicts
git status

# 2. Open conflicted files and look for:
# <<<<<<< HEAD
# Your changes
# =======
# Partner's changes
# >>>>>>> feature-branch

# 3. Edit files to resolve conflicts

# 4. Add resolved files
git add conflicted-file.html

# 5. Complete the merge
git commit -m "Resolve merge conflicts"

# OR abort the merge
git merge --abort
```

### Avoiding Conflicts
```bash
# Always pull before starting work
git pull origin main

# Check for changes before pushing
git fetch origin
git status
```

---

## Advanced Commands

### Stashing (Temporarily Save Work)
```bash
# Save current changes without committing
git stash

# Stash with description
git stash save "Work in progress on navigation"

# List all stashes
git stash list

# Apply most recent stash
git stash apply

# Apply and remove stash
git stash pop

# Apply specific stash
git stash apply stash@{2}

# Delete specific stash
git stash drop stash@{0}

# Clear all stashes
git stash clear
```

### Tagging (Version Releases)
```bash
# Create lightweight tag
git tag v1.0

# Create annotated tag (recommended)
git tag -a v1.0 -m "First release"

# List all tags
git tag

# Push tag to GitHub
git push origin v1.0

# Push all tags
git push --tags

# Delete tag
git tag -d v1.0

# Delete remote tag
git push origin --delete v1.0
```

### Cherry-picking (Copy Specific Commits)
```bash
# Apply specific commit to current branch
git cherry-pick abc123

# Cherry-pick multiple commits
git cherry-pick abc123 def456
```

### Rebasing (Alternative to Merging)
```bash
# Rebase current branch onto main
git rebase main

# Interactive rebase (edit commit history)
git rebase -i HEAD~3

# Abort rebase
git rebase --abort

# Continue after resolving conflicts
git rebase --continue
```

---

## Common Scenarios

### Scenario 1: Starting a New Project
```bash
# 1. Create project folder
mkdir my-web-project
cd my-web-project

# 2. Initialize Git
git init

# 3. Create .gitignore file
echo "node_modules/" > .gitignore
echo ".DS_Store" >> .gitignore

# 4. Create initial files
touch index.html

# 5. First commit
git add .
git commit -m "Initial commit"

# 6. Connect to GitHub
git remote add origin https://github.com/mo-dhubai/my-web-project.git
git push -u origin main
```

### Scenario 2: Daily Work Routine
```bash
# Start of day - get latest changes
git pull origin main

# Make changes to files...

# Check what changed
git status
git diff

# Stage and commit
git add .
git commit -m "Add responsive header"

# Push to GitHub
git push

# End of day - make sure everything is committed
git status
```

### Scenario 3: Working with a Partner
```bash
# Before starting work
git pull origin main

# Create feature branch
git checkout -b feature-contact-form

# Make changes and commit
git add .
git commit -m "Add contact form HTML structure"

# Push your branch
git push origin feature-contact-form

# Partner reviews and merges on GitHub
# Then you update your local main
git checkout main
git pull origin main

# Delete old feature branch
git branch -d feature-contact-form
```

### Scenario 4: You Made a Mistake
```bash
# Wrong file committed
git reset HEAD~1
git add correct-file.html
git commit -m "Add correct file"

# Wrong commit message
git commit --amend -m "Correct commit message"

# Want to undo last commit completely
git reset --hard HEAD~1

# Committed to wrong branch
git checkout correct-branch
git cherry-pick abc123  # Copy the commit
git checkout wrong-branch
git reset --hard HEAD~1  # Remove from wrong branch
```

### Scenario 5: Lost Work Recovery
```bash
# Find lost commits
git reflog

# Recover lost commit
git checkout abc123
git checkout -b recovered-work

# Or reset to lost commit
git reset --hard abc123
```

### Scenario 6: Clean Up Before Pushing
```bash
# Check what will be pushed
git log origin/main..HEAD

# Combine last 3 commits into one
git rebase -i HEAD~3
# In editor: change 'pick' to 'squash' for commits to combine

# Force push (only if not shared with others!)
git push --force
```

### Scenario 7: Working on Multiple Features
```bash
# Currently on feature-A, need to switch to feature-B
git stash save "Incomplete feature-A work"
git checkout -b feature-B

# Work on feature-B
git add .
git commit -m "Complete feature-B"
git push origin feature-B

# Return to feature-A
git checkout feature-A
git stash pop
```

---

## Quick Reference Table

| Task | Command |
|------|---------|
| Initialize repo | `git init` |
| Check status | `git status` |
| Stage file | `git add filename` |
| Stage all | `git add .` |
| Commit | `git commit -m "message"` |
| Push | `git push` |
| Pull | `git pull` |
| Create branch | `git checkout -b branch-name` |
| Switch branch | `git checkout branch-name` |
| Merge branch | `git merge branch-name` |
| View history | `git log --oneline` |
| Undo changes | `git checkout -- filename` |
| Unstage | `git reset HEAD filename` |
| Stash work | `git stash` |
| Apply stash | `git stash pop` |

---

## Best Practices

1. **Commit frequently** - After each logical change
2. **Write clear messages** - Use present tense: "Add feature" not "Added feature"
3. **Pull before push** - Always sync before pushing your changes
4. **Never commit sensitive data** - Passwords, API keys, personal info
5. **Use .gitignore** - Don't commit generated files or dependencies
6. **Branch for features** - Keep main branch stable
7. **Review before committing** - Use `git diff` and `git status`
8. **Don't force push** - Unless you're alone on the branch
9. **Commit complete work** - Don't leave broken code in commits
10. **Keep commits atomic** - One feature/fix per commit

---

## Troubleshooting

### Problem: "Repository not found"
```bash
# Check remote URL
git remote -v

# Update if wrong
git remote set-url origin https://github.com/username/repo.git
```

### Problem: "Failed to push - rejected"
```bash
# Someone else pushed first - pull and merge
git pull origin main
# Resolve any conflicts
git push origin main
```

### Problem: "Merge conflict"
```bash
# See conflicted files
git status

# Edit files to resolve
# Then add and commit
git add .
git commit -m "Resolve conflicts"
```

### Problem: "Accidentally committed to wrong branch"
```bash
# On wrong branch
git reset --soft HEAD~1

# Switch to correct branch
git checkout correct-branch
git add .
git commit -m "Your message"
```

### Problem: "Need to undo everything"
```bash
# Nuclear option - reset to last remote state
git fetch origin
git reset --hard origin/main
```

---

## Additional Resources

- **Official Git Documentation**: https://git-scm.com/doc
- **Pro Git Book** (Free): https://git-scm.com/book/en/v2
- **GitHub Docs**: https://docs.github.com
- **Interactive Git Tutorial**: https://learngitbranching.js.org
- **Git Cheat Sheet**: https://education.github.com/git-cheat-sheet-education.pdf

---

*Created for Web Technology Course - VU Amsterdam*
*Last Updated: January 2025*
