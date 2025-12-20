# Git Commands

- Git is a free and open source distributed version control system.
- It is designed to handle everything from small to very large projects with speed and efficiency.

---

## 1. Setup & Configuration

- **Configure user information**:
  - Sets the name and email attached to your commit transactions.

```shell
> git config --global user.name "Your Name"
> git config --global user.email "your.email@example.com"
```

- **Check configuration**:

```shell
> git config --list
```

---

## 2. Getting & Creating Projects

- **Initialize a repository**:
  - Turns the current directory into a new Git repository.

```shell
> git init
```

- **Clone a repository**:
  - Creates a copy of a remote repository on your local machine.

```shell
> git clone [url]
```

---

## 3. Basic Snapshotting

- **Check status**:
  - Lists valid files with new content or modifications to be committed.

```shell
> git status
```

- **Add files to staging area**:
  - Adds files to the staging area to be included in the next commit.

```shell
> git add [file]       # Add specific file
> git add .            # Add all files
```

- **Commit changes**:
  - Records the changes in the staging area to the repository history.

```shell
> git commit -m "Commit message"
```

---

## 4. Branching & Merging

- **List branches**:
  - Lists all local branches in the current repository.

```shell
> git branch
> git branch -a        # List all branches (local + remote)
```

- **Create a branch**:

```shell
> git branch [branch-name]
```

- **Switch branches**:
  - Switches the working directory to the specified branch.

```shell
> git checkout [branch-name]
> git switch [branch-name]  # Updated command for switching
```

- **Create & switch**:

```shell
> git checkout -b [branch-name]
```

- **Merge branches**:
  - Merges the specified branch’s history into the current branch.

```shell
> git merge [branch-name]
```

- **Delete a branch**:

```shell
> git branch -d [branch-name]
```

---

## 5. Sharing & Updating

- **Add remote**:
  - Connects your local repository to a remote server.

```shell
> git remote add origin [url]
```

- **Push changes**:
  - Uploads all local branch commits to the remote repository.

```shell
> git push origin [branch-name]
> git push -u origin [branch-name]   # Set upstream for future pushes
```

- **Pull changes**:
  - Fetches and attempts to merge changes from the remote branch.

```shell
> git pull
```

- **Fetch changes**:
  - Downloads new history from the remote repository but doesn't merge.

```shell
> git fetch
```

---

## 6. Inspection & Comparison

- **View commit history**:

```shell
> git log
> git log --oneline     # Simplified log
```

- **View changes (Diff)**:
  - Shows differences between commits, commit and working tree, etc.

```shell
> git diff              # Changes in working directory
> git diff --staged     # Changes in staging area
```

---

## 7. Advanced Commands

- **Stashing**:
  - Temporarily stores modified, tracked files in order to change branches.

```shell
> git stash             # Save modified and staged changes
> git stash pop         # Apply stored stash and remove from stack
> git stash list        # List stack-order of stashed file changes
```

- **Rebase**:
  - Reapplies commits on top of another base tip.

```shell
> git rebase [branch-name]
```

- **Reset**:
  - Resets current HEAD to the specified state.

```shell
> git reset --soft [commit]   # Undo commit, keep changes staged
> git reset --hard [commit]   # Undo commit, discard changes
```

- **Cherry Pick**:
  - Apply the changes introduced by some existing commits.

```shell
> git cherry-pick [commit-hash]
```

- **Tagging**:
  - Mark specific points in history as important (e.g. releases).

```shell
> git tag [tag-name]
```

---

## 8. Ignoring Files (.gitignore)

- A `.gitignore` file specifies intentionally untracked files that Git should ignore.
- **Common usage**:
  - `__pycache__/`
  - `.env`
  - `node_modules/`
  - `*.log`

---

## 9. Undo Changes (Modern)

- **Restore working tree files**:
  - Discard changes in working directory (like `git checkout -- file`).

```shell
> git restore [file]
```

- **Unstage files**:
  - Remove files from staging area (like `git reset HEAD file`).

```shell
> git restore --staged [file]
```

---
