# Git Complete Guide & Reference

A comprehensive guide covering Git installation, configuration, and commands for version control. Perfect for beginners and experienced developers alike.

## Table of Contents

- [Initial Configuration](#initial-configuration)
- [Basic Commands](#basic-commands)
- [Branching & Merging](#branching--merging)
- [Remote Repositories](#remote-repositories)
- [Undoing Changes](#undoing-changes)
- [Stashing](#stashing)
- [Tagging](#tagging)
- [Searching & Finding](#searching--finding)
- [Advanced Operations](#advanced-operations)

## Initial Configuration

### Setting Up Your Identity (Required)

Configure your name and email for commits:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### Essential Configuration

```bash
# Set default branch name to 'main'
git config --global init.defaultBranch main

# Set VS Code as default editor
git config --global core.editor "code --wait"

# Enable colored output
git config --global color.ui auto

# Set pull to rebase by default
git config --global pull.rebase true
```

### Useful Aliases

```bash
git config --global alias.st status
git config --global alias.cm "commit -m"
git config --global alias.lg "log --oneline --graph --all --decorate"
git config --global alias.unstage "reset HEAD --"
```

## Basic Commands

### Creating Repositories

```bash
# Initialize new repository
git init

# Clone existing repository
git clone <url>

# Clone specific branch
git clone -b branch-name <url>
```

### Working with Files

```bash
# Check status
git status

# Add files to staging
git add filename.txt
git add .                # Add all files

# Commit changes
git commit -m "Commit message"
git commit -am "Quick commit"  # Stage and commit tracked files

# View history
git log
git log --oneline --graph --all
```

### Viewing Changes

```bash
# Show unstaged changes
git diff

# Show staged changes
git diff --staged

# Show changes in specific file
git diff filename.txt
```

## Branching & Merging

### Branch Management

```bash
# List branches
git branch
git branch -a         # Include remote branches

# Create new branch
git branch feature-name

# Switch to branch
git checkout feature-name
git switch feature-name   # New syntax (Git 2.23+)

# Create and switch
git checkout -b feature-name
git switch -c feature-name

# Delete branch
git branch -d feature-name
git branch -D feature-name  # Force delete
```

### Merging

```bash
# Merge branch into current branch
git merge feature-name

# Merge without fast-forward
git merge --no-ff feature-name

# Abort merge
git merge --abort
```

### Rebasing

```bash
# Rebase current branch onto main
git rebase main

# Interactive rebase (last 5 commits)
git rebase -i HEAD~5

# Continue/skip/abort rebase
git rebase --continue
git rebase --skip
git rebase --abort
```

## Remote Repositories

### Remote Management

```bash
# List remotes
git remote -v

# Add remote
git remote add origin <url>

# Change remote URL
git remote set-url origin <new-url>

# Remove remote
git remote remove origin
```

### Fetching & Pulling

```bash
# Fetch from remote
git fetch origin

# Pull changes (fetch + merge)
git pull origin main

# Pull with rebase
git pull --rebase origin main
```

### Pushing

```bash
# Push to remote
git push origin main

# Push and set upstream
git push -u origin main

# Push all branches
git push --all origin

# Push tags
git push --tags
```

## Undoing Changes

### Working Directory

```bash
# Discard changes in file
git restore filename.txt
git checkout -- filename.txt  # Old syntax

# Discard all changes
git restore .
```

### Staging Area

```bash
# Unstage file
git restore --staged filename.txt
git reset HEAD filename.txt  # Old syntax
```

### Commits

```bash
# Undo last commit, keep changes
git reset --soft HEAD~1

# Undo last commit, discard changes
git reset --hard HEAD~1

# Revert commit (safe for pushed commits)
git revert HEAD

# Amend last commit
git commit --amend -m "New message"
git commit --amend --no-edit  # Keep message
```

### Recovery

```bash
# Show reflog (history of HEAD)
git reflog

# Restore to previous state
git reset --hard HEAD@{1}

# Create branch from lost commit
git branch recovered-branch abc123
```

## Stashing

```bash
# Stash changes
git stash
git stash save "Work in progress"

# Stash including untracked files
git stash -u

# List stashes
git stash list

# Apply stash
git stash apply
git stash pop  # Apply and remove

# Drop stash
git stash drop stash@{0}

# Clear all stashes
git stash clear
```

## Tagging

```bash
# Create lightweight tag
git tag v1.0.0

# Create annotated tag
git tag -a v1.0.0 -m "Release version 1.0.0"

# List tags
git tag

# Delete tag
git tag -d v1.0.0

# Push tag to remote
git push origin v1.0.0
git push --tags  # Push all tags

# Checkout tag
git checkout v1.0.0
```

## Searching & Finding

### Search Content

```bash
# Search for text
git grep "search term"

# Search with line numbers
git grep -n "search term"

# Find commit that introduced text
git log -S "function_name"

# Find by commit message
git log --grep="bug fix"

# Find by author
git log --author="John"
```

### Blame

```bash
# Show who changed each line
git blame filename.txt

# Blame specific lines
git blame -L 10,20 filename.txt
```

## Advanced Operations

### Interactive Rebase Actions

When running `git rebase -i HEAD~5`:

- **pick** - use commit
- **reword** - use commit, edit message
- **edit** - use commit, stop for amending
- **squash** - meld into previous commit
- **fixup** - like squash, discard message
- **drop** - remove commit

### Submodules

```bash
# Add submodule
git submodule add <url> path/to/submodule

# Initialize submodules
git submodule update --init

# Clone with submodules
git clone --recurse-submodules <url>

# Update submodules
git submodule update --remote
```

### Cleaning

```bash
# Show what would be removed
git clean -n

# Remove untracked files
git clean -f

# Remove untracked files and directories
git clean -fd
```

## Configuration Levels

Git has three configuration levels:

1. **System** - All users: `git config --system`
2. **Global** - Current user: `git config --global`
3. **Local** - Current repository: `git config --local`

Priority: Local > Global > System

### View Configuration

```bash
# List all settings
git config --list

# Show where settings come from
git config --list --show-origin

# Edit global config
git config --global --edit
```

## .gitignore Patterns

Create a `.gitignore` file to exclude files from version control:

```
# Dependencies
node_modules/
vendor/

# Environment files
.env
.env.local

# Build outputs
dist/
build/
*.min.js

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db

# Logs
*.log
```

## Best Practices

1. **Commit often** with clear, descriptive messages
2. **Use branches** for features and bug fixes
3. **Pull before push** to avoid conflicts
4. **Don't commit sensitive data** (passwords, API keys)
5. **Write meaningful commit messages** following conventions
6. **Keep commits atomic** - one logical change per commit
7. **Review changes** before committing with `git diff`
8. **Use `.gitignore`** to exclude unnecessary files
9. **Never rewrite public history** (avoid force push on shared branches)
10. **Test before committing** to ensure code works

## Common Workflows

### Feature Branch Workflow

```bash
# 1. Create and switch to feature branch
git checkout -b feature-name

# 2. Make changes and commit
git add .
git commit -m "Add feature"

# 3. Push to remote
git push -u origin feature-name

# 4. Create Pull Request (on GitHub/GitLab)

# 5. After merge, update main and delete branch
git checkout main
git pull
git branch -d feature-name
```

### Fixing a Bug

```bash
# 1. Create bugfix branch
git checkout -b bugfix-issue-123

# 2. Fix and commit
git add .
git commit -m "Fix: resolve issue #123"

# 3. Push and create PR
git push -u origin bugfix-issue-123
```

## Quick Reference

| Command | Description |
|---------|-------------|
| `git status` | Check repository status |
| `git add .` | Stage all changes |
| `git commit -m "msg"` | Commit with message |
| `git push` | Push to remote |
| `git pull` | Pull from remote |
| `git checkout -b branch` | Create and switch to branch |
| `git merge branch` | Merge branch into current |
| `git log --oneline` | View commit history |
| `git diff` | Show unstaged changes |
| `git stash` | Temporarily save changes |

## Getting Help

```bash
# Get help for a command
git help <command>
git <command> --help

# Quick help
git <command> -h
```

## Resources

- [Official Git Documentation](https://git-scm.com/doc)
- [Pro Git Book](https://git-scm.com/book/en/v2)
- [GitHub Guides](https://guides.github.com/)
- [GitLab Documentation](https://docs.gitlab.com/)

---

**Note**: This guide covers Git version 2.x+. Some commands may differ in older versions.