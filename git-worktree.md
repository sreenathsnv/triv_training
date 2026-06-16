# Git Worktree Workflow for Emergency Hotfixes

This guide explains how to use `git worktree` to handle emergency hotfixes without interrupting your current development work.

---

# Scenario

You are working on:

```bash
feature-x
```

and running a long-lived process like:

```bash
npm run dev
```

Suddenly, production needs a hotfix from `main`.

You want to:

* keep `feature-x` running
* create a separate worktree
* create a hotfix branch
* fix and merge the issue
* push changes
* return to feature work uninterrupted

---

# Why Use Git Worktree?

Without worktrees, you would typically:

```bash
git stash
git checkout main
# fix issue
git checkout feature-x
git stash pop
```

Problems with this approach:

* stops running processes
* rebuilds environments
* risks stash conflicts
* causes context switching chaos

With `git worktree`, each branch gets its own directory.

Your running process continues uninterrupted.

---

# Example Repository Layout

Assume your current repository is:

```text
~/projects/myapp
```

Current state:

```text
~/projects/myapp  -> feature-x
```

---

# Step 1 — Continue Working on Feature Branch

Inside your main repo:

```bash
cd ~/projects/myapp
git branch
```

Output:

```text
* feature-x
```

Start your development process:

```bash
npm run dev
```

Leave this terminal running.

---

# Step 2 — Create a Separate Worktree for Hotfix

Open a new terminal.

Fetch latest changes:

```bash
cd ~/projects/myapp
git fetch origin
```

Create a new worktree from `main`:

```bash
git worktree add ../myapp-hotfix main
```

Now your directories look like:

```text
~/projects/myapp          -> feature-x
~/projects/myapp-hotfix   -> main
```

Your original process is still running.

---

# Step 3 — Create a Hotfix Branch

Move into the new worktree:

```bash
cd ../myapp-hotfix
```

Create a hotfix branch:

```bash
git switch -c hotfix-login-bug
```

Now:

```text
feature-x worktree  -> feature-x
hotfix worktree     -> hotfix-login-bug
```

---

# Step 4 — Fix the Issue

Make your code changes.

Commit them:

```bash
git add .
git commit -m "Fix login crash"
```

---

# Step 5 — Merge into Main

Switch back to `main`:

```bash
git switch main
```

Merge the hotfix branch:

```bash
git merge hotfix-login-bug
```

---

# Step 6 — Push Changes

Push updated `main`:

```bash
git push origin main
```

Optionally push the hotfix branch:

```bash
git push origin hotfix-login-bug
```

---

# Step 7 — Cleanup

Remove the worktree:

```bash
cd ..
git worktree remove myapp-hotfix
```

Delete the temporary branch:

```bash
git branch -d hotfix-login-bug
```

---

# One-Line Shortcut

You can create the worktree and branch together:

```bash
git worktree add -b hotfix-login-bug ../myapp-hotfix main
```

This command:

* creates a new worktree
* creates a new branch
* starts from `main`
* checks out the branch automatically

---

# Useful Commands

## List Worktrees

```bash
git worktree list
```

---

## Remove a Worktree

```bash
git worktree remove <path>
```

Example:

```bash
git worktree remove ../myapp-hotfix
```

---

## Cleanup Stale Worktree Metadata

```bash
git worktree prune
```

---

# Recommended Professional Setup

Many developers keep multiple parallel worktrees:

```text
repo/              -> active feature
repo-hotfix/       -> production fixes
repo-release/      -> release branch
repo-experiment/   -> spike/testing work
```

This is especially useful for:

* monorepos
* frontend/backend parallel work
* release engineering
* CI debugging
* long-running dev servers

---

# Key Benefits

* No stashing
* No stopping running processes
* Parallel branch development
* Cleaner mental context
* Faster switching between tasks
* Shared Git history without full clones

---

# Quick Cheat Sheet

```bash
# create worktree from existing branch
git worktree add ../dir branch

# create worktree + new branch
git worktree add -b newbranch ../dir main

# list worktrees
git worktree list

# remove worktree
git worktree remove ../dir

# cleanup stale metadata
git worktree prune
```
