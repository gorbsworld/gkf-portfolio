
# Troubleshooting Git Push Errors (Beginner-Friendly Guide)

## Overview

This guide helps beginners diagnose and fix common errors when running:

```bash
git push
```

It focuses on the most frequent problems new users encounter when working with Git and GitHub, especially around authentication and branches.

**Audience:**  
New Git/GitHub users who understand basic commands (`git add`, `git commit`, `git push`) but get stuck when errors appear.

**Prerequisites:**

- Git installed
- A local repository with at least one commit
- A remote repository on GitHub (or similar)

---

## 1. Quick Reference Table

Use this table when you see an error message and want a fast explanation + fix.

| Error message (snippet) | Root cause (most likely) | Quick fix |
|-------------------------|--------------------------|-----------|
| `Password authentication is not supported for Git operations` | Using GitHub account password instead of a Personal Access Token (PAT) | Create a PAT and use it as the password when pushing |
| `fatal: not a git repository (or any of the parent directories)` | You’re not inside a Git repo folder | `cd` into the correct project folder |
| `fatal: repository 'https://github.com/.../.git' not found` | URL or remote name is wrong, or repo doesn’t exist | Check remote URL and repo name; fix with `git remote set-url` |
| `error: src refspec main does not match any` | The branch `main` doesn’t exist locally yet | Check branch name with `git branch`; push the correct branch |
| `fatal: 'origin' does not appear to be a git repository` | Remote `origin` is not set | Add remote with `git remote add origin <URL>` |
| `permission denied (publickey)` | SSH keys not set up or wrong key | Add or fix SSH key, or use HTTPS + PAT |

Later sections explain each issue in detail.

---

## 2. Diagnostic Flow: Start Here

When `git push` fails, follow this sequence:

1. **Check if you’re inside a Git repository**

   ```bash
   git status
   ```

   - If you see: `fatal: not a git repository...` → go to [Section 3](#3-not-a-git-repository-error)  
   - Otherwise, continue

2. **Check what branch you’re on**

   ```bash
   git branch
   ```

   - Look for the branch with `*` (e.g. `* main` or `* master`)
   - If you push `main` but your branch is `master`, that’s the issue → see [Section 5](#5-src-refspec-main-does-not-match-any)

3. **Try pushing and read the exact error**

   ```bash
   git push origin main
   ```

   - If you see password / authentication errors → [Section 4](#4-password-authentication-is-not-supported-for-git-operations)
   - If you see refspec errors → [Section 5](#5-src-refspec-main-does-not-match-any)
   - If you see remote/origin errors → [Section 6](#6-origin-does-not-appear-to-be-a-git-repository)
   - If you see 404 / repo not found → [Section 7](#7-repository-not-found)

---

## 3. `not a git repository` Error

**Error:**

```text
fatal: not a git repository (or any of the parent directories): .git
```

### What it means

- Git doesn’t see a `.git` folder in your current directory 
- You’re running Git commands **outside** of a repository

### How to fix it

1. Check where you are:

   ```bash
   pwd      # Mac/Linux/Git Bash
   cd       # Windows
   ```

2. List files:

   ```bash
   ls       # Mac/Linux/Git Bash
   dir      # Windows
   ```

3. Look for your project folder (for example, `my-project` or `username.github.io`).

4. Move into it:

   ```bash
   cd my-project
   git status
   ```

If `git status` now shows tracked files instead of an error, you’re in the right place.

---

## 4. `Password authentication is not supported for Git operations`

**Typical output:**

```text
Password for 'https://username@github.com':
remote: Invalid username or token. Password authentication is not supported for Git operations.
fatal: Authentication failed for 'https://github.com/username/repo.git/'
```

### What it means

GitHub no longer accepts account passwords for `git push` over HTTPS.  
You must use a **Personal Access Token (PAT)** (or SSH keys) instead of your GitHub password.

### How to fix it (use a PAT)

1. **Create a Personal Access Token (PAT)** on GitHub:  
   - Go to: `GitHub → Settings → Developer settings → Personal access tokens`  
   - Choose **Tokens (classic)**  
   - Click **Generate new token**  
   - Give it a note (e.g. `Git on my PC`)  
   - Select at least the `repo` scope  
   - Generate and copy the token (you won’t see it again)

2. **Push again from the terminal:**

   ```bash
   git push origin main
   ```

3. When prompted:

   ```text
   Username for 'https://github.com': your-username
   Password for 'https://your-username@github.com':
   ```

   - Enter your **GitHub username** as usual  
   - Paste your **PAT** where it asks for the password

Git may offer to remember these credentials on your machine — that’s usually safe on a personal computer.

---

## 5. `src refspec main does not match any`

**Typical error:**

```text
error: src refspec main does not match any
error: failed to push some refs to 'https://github.com/username/repo.git'
```

### Common causes

1. You don’t have a local branch called `main`  
2. You have no commits on `main` yet  
3. Your current branch is `master` (or something else), not `main`

### How to diagnose

Check your branches:

```bash
git branch
```

You’ll see something like:

```text
* master
```

or:

```text
* main
  feature-branch
```

### How to fix it

#### Option A — Push the branch you’re actually on

If `git branch` shows:

```text
* master
```

then run:

```bash
git push origin master
```

instead of `main`.

#### Option B — Rename `master` to `main` (optional)

If you want to use `main` instead of `master`:

```bash
git branch -m master main
git push -u origin main
```

> Note: Only do this if you know no one else is depending on the old branch name.

#### Option C — Make an initial commit

If you have no commits, Git has nothing to push

1. Create or edit a file  
2. Stage and commit:

   ```bash
   git add .
   git commit -m "Initial commit"
   git push origin main
   ```

---

## 6. `'origin' does not appear to be a git repository`

**Error:**

```text
fatal: 'origin' does not appear to be a git repository
fatal: Could not read from remote repository.
```

### What it means

The remote named `origin` is not set, or it’s set to something invalid.

### How to check your remotes

```bash
git remote -v
```

- If you see nothing → no remotes are configured
- If `origin` exists but the URL is wrong, you’ll need to update it

### How to fix it

#### Add a new remote

Replace `USERNAME` and `REPO` with your GitHub details:

```bash
git remote add origin https://github.com/USERNAME/REPO.git
git push -u origin main
```

#### Or update the existing remote

If `origin` is present but incorrect:

```bash
git remote set-url origin https://github.com/USERNAME/REPO.git
git push -u origin main
```

---

## 7. `repository not found` (404-type errors)

**Typical error:**

```text
fatal: repository 'https://github.com/username/wrong-repo.git/' not found
```

### Common causes

- The repository name is misspelled  
- The repository is private and you don’t have access  
- You’re using the wrong username (e.g. old account name)  

### How to fix it

1. In your browser, go to the repo URL directly:

   ```text
   https://github.com/USERNAME/REPO
   ```

2. Confirm:
   - The repository exists  
   - The name matches exactly (case-sensitive)  
   - It’s under the correct GitHub account

3. Update your remote URL if needed:

   ```bash
   git remote set-url origin https://github.com/USERNAME/CORRECT_REPO.git
   git push -u origin main
   ```

---

## 8. `permission denied (publickey)` (SSH issues)

**Error:**

```text
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.
```

### What it means

You’re using SSH (`git@github.com:...`) and GitHub is expecting a valid SSH key, but:

- No key is installed  
- The key is not added to your GitHub account  
- The wrong key is being used

### Basic fixes

If you don’t want to handle SSH keys right now, you can switch to using a PAT which we cover in [Section 4](#4-password-authentication-is-not-supported-for-git-operations).

Or you can set up an SSH key, which will be covered in a separate guide.

---

## 9. Summary: A Safe Push Workflow

Here’s a reliable sequence you can follow when working with Git and GitHub:

```bash
# 1. Check where you are
pwd        # or 'cd' on Windows to see current directory
git status # should NOT say "not a git repository"

# 2. See which branch you're on
git branch

# 3. Stage and commit changes
git add .
git commit -m "Describe your change"

# 4. Push to the correct branch
git push origin main    # or 'master', depending on your branch name
```

If something goes wrong, match the error you see with the sections in this guide.

---
