# Git Basics: A Beginner's Guide

This guide will help you understand the basic Git commands you need to start version controlling your projects.

## Setting Up Git

There are many ways to work with Git, as there are numerous programs available:

- **RStudio**: Integrated Git support for projects*.
- **VS Code**: Built-in Git tools and extensions.
- **Standalone Tools**: Many standalone Git clients are also available. E.g. Gitcraken

* Integrated when using one of the share NINA-servers like https://rstudio.nina.no. If using the Windows laptop Git has be installed using Firmaportal and searching for "git 2".

However, this guide uses Git in the terminal, as it is a universal approach that works across all environments. The subcommand in the Git commands will match what you see in your chosen program anyway.


### First-time Setup
Before you start using Git, you should set up your identity:
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

## Basic Git Commands

### Creating a New Local Repository
To start version controlling a project:
```bash
# Navigate to your project folder
cd your-project-folder

# Initialize Git repository
git init
```
### Working with Changes

#### Checking Status
Always start by checking what files have changed:
```bash
git status
```

#### Adding Files
To prepare files for commit (staging):
```bash
# Add a specific file
git add filename.txt

# Add multiple files
git add file1.txt file2.txt

# Add all changed files in the current directory
git add .

# Add all files across entire project and show the files that are added
git add -Av

# Add all files with a specific extension
git add *.txt
```

#### Committing Changes
Save your staged changes:
```bash
# Basic commit
git commit -m "Your commit message"

# Add and commit in one command (only for tracked files)
git commit -am "Your commit message"
```

#### Viewing Changes
See what you've changed:
```bash
# See unstaged changes
git diff

# See staged changes
git diff --staged

# See commit history
git log
```

### Working with Remote Repositories

There are two ways to get a connect to an existing remote repository:

#### Cloning an Existing Remote Repository
This is done when the remote repostory has a lot of files.
To get a copy of an existing Git repository:
```bash
# Clone a repository from GitHub/GitLab etc.
git clone https://github.com/username/repository-name.git

# Clone to a specific folder
git clone https://github.com/username/repository-name.git my-folder
```


#### Adding a Remote Repository
Connecting a local repository to a remote empty repository:
```bash
git remote add origin https://github.com/username/repository-name.git
```

#### Pushing Changes
Send your commits to the remote repository:
```bash
# First time push from a new branch
git push -u origin main

# Subsequent pushes
git push
```

#### Getting Updates
Remember: Always pull before you push to avoid conflicts!
Get and integrate changes from the remote repository:
```bash
# Fetch changes without merging
git fetch

# Fetch and merge changes
git pull
```

## Common Workflows

### Starting a New Project
```bash
# Create a new directory
mkdir my-project
cd my-project

# Initialize Git
git init

# Create some files
touch README.md

# Add and commit files
git add .
git commit -m "Initial commit"

# Connect to remote (if using GitHub/GitLab)
git remote add origin https://github.com/username/my-project.git
git push -u origin main
```

### Working on an Existing Project
```bash
# Clone the repository
git clone https://github.com/username/project.git

# Make changes to files
# ...

# Check status
git status

# Add changes
git add .

# Commit changes
git commit -m "Description of changes"

# Push changes
git push
```

## Best Practices

1. **Commit Messages**
   - Use clear, descriptive commit messages
   - Start with a verb (Add, Update, Fix, etc.)
   - Keep messages concise but informative

2. **Frequent Commits**
   - Commit small, logical changes
   - Don't wait until you have many changes
   - Each commit should represent one logical change

3. **Pull Before Push**
   - Always pull before pushing to avoid conflicts
   - Handle any conflicts locally before pushing

4. **Check Status Regularly**
   - Use `git status` frequently
   - Verify what files are staged before committing

## Common Issues and Solutions

### Undoing Changes
```bash
# Undo unstaged changes to a file
git checkout -- filename

# Unstage a file (but keep changes)
git reset HEAD filename

# Undo last commit (keep changes staged)
git reset --soft HEAD^

# Undo last commit and all changes
git reset --hard HEAD^
```

### Fixing Wrong Commit Message
```bash
# Fix last commit message
git commit --amend -m "New message"
```

### Handling Merge Conflicts
When you get a merge conflict:
1. Open the conflicted files
2. Look for the conflict markers (<<<<<<, =======, >>>>>>>)
3. Edit the files to resolve conflicts
4. Add the resolved files
5. Complete the merge with commit

```bash
# After resolving conflicts
git add .
git commit -m "Resolve merge conflicts"
```
