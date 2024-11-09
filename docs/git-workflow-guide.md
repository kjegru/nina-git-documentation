# Git Workflow Guide

This document outlines the branching strategy and workflow used in this project to ensure stability, efficient development, and smooth deployment to production and testing environments.

## Branch Overview

1. **production**: Protected production branch that deploys directly to production servers. Only accepts PRs from `main`.
2. **main**: Protected source of truth, representing the latest stable and approved state of the project.
3. **test**: Protected integration testing branch that deploys to test servers.
4. **dev**: Development branches for individual features (`feat/`) or patches (`fix/`).

## Branching Strategy

### 1. `production` Branch
- **Purpose**: Production-ready code only
- **Protection**: Requires PR and approvals from `main`
- **Deploys**: Automatically to production servers
- **Rules**: No direct commits, PR only

### 2. `main` Branch
- **Purpose**: Source of truth for stable code
- **Protection**: Requires PR and approvals
- **Updates**: Accepts PRs from `test` after successful testing
- **Rules**: No direct commits, PR only

### 3. `test` Branch
- **Purpose**: Integration testing environment
- **Protection**: Requires PR from feature/fix branches
- **Deploys**: Automatically to test servers
- **Rules**: PR required, automated tests must pass

### 4. Feature and Fix Branches
- **Purpose**: Individual development work
- **Naming**: 
  - Features: `feat/feature-name`
  - Fixes: `fix/issue-name`
- **Source**: Always branch from `test`
- **Merge**: Back to `test` via PR

## Workflow Steps

### 1. Starting New Work
```bash
# Update test branch
git checkout test
git pull origin test

# Create new feature branch
git checkout -b feat/feature-name
# or for fixes
git checkout -b fix/issue-name
```

### 2. Development Process
```bash
# Regular commits to your branch
git add .
git commit -m "feat: descriptive message"

# Keep branch updated with test
git checkout test
git pull origin test
git checkout feat/feature-name
git rebase test
```

### 3. Creating Pull Requests
1. **Feature → Test**
   - Create PR from your feature branch to `test`
   - Ensure all tests pass
   - Get code review approval
   - Merge using rebase strategy

2. **Test → Main**
   - After testing in test environment
   - Create PR from `test` to `main`
   - Requires additional review
   - Merge using rebase strategy

3. **Main → Production**
   - Create PR from `main` to `production`
   - Final review and approval
   - Merge using rebase strategy

## Best Practices

1. **Commit Messages**
   - Use conventional commits format:
     - `feat: add new feature`
     - `fix: resolve issue`
     - `docs: update documentation`
     - `refactor: improve code structure`

2. **Branch Management**
   - Keep branches short-lived
   - Delete branches after merging
   - Regularly rebase with `test`

3. **Code Review**
   - Required for all PRs
   - Check for:
     - Code quality
     - Test coverage
     - Documentation updates
     - Security considerations

4. **Deployment Verification**
   - Verify deployments in test environment
   - Run full test suite before production merge
   - Monitor deployments for issues

## Common Commands

```bash
# Create new feature branch
git checkout -b feat/feature-name

# Update branch with latest test changes
git checkout test
git pull origin test
git checkout feat/feature-name
git rebase test

# Force push after rebase (if needed)
git push origin feat/feature-name --force-with-lease

# Delete local branch after merge
git branch -d feat/feature-name

# Delete remote branch
git push origin --delete feat/feature-name
```
