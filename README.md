# Git Command Guide: From Setup to Reflog

This repository contains a practical Git command reference. Use it as a learning guide for common Git workflows, from install/setup to troubleshooting with `git reflog`.

Git tracks changes to files in a repository. A repository usually contains a `.git` directory and a working directory of files. Commands are executed from a terminal and work by reading or writing Git metadata inside `.git`.

The format below explains each command with:

- What it does
- How it works
- When to use it
- Example

---

## 1. Setup and Global Configuration

### `git config --global user.name "Your Name"`

- Description: Sets the author name for commits.
- How it works: Writes your name into the global Git configuration file.
- When to use: Before your first commit, or when changing your identity.
- Example:
  ```sh
  git config --global user.name "Alice Developer"
  ```

### `git config --global user.email "you@example.com"`

- Description: Sets the author email for commits.
- How it works: Stores your email in the global configuration file.
- When to use: Before making commits.
- Example:
  ```sh
  git config --global user.email "alice@example.com"
  ```

### `git config --global init.defaultBranch main`

- Description: Sets the default branch name to `main` for new repositories.
- How it works: Changes Git’s default initial branch naming behavior.
- When to use: When you prefer `main` over `master`.
- Example:
  ```sh
  git config --global init.defaultBranch main
  ```

### `git config --list`

- Description: Lists all current Git configuration values.
- How it works: Reads the local, global, and system config files and prints them.
- When to use: To inspect your Git setup.
- Example:
  ```sh
  git config --list
  ```

### `git --version`

- Description: Shows the installed Git version.
- How it works: Runs the Git binary and prints its version.
- When to use: To confirm Git is installed.
- Example:
  ```sh
  git --version
  ```

---

## 2. Creating and Cloning Repositories

### `git init`

- Description: Creates a new local Git repository.
- How it works: Creates a `.git` directory and starts Git tracking in the current folder.
- When to use: When starting a project from scratch.
- Example:
  ```sh
  mkdir project && cd project
  git init
  ```

### `git clone https://github.com/user/repo.git`

- Description: Copies an existing remote repository locally.
- How it works: Downloads the repository files and `.git` directory to your computer.
- When to use: When joining a project or starting work from an existing repo.
- Example:
  ```sh
  git clone https://github.com/user/repo.git
  ```

### `git clone -b feature-branch https://github.com/user/repo.git`

- Description: Clones a repository and checks out a specific branch.
- How it works: Downloads the project and selects the given branch.
- When to use: When you want to work from a branch from the start.
- Example:
  ```sh
  git clone -b feature-branch https://github.com/user/repo.git
  ```

---

## 3. Working with Changes

### `git status`

- Description: Shows the current state of your working directory and staged files.
- How it works: Compares the working tree with the index and the latest commit.
- When to use: Before committing or resolving file changes.
- Example:
  ```sh
  git status
  ```

### `git add file.txt`

- Description: Adds a file to the staging area.
- How it works: Moves a tracked or new file into Git’s staging area for the next commit.
- When to use: Before committing your changes.
- Example:
  ```sh
  git add app.py
  ```

### `git add .`

- Description: Adds all current file changes in the project to the staging area.
- How it works: Stages every file except files ignored by `.gitignore`.
- When to use: When you are ready to commit many files.
- Example:
  ```sh
  git add .
  ```

### `git restore file.txt`

- Description: Restores a file from the last commit or index.
- How it works: Reverts work-tree or staged changes to a known state.
- When to use: To discard a local edit or unstage a file.
- Example:
  ```sh
  git restore file.txt
  ```

### `git restore --staged file.txt`

- Description: Removes a file from the staging area while keeping its working changes.
- How it works: Moves the file back from the index to the working directory.
- When to use: If you accidentally staged a file before checking it.
- Example:
  ```sh
  git restore --staged file.txt
  ```

### `git rm file.txt`

- Description: Removes a file from Git and the working directory.
- How it works: Deletes the file from the repo and stages the deletion.
- When to use: When a file should be deleted from the project.
- Example:
  ```sh
  git rm old_script.py
  ```

### `git mv old.txt new.txt`

- Description: Renames or moves a file inside the repo.
- How it works: Performs a rename and stages the operation.
- When to use: When you want a tracked file rename recorded cleanly.
- Example:
  ```sh
  git mv old_name.txt new_name.txt
  ```

---

## 4. Committing

### `git commit -m "message"`

- Description: Records staged changes in a commit.
- How it works: Creates a new snapshot from the staged files and records the author/date/message.
- When to use: After staging changes and wanting to save them permanently in history.
- Example:
  ```sh
  git add README.md
  git commit -m "Add installation guide"
  ```

### `git commit --amend -m "new message"`

- Description: Changes the most recent commit message or contents.
- How it works: Rewrites the latest commit by replacing it with an amended version.
- When to use: When you need to fix a commit message or include missed files.
- Example:
  ```sh
  git add missing-file.txt
  git commit --amend -m "Add installation guide and missing file"
  ```

### `git commit -a -m "message"`

- Description: Stages tracked changes automatically and commits them.
- How it works: Adds tracked files that already exist in the repository and commits them.
- When to use: For fast commits without running `git add` manually.
- Example:
  ```sh
  git commit -a -m "Update configuration"
  ```

---

## 5. Viewing History and Differences

### `git log`

- Description: Lists commit history.
- How it works: Reads commit objects and prints the repository timeline.
- When to use: To review project history and discover what changed.
- Example:
  ```sh
  git log --oneline --graph --all
  ```

### `git show HEAD`

- Description: Shows the contents and metadata of the latest commit.
- How it works: Displays the commit object, files changed, and patch.
- When to use: To inspect a commit in detail.
- Example:
  ```sh
  git show HEAD
  ```

### `git diff`

- Description: Shows differences between working tree and index.
- How it works: Compares file contents and prints changes.
- When to use: Before staging, to review local edits.
- Example:
  ```sh
  git diff
  ```

### `git diff --staged`

- Description: Shows changes currently in the staging area.
- How it works: Compares the index against the last commit.
- When to use: Before committing staged changes.
- Example:
  ```sh
  git diff --staged
  ```

### `git diff branch1..branch2`

- Description: Shows differences between two branches.
- How it works: Compares the tree snapshots of the branches.
- When to use: To review what one branch has that another branch does not.
- Example:
  ```sh
  git diff main..feature
  ```

### `git blame file.txt`

- Description: Shows who last changed each line in a file.
- How it works: Reads line-by-line history from commit metadata.
- When to use: To identify authorship or origins of code.
- Example:
  ```sh
  git blame README.md
  ```

### `git grep "text"`

- Description: Searches tracked files for a string.
- How it works: Searches repository content and prints matching lines.
- When to use: To locate words, error text, or identifiers.
- Example:
  ```sh
  git grep "TODO"
  ```

---

## 6. Branching

### `git branch`

- Description: Lists local branches.
- How it works: Reads local branch pointers from `.git/refs/heads`.
- When to use: To see available branches.
- Example:
  ```sh
  git branch
  ```

### `git branch new-feature`

- Description: Creates a new branch named `new-feature`.
- How it works: Creates a pointer to the current commit.
- When to use: To start a feature without affecting the main branch.
- Example:
  ```sh
  git branch feature/login
  ```

### `git switch feature/login`

- Description: Switches to the named branch.
- How it works: Updates the working directory to reflect the branch commit snapshot.
- When to use: To move between branches.
- Example:
  ```sh
  git switch feature/login
  ```

### `git checkout feature/login`

- Description: Older command to switch branches or restore files.
- How it works: Changes the current branch or checks out files from a tree.
- When to use: In older workflows and scripts.
- Example:
  ```sh
  git checkout feature/login
  ```

### `git checkout -b feature/login`

- Description: Creates a new branch and switches to it.
- How it works: Creates a branch pointer and changes the current working branch.
- When to use: When beginning a new task.
- Example:
  ```sh
  git checkout -b feature/login
  ```

### `git branch -d feature/login`

- Description: Deletes a merged branch safely.
- How it works: Checks whether the branch is fully merged and removes the pointer.
- When to use: After a feature branch is merged.
- Example:
  ```sh
  git branch -d feature/login
  ```

### `git branch -D feature/login`

- Description: Force-deletes a branch.
- How it works: Removes the branch pointer even if the branch is not merged.
- When to use: When you are sure the branch is not needed.
- Example:
  ```sh
  git branch -D feature/login
  ```

---

## 7. Merging and Rebasing

### `git merge feature/login`

- Description: Combines the history of another branch into the current branch.
- How it works: Integrates the branch’s changes and creates a merge commit when needed.
- When to use: When you want to merge a finished feature branch into `main`.
- Example:
  ```sh
  git switch main
  git merge feature/login
  ```

### `git merge --no-ff feature/login`

- Description: Forces a merge commit even if Git can fast-forward.
- How it works: Creates an explicit merge commit instead of linear fast-forwarding.
- When to use: In teams that want a visible merge record.
- Example:
  ```sh
  git merge --no-ff feature/login
  ```

### `git rebase main`

- Description: Replays commits from the current branch on top of `main`.
- How it works: Moves a branch’s commits to a new base point.
- When to use: To keep a feature branch clean and up to date.
- Example:
  ```sh
  git switch feature/login
  git rebase main
  ```

### `git rebase -i HEAD~5`

- Description: Interactive rebase for editing, squashing, or rearranging recent commits.
- How it works: Opens the commit history for manual editing before replaying.
- When to use: To clean up Git history before pushing.
- Example:
  ```sh
  git rebase -i HEAD~5
  ```

---

## 8. Remotes

### `git remote -v`

- Description: Lists the configured remote repositories.
- How it works: Reads remote URLs from `.git/config`.
- When to use: To know where code is pushed or fetched.
- Example:
  ```sh
  git remote -v
  ```

### `git remote add origin https://github.com/user/repo.git`

- Description: Adds a remote named `origin`.
- How it works: Stores the repository URL in the local Git configuration.
- When to use: When creating a new repo or linking a clone to a server.
- Example:
  ```sh
  git remote add origin https://github.com/user/repo.git
  ```

### `git remote remove origin`

- Description: Removes a remote named `origin`.
- How it works: Deletes the URL mapping from Git config.
- When to use: To disconnect a repository from a remote server.
- Example:
  ```sh
  git remote remove origin
  ```

### `git remote set-url origin https://github.com/user/new-repo.git`

- Description: Updates the URL of a remote.
- How it works: Rewrites the remote URL in `.git/config`.
- When to use: When you moved the repository.
- Example:
  ```sh
  git remote set-url origin https://github.com/user/new-repo.git
  ```

---

## 9. Fetch, Pull, Push

### `git fetch origin`

- Description: Downloads new commits, branches, and tags from a remote without changing your working branch.
- How it works: Contacts the remote repository and updates remote-tracking refs.
- When to use: To inspect remote updates safely before merging.
- Example:
  ```sh
  git fetch origin
  ```

### `git pull origin main`

- Description: Fetches and merges the latest changes from a remote branch.
- How it works: Runs `fetch` followed by a `merge` or `rebase` depending on config.
- When to use: When you want your local branch to include remote updates.
- Example:
  ```sh
  git pull origin main
  ```

### `git push origin main`

- Description: Pushes local commits to the remote repository.
- How it works: Uploads your local branch commits to the remote branch server.
- When to use: After a commit is ready to share.
- Example:
  ```sh
  git push origin main
  ```

### `git push -u origin main`

- Description: Pushes the branch and sets the upstream tracking relationship.
- How it works: Uploads the branch and records the default branch to track.
- When to use: First push of a new branch.
- Example:
  ```sh
  git push -u origin main
  ```

### `git push --force-with-lease origin main`

- Description: Safely force-pushes a rewritten branch.
- How it works: Force-updates the remote branch only if the remote has not changed since your last fetch.
- When to use: After a clean `rebase` or `commit --amend`.
- Example:
  ```sh
  git push --force-with-lease origin main
  ```

---

## 10. Tags and Releases

### `git tag`

- Description: Lists tags in the repository.
- How it works: Reads tag pointers stored in Git.
- When to use: To view release names.
- Example:
  ```sh
  git tag
  ```

### `git tag v1.0.0`

- Description: Creates a lightweight tag or annotated tag named `v1.0.0`.
- How it works: Creates a reference to a specific commit.
- When to use: To mark version releases.
- Example:
  ```sh
  git tag v1.0.0
  ```

### `git tag -a v1.0.0 -m "Release 1.0.0"`

- Description: Creates an annotated Git tag with a message.
- How it works: Stores metadata and a message in tag object.
- When to use: When you need a descriptive release tag.
- Example:
  ```sh
  git tag -a v1.0.0 -m "Release 1.0.0"
  ```

### `git push origin v1.0.0`

- Description: Pushes a specific tag to a remote.
- How it works: Uploads the tag object and reference to the remote.
- When to use: When sharing a release tag.
- Example:
  ```sh
  git push origin v1.0.0
  ```

---

## 11. Stashing and Temporary Saves

### `git stash`

- Description: Saves uncommitted changes temporarily.
- How it works: Stores your working tree and index changes in a stash stack.
- When to use: To switch branches without committing incomplete work.
- Example:
  ```sh
  git stash
  ```

### `git stash list`

- Description: Lists saved stash entries.
- How it works: Reads the stash stack from Git refs.
- When to use: To inspect saved work.
- Example:
  ```sh
  git stash list
  ```

### `git stash pop`

- Description: Applies and removes the latest stash entry.
- How it works: Restores saved changes into the working directory and deletes the stash.
- When to use: To recover unfinished work.
- Example:
  ```sh
  git stash pop
  ```

### `git stash apply`

- Description: Applies a stash without deleting it.
- How it works: Restores the saved changes from a stash stack entry.
- When to use: When you want to keep the stash and apply it later.
- Example:
  ```sh
  git stash apply stash@{0}
  ```

---

## 12. Fixing Mistakes and Safely Recovering

### `git revert HEAD`

- Description: Creates a new commit that reverses the latest commit.
- How it works: Applies the inverse of the target commit.
- When to use: To undo a bad commit safely without rewriting history.
- Example:
  ```sh
  git revert HEAD
  ```

### `git reset --soft HEAD~1`

- Description: Moves the current branch back one commit while keeping changes staged.
- How it works: Moves the branch pointer backward and leaves content in the index.
- When to use: To undo a commit but keep the changes staged.
- Example:
  ```sh
  git reset --soft HEAD~1
  ```

### `git reset --mixed HEAD~1`

- Description: Moves the branch back one commit and unstages changes.
- How it works: Resets branch pointer and leaves working tree file edits as unstaged changes.
- When to use: To undo the latest commit and rework it.
- Example:
  ```sh
  git reset --mixed HEAD~1
  ```

### `git reset --hard HEAD~1`

- Description: Completely moves the repository back one commit.
- How it works: Resets branch pointer, index, and working tree to a previous snapshot.
- When to use: To discard commits and changes permanently.
- Example:
  ```sh
  git reset --hard HEAD~1
  ```

### `git clean -fd`

- Description: Removes untracked files and directories.
- How it works: Deletes files not tracked by Git.
- When to use: To clean a workspace before a build or after experimentation.
- Example:
  ```sh
  git clean -fd
  ```

### `git clean -fdx`

- Description: Removes untracked files including ignored files.
- How it works: Deletes ignored files and directories as well.
- When to use: To fully clean a directory.
- Example:
  ```sh
  git clean -fdx
  ```

---

## 13. Advanced Collaboration and History Rewriting

### `git cherry-pick <commit>`

- Description: Applies a specific commit from one branch to another.
- How it works: Copies the diff of one commit onto the current branch.
- When to use: To take one fix from another branch.
- Example:
  ```sh
  git cherry-pick abc123
  ```

### `git bisect start`

- Description: Begins a binary search to locate a bad commit.
- How it works: Uses good/bad checkpoints to find the first bad commit.
- When to use: To identify the commit that introduced a bug.
- Example:
  ```sh
  git bisect start
  git bisect bad
  git bisect good v1.0.0
  ```

### `git worktree add ../feature-demo feature/login`

- Description: Creates an additional working directory linked to another branch.
- How it works: Shares the same repository but checks out a different branch in another location.
- When to use: When you need to work on two branches at the same time.
- Example:
  ```sh
  git worktree add ../feature-demo feature/login
  ```

### `git archive --format=zip --output=release.zip main`

- Description: Creates a source archive of a branch or commit.
- How it works: Packages the selected tree into a zip or tar file.
- When to use: To create a deploy artifact or release package.
- Example:
  ```sh
  git archive --format=zip --output=release.zip main
  ```

---

## 14. Reflog and Recovery

### `git reflog`

- Description: Records every branch update, including commits, rebases, resets, and branch checkouts.
- How it works: Git writes local movement history to the `.git/logs/refs` and HEAD logs.
- When to use: To recover lost commits, find a previous branch position, or inspect accidental resets.
- Example:
  ```sh
  git reflog
  ```

### `git reflog --date=iso`

- Description: Shows reflog entries with ISO timestamps.
- How it works: Adds date information to each reflog record.
- When to use: When you need to understand when each Git movement happened.
- Example:
  ```sh
  git reflog --date=iso
  ```

### `git reflog --all`

- Description: Shows reflog entries for all refs in the repository.
- How it works: Reads local and all-branch movement logs instead of just the current branch.
- When to use: For full recovery context across branches.
- Example:
  ```sh
  git reflog --all
  ```

### `git reflog show HEAD`

- Description: Displays the reflog specifically for `HEAD`.
- How it works: Reads the branch’s head log entries.
- When to use: To find recent `HEAD` movements and recover a lost checkout or commit.
- Example:
  ```sh
  git reflog show HEAD
  ```

### Recover a lost commit with `git reflog`

- Description: Finds a lost commit hash and restores it by checking out or branching from the hash.
- How it works: Git’s reflog keeps old commit hashes even after they are no longer on the branch.
- When to use: After a hard reset, unintended rebase, or accidental branch deletion.
- Example:
  ```sh
  git reflog
  git switch -c recovered-branch abc123
  ```

### Recover after a mistaken reset with `git reflog`

- Description: Use reflog to walk back to the correct commit after a destructive reset.
- How it works: Reflog records the old `HEAD` before the reset.
- When to use: When you need to undo `git reset --hard`.
- Example:
  ```sh
  git reflog
  git reset --hard abc123
  ```

---

## 15. Practical Workflow Example

```sh
# 1. Configure Git
git config --global user.name "Alice Developer"
git config --global user.email "alice@example.com"

# 2. Create a repository
mkdir demo && cd demo
git init

# 3. Check repository status
git status

# 4. Create a file and stage it
echo "Hello Git" > hello.txt
git add hello.txt

# 5. Commit
git commit -m "Create hello.txt"

# 6. Create a branch
git switch -c feature/docs

# 7. Make changes
# edit README.md

git add README.md
git commit -m "Update documentation"

# 8. Merge branch back to main
git switch main
git merge feature/docs

# 9. Push to remote
git remote add origin https://github.com/user/demo.git
git push -u origin main

# 10. If needed, recover accidental changes using reflog
git reflog
```

---

## 16. Useful Daily Git Commands

```sh
git status
git add .
git commit -m "Improve feature"
git pull origin main
git push origin main
git log --oneline --graph --decorate --all
git branch
git switch main
git stash save "temporary work"
git reflog
```

---

## 17. Common Git Rules

1. Always check `git status` before committing.
2. Commit small, clear changes with descriptive messages.
3. Pull before pushing to avoid remote conflicts.
4. Use branches for features and fixes.
5. Use `git reflog` before destructive commands such as `reset --hard`.
6. Prefer `git revert` for public/shared history and `git reset` for local/private history.

This guide covers the typical Git lifecycle from setup to advanced commands such as `git rebase`, `git cherry-pick`, `git worktree`, and `git reflog`.
