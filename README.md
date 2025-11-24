# Git Command Reference Guide

---

Terminology used:

- `origin`: the default name git gives to the remote repository you cloned from (origin = <https://github.com/>...)

- `tracked`: when `git add` is used

- `staged`: when `git commit` is used

- `linear`: meaning commits follow a linear pattern like `A -- B -- C -- D`

- `non-linear`: meaning commits don't follow a linear order
  
```
A -- B -- C
      \ 
       D -- E
            \
             M   (merge commit)
```

<img width="800" height="330" alt="image" src="https://github.com/user-attachments/assets/69759b01-1250-4f07-9e6e-df501f066465" />


## How to write good commits:

When applied, this commit with \_\_\_.

Try and explain everything you do in this format, if its clear and makes the commit!

## 1. Repository Initialization

### 1.1 Initialize Repository

**Command:** `git init`

**Parameters:**

- `--initial-branch`: sets the initial branch in a newly created repository

**Description:**

Creates an empty git repository - basically a `.git` directory with sub-directories.

---

## 2. Basic Operations

### 2.1 Check Status

**Command:** `git status`

**Parameters:** _NONE_

**Description:**

Shows the difference between the staged area and working directory (the HEAD commit and the index file)

**Use Case:**

See modified, staged, and untracked files. 
Whats staged but not committed?

### 2.2 View Changes

**Command:** `git diff`

**Parameters:**

- `--staged` is staged changes that have not yet been committed.
- `-w` ignore the white spacce

**Description:**

Compared the changes made in your working directory to the staged directory.

**Use Case:**

Whats changed but not staged?


**Command:** `git show`

**Parameters:**
- _HASH ID_

**Description:**

Show changes made in a commit

---

## 3. Staging and Committing

### 3.1 Tracking Files

**Command:** `git add <file>`

**Parameters:**

- `-p` / `--patch` hunks specific code to add them to the index. Gives you a chance to review the difference before adding modified contents to the index.

**Description:**

Adds files to be tracked.

### 3.2 Commit Changes

**Command:** `git commit`

**Parameters:**

- _NONE_ an interactive environment, allows for setting long-descriptions by using an empty space
- `-m "<message>"` adds a message describing the commit
- `-a "<message>"` does a `git add .` and provides an interactive environment.
- `-am "<message>"` just like above but also does a `git add .`
- `-p` exactly like `git add -p` just remember not to do a `git add` before
- `--amend` allows you to edit commit message, and adds the most recent changes to your latest commit

**Description:**

Commits staged files and records a snapshot of the project.

A git commit should only be selective and include relevant changes

**Use Case:**

Saving a stable point, to revert back to in the future.

### 3.3 View Commit History

**Command:** `git log`

**Parameters:**

- `--oneline` exactly what the name says (keeps simplicity by including commit hash and message)
- `--graph` graphs logs in a horizontal format
- `--oneline --graph` a simplified graph
- `-p` logs actual changes in a file
- `--no-merges` removes the merge commits
- `--decorate` decorates with merge commits, branches, tags
- `--parents` shows parents of each commit

for (commit/s) filters:

- `--grep` for message
- `--after` and `--before` for dates
- `--author` by the author
- `--` for a specific file

to compare:
`git log feature/login..main` all commits that are in main but not in feature/login

**Description:**

Shows a timeline of project changes and commits.

---

## 4. Branching

### 4.1 Manage Branches

**Command:** `git branch`

**Parameters:**

- _NONE_ creates a new branch
- `-a` shows all the branches
- `-m` renames a branch
- `branch/subbranch` adds sub-branches

**Description:**

Managing branches in a repository

Long-running branches are branches that have been in the complete life-cycle. You mirror this structure (used for releasing code)

Short-lived branches for new features, bug fix and refactoring

### 4.2 Switch Branches

**Command:** `git checkout`

**Parameters:**

`<hash | commit id>` checkout to a specific hash
`<branch>` checkout a branch
`<tags>` checkout to a tag
- `-b` creates a branch and switches automatically

**Description:**

Switch to a commit, branch, or tag.

---

## 5. Remote Repositories

### 5.1 Add Remote

**Command:** `git remote add`

**Parameters:**

`<origin-name> <url>`

**Description:**

Links your local repository to a remote one

**Use Case:**

### 5.2 Fetch Changes

**Command:** `git fetch`

**Parameters:**

`--depth` to set how deep its history will go

**Description:**

Downloads objects and refs from a remote without merging

**Use Case:**

Check for updates but don't touch my files.

```
git fetch origin
git log main..origin/main
```

### 5.3 Pull Changes

**Command:** `git pull`

**Parameters:**

`<origin> <branch>`
`--rebase` solve merge conflicts, meaning git will first pull changes, then reapply your unpushed commits on top of the latest version of the remote branch (no need to merge).

**Description:**

Acts exactly like fetch but also merges (or rebase) the two repositories

### 5.4 Push Changes

**Command:** `git push`

**Parameters:**

`<origin> <branch>`
`--set-upstream` / `-u` flags a local branch to a remote branch. (acts more as a setting option, set it once and forget about it, it links your `branch` to the `origin/branch`)
`--tags` push all the tags

**Description:**

Uploads the local repository with the staged changes to the remote

---

## 6. Integrating Changes

### 6.1 Merge Branches

**Command:** `git merge`

**Parameters:**

- `<branch>` specifies the branch to merge from
- `--no-ff` prevents git from making a linear history (no-fast-forward)

**Description:**

Combines two branches into one

**Use Case:**

Merge is additive meaning history is preserved.

**Fast forwarding:**

In the terminology, i mentioned that we have two types of repositories, linear and non-linear. This same concept can be applied to git merge, a linear merge will have all the commits after the commit, otherwise it git will keep the current branch and make a new commit with the branch creating a non-linear history. 

This is useful when we have a collection of closely related branches.

### 6.2 Rebase

**Command:** `git rebase`

**Parameters:**

`<branch>` specifies the branch to rebase from``
`-i` provides an interactive setup for rebasing

**Description:**

Reapplies commits on top of another branch.

**Use Case:**

Clean up local commit history. Rebase is reconstructive meaning history is rewritten.

### 6.3 Cherry-pick

**Command:** `git cherry-pick`

**Parameters:**

`<commit-hash>` the hash of the commit you want to cherry pick

`<hash1> <hash2> <hash3>` / `A..B` for selecting multiple hashes

**Description:**

Copies a specific commit from one branch and applies it onto the current branch. Notes that it duplicates commits.

**Use Case:**

When you've mistakenly committed to the wrong branch you use cherry-pick to revert.

---

## 7. Undoing Changes

### 7.1 Reset

**Command:** `git reset`

**Parameters:**

`--hard` completely discards commits and changes.
`--soft` uncommit changes but keep them staged (moves HEAD back to a previous commit).
`--mixed` uncommit and unstage changes.
`<commit>` you can also do some cool stuff like `HEAD~1` meaning last commit from head

**Description:**

Resets branch to a specific commit

**Use Case:**

You committed too early or made a typo in the message.

### 7.2 Revert

**Command:** `git revert`

**Parameters:**

`<commit-hash>` the hash of the commit
`-n` tells git only to look at the changes

**Description:**

Creates a new commit that undoes changes from a previous one while keeping history intact.

**Use Case:**

You pushed a commit that breaks stuff, you cant change history so you revert it instead.

---

## 8. Temporary Storage

### 8.1 Stash Changes

**Command:** `git stash`

**Parameters:**
`-p` stash only some files
`list` view saved stashes
`apply {stash}` reaply a stash

**Description:**
Temporarily saves uncommitted changes.

**Use Case:**
You've made new changes yet need to prioritize something new, without committing save your code and commit later.

---

## 9. Conflict Resolution

### 9.1 Merge Tool

**Command:** `git mergetool`

**Parameters:** _NONE_

**Description:**

Launches a graphical or diff tool to help resolve merge conflicts.

---

## 10. Recovery and History

### 10.1 Reference Log

**Command:** `git reflog`

**Parameters:** _NONE_

**Description:**

Acts as gits "undo history", meaning even if you have rebased or reset you can see where your branch used to point

**Use Case:**

You mistakenly delete a branch, you can use reflog to get the hash and checkout back to it

```
git checkout def5678
git reset --hard def5678
```

---

## 11. Submodules

### 11.1 Manage Submodules

**Command:** `git submodule`

**Parameters:**

`add <repository>` self explanatory
`update --remote` pull all the latest versions of the submodules

**Description:**

A git repository inside another git repository.

FYI: when others clone your repo they should also initialize your submodules with `submodule init` or `clone --recurse-submodules`

Also submodules track commits and not branches (meaning when you clone a repository it goes to the exact commit at where the submodules was added, yet in web based github it opts to look at the default branch)

**Use Case:**

When wanting to use other repositories in your current repository you can have it set as a submodule

---

## 12. Working Trees

### 12.1 Manage Worktrees

**Command:** `git worktree`

**Parameters:**

`list` shows all the worktrees
`remove ../` removes a worktree
`add ../ -b new-branch` adds a worktree

**Description:**

Allows for having multiple working directories for a single git repository. It allows for multiple workspaces in the same repository.

**Use Case:**

You want to work on multiple branches without having to switch all the time

---

## 13. Configuration

### 13.1 Configure Git

**Command:** `git config`

**Parameters:**

`--global alias.l "log --oneline --graph"`

**Use Case:**
Easily set aliases for commands you use all the time but don't want to type out the whole name

---

## 14. Tagging

### 14.1 Manage Tags

**Command:** `git tag`

**Parameters:**

_NONE_ lists all the tags
`v1.0` a pointer to the latest commit
`v1.0 <hash>` to a commit in the past
`-a v1.0 -m "<message>"` includes metadata

**Description:**

A git tag is a pointer to a specific commit in git.

**Use Case:**

Acts like a sticky note like releases and milestones. They don't move after they're created.

---

## 15. Cleaning

### 15.1 Clean Untracked Files

**Command:** `git clean`

**Parameters:**

`-n` show only what would be deleted
`-f` actually delete the files

**Description:**
Removes untracked files from your currently working directory

**Use Case:**
Remove artifacts, temp files, and debug outputs.

---

## 16. Cloning

### 16.1 Clone Repository

**Command:** `git clone`

**Parameters:**

`--depth`: add depth for the history of the repository

**Description:**
Cloning a repository

---

## 17. Bisect

### 17.1 Bisect Commits

**Command:** `git bisect`

**Parameters:**

`start` start the bisect
`bad` mark the bad comit
`good <commit>` mark the good commit
`reset` finish when the bisect is done

**Description:**
Helps you find a specific commit that introduced a bug in the code using binary search.

---
