# How to Combine Multiple Git Repositories Into One (With Full History)

This guide explains how to merge multiple independent Git repositories into a **single parent repository**, while keeping **all past commits, authors, and timestamps**.

No frameworks assumed. Works for any project.

---

## Problem

You have:

* Multiple standalone Git repositories
* You want **one parent repo**
* Each old repo should live in its **own folder**
* **Commit history must be preserved**
* Root files (README, homepage, config) must stay separate

---

## Solution Overview

Use **`git subtree`**.

Why:

* Imports a repo into a folder
* Preserves full history
* Avoids merge conflicts
* Keeps root clean

---

## Step 1: Create Parent Repository

```bash
git init parent-repo
cd parent-repo
```

Add root files (README, homepage, config), then:

```bash
git add .
git commit -m "Initial root commit"
```

> This initial commit is required.

---

## Step 2: Add Old Repositories as Remotes

```bash
git remote add repo1 <repo-1-url>
git remote add repo2 <repo-2-url>

git fetch repo1
git fetch repo2
```

Remote names are just labels.

---

## Step 3: Import Each Repo Into Its Own Folder

⚠️ Target folders must **not exist** before this step.

```bash
git subtree add --prefix=repo-1-folder repo1 main
git subtree add --prefix=repo-2-folder repo2 main
```

This:

* Copies all commits
* Places files inside folders
* Keeps root untouched

---

## Step 4: Shared Assets (Plain HTML / No Framework)

Recommended:

* One shared `public/` or `assets/` folder at root
* Remove duplicate assets from subfolders

Path rules:

* Same folder → `file.ext`
* Shared assets → `../public/file.ext`
* No framework shortcuts

---

## Step 5: Verify History

Full history:

```bash
git log --oneline --graph --all
```

History per folder:

```bash
git log -- path/to/folder
```

If old commits appear → history is preserved.

---

## Step 6: Final Commit & Push

```bash
git add .
git commit -m "Finalize combined repository"
git push -u origin main
```

---

## Important Notes

* Deleting original repositories **does not remove history**
* Once commits are inside the parent repo, they are permanent
* Fetching from deleted repos is unnecessary
* `git subtree` is safer than manual merges for this use case

---

## When to Use This Approach

Use this when:

* You are consolidating projects
* You want clean structure
* You care about commit history
* You don’t want submodules

---

### Opinion

For repository consolidation, **`git subtree` is the cleanest and safest method**.

Done.
Got it.
Here is a **generic, reusable tutorial** (not project-specific).
You can paste this into **any root `README.md`**.

---

# How to Combine Multiple Git Repositories Into One (With Full History)

This guide explains how to merge multiple independent Git repositories into a **single parent repository**, while keeping **all past commits, authors, and timestamps**.

No frameworks assumed. Works for any project.

---

## Problem

You have:

* Multiple standalone Git repositories
* You want **one parent repo**
* Each old repo should live in its **own folder**
* **Commit history must be preserved**
* Root files (README, homepage, config) must stay separate

---

## Solution Overview

Use **`git subtree`**.

Why:

* Imports a repo into a folder
* Preserves full history
* Avoids merge conflicts
* Keeps root clean

---

## Step 1: Create Parent Repository

```bash
git init parent-repo
cd parent-repo
```

Add root files (README, homepage, config), then:

```bash
git add .
git commit -m "Initial root commit"
```

> This initial commit is required.

---

## Step 2: Add Old Repositories as Remotes

```bash
git remote add repo1 <repo-1-url>
git remote add repo2 <repo-2-url>

git fetch repo1
git fetch repo2
```

Remote names are just labels.

---

## Step 3: Import Each Repo Into Its Own Folder

⚠️ Target folders must **not exist** before this step.

```bash
git subtree add --prefix=repo-1-folder repo1 main
git subtree add --prefix=repo-2-folder repo2 main
```

This:

* Copies all commits
* Places files inside folders
* Keeps root untouched

---

## Step 4: Shared Assets (Plain HTML / No Framework)

Recommended:

* One shared `public/` or `assets/` folder at root
* Remove duplicate assets from subfolders

Path rules:

* Same folder → `file.ext`
* Shared assets → `../public/file.ext`
* No framework shortcuts

---

## Step 5: Verify History

Full history:

```bash
git log --oneline --graph --all
```

History per folder:

```bash
git log -- path/to/folder
```

If old commits appear → history is preserved.

---

## Step 6: Final Commit & Push

```bash
git add .
git commit -m "Finalize combined repository"
git push -u origin main
```

---

## Important Notes

* Deleting original repositories **does not remove history**
* Once commits are inside the parent repo, they are permanent
* Fetching from deleted repos is unnecessary
* `git subtree` is safer than manual merges for this use case

---

## When to Use This Approach

Use this when:

* You are consolidating projects
* You want clean structure
* You care about commit history
* You don’t want submodules

---
