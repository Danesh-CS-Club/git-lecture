# 🧭 An Introduction to Git

---

## 🏁 Initialization

**Command:** `git init`
**Parameters:** _None_
**Description:** Initializes a new Git repository with the default branch name.
**Use Case:** When starting a new project or converting an existing folder into a Git repository.

---

## 📋 Checking Repository Status

**Command:** `git status`
**Parameters:** _None_
**Description:** Displays the state of the working directory and the staging area.
**Use Case:** See which files are modified, staged, or untracked.

---

## 📂 Staging and Committing

### 1. Add Files

**Command:** `git add <file>`
**Parameters:**
- `<file>` — specific file name or use `.` to add all changes
**Description:** Adds files to the staging area (prepares them for commit).
**Use Case:** Use before committing to include changes in the next snapshot.

---

### 2. Commit Changes

**Command:** `git commit <params> -m "<message>"`
**Parameters:**
- `-m "<message>"` — adds a message describing the commit
**Description:** Commits staged files and records a snapshot of your project.
**Use Case:** Save a stable point in your code history that you can revert to later.

---

### 3. View Commit History

**Command:** `git log`
**Alternative:** `git log --oneline --graph`
**Description:** Shows commit history, optionally as a compact visual graph.
**Use Case:** Review the project’s change history or find specific commits.

---

## 🌿 Branching

**Command:** `git branch <params> <name>`
**Parameters:**
- No params — create a new branch
- `-b` — create and switch to the branch automatically
- `-m old new` — rename a branch
**Description:** Manages branches within your repository.
**Use Case:** Isolate development for new features, fixes, or experiments.

---

## 🔁 Switching and Checkout

**Command:** `git checkout <hash | commit-id>`
**Description:** Switches to a specific commit, branch, or tag.
**Use Case:** View or work from a specific state of the code.

---

## 🌐 Remote Repositories

### 1. Add Remote

**Command:** `git remote add <origin-name> <url>`
**Description:** Links your local repo to a remote one (e.g., GitHub).
**Use Case:** Sync your code with a remote server for collaboration or backup.

---

### 2. Push Changes

**Command:**
- `git push -u <origin> <branch>`
- `git push --set-upstream` (alternative form)
**Description:** Uploads commits from local to remote.
**Use Case:** Push your local commits online and set the default tracking branch.

---

### 3. Pull Changes

**Command:** `git pull`
**Description:** Fetches and merges changes from the remote repository.
**Use Case:** Update your local repo with remote changes.
**Extra:** You can specify `git pull origin main` to pull from a specific branch.

---

### 4. Fetch Changes

**Command:** `git fetch`
**Description:** Downloads objects and refs from another repository without merging.
**Use Case:** Update local knowledge of remote branches without changing your working files.
**Difference from pull:** `pull = fetch + merge`

---

## 🔀 Merging and Rebasing

### 1. Merge

**Command:** `git merge <branch>`
**Description:** Combines another branch into the current one.
**Use Case:** Safely integrate finished work or features.
**Note:** Merge keeps all commit history intact.

---

### 2. Rebase

**Command:** `git rebase <branch>`
**Description:** Reapplies commits on top of another branch (rewriting history).
**Use Case:** Clean up local commit history before merging to main.
**Tip:**
- Merge = additive (preserves history)
- Rebase = reconstructive (rewrites it)
**After conflicts:** Use `git rebase --continue`

---

## 🕹 Resetting and Reverting

### 1. Reset

**Command:** `git reset [--soft | --mixed | --hard] <commit>`
**Description:** Resets your branch to a specific commit.
**Use Cases:**
1. **Soft:** Uncommit but keep changes staged.
2. **Mixed:** Uncommit and unstage changes.
3. **Hard:** Completely discard commits and changes.

---

### 2. Revert

**Command:** `git revert <commit>`
**Description:** Creates a new commit that undoes changes from a previous one while keeping history intact.
**Use Case:** Safely undo a commit in public repositories.
**Tip:** Use `git revert --continue` after resolving conflicts.

---

## 🧳 Stashing

**Command:** `git stash`
**Additional Commands:**
- `git stash list` — view saved stashes
- `git stash apply {stash}` — reapply a stash
**Description:** Temporarily saves uncommitted changes.
**Use Case:** Switch tasks without committing incomplete work.

---

## 🧠 Writing Proper Commit Messages

**Guideline:**
Ask yourself — _“If added to the codebase, this code will ___.”_

**Tips:**
- Write in **imperative mood** (e.g., “Add feature X”, “Fix login bug”)
- Keep it short but descriptive

**Examples:**
✅ `Add API authentication middleware`
❌ `Added API authentication middleware`

---

## 📎 References

- **YouTube Tutorial:** [Git Basics Explained](https://www.youtube.com/watch?v=yTFC_MvwJvQ)
- **Topics to Review:**
  - `git fetch` (see above)
  - `git reset` vs `git revert`
  - Common Git parameters and commit message conventions
