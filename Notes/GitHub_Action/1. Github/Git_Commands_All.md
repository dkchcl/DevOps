Here’s a comprehensive list of commonly used Git commands categorized by purpose:

---

### **Setup and Configuration**

```bash
git config --global user.name "Your Name"               # Set your username
git config --global user.email "your_email@example.com" # Set your email
git config --list                                       # List all configurations
git config --global core.editor "code --wait"           # Set VS Code as the default editor
```

---

### **Repository Initialization**

```bash
git init                                # Initialize a new repository
git clone <repository_url>              # Clone a remote repository
```

---

### **Basic Commands**

```bash
git status                              # Show the status of the working directory
git add <file>                          # Stage a specific file
git add .                               # Stage all changes
git commit -m "Commit message"          # Commit staged changes with a message
git log                                 # Show commit history
git show <commit_hash>                  # Show details of a specific commit
```

---

### **Branch Management**

```bash
git branch                              # List all branches
git branch <branch_name>                # Create a new branch
git checkout <branch_name>              # Switch to a branch
git checkout -b <branch_name>           # Create and switch to a new branch
git merge <branch_name>                 # Merge a branch into the current branch
git branch -d <branch_name>             # Delete a branch
```

---

### **Remote Repositories**

```bash
git remote -v                           # Show remote repositories
git remote add origin <url>             # Add a new remote repository
git push -u origin <branch_name>        # Push changes to a remote branch
git pull                                # Fetch and merge changes from a remote repository
git fetch                               # Fetch changes from a remote repository
```

---

### **Stashing and Cleaning**

```bash
git stash                               # Stash changes in the working directory
git stash list                          # List stashed changes
git stash apply                         # Apply stashed changes
git stash drop                          # Delete a stash
git clean -f                            # Remove untracked files
```

---

### **Tagging**

```bash
git tag                                 # List all tags
git tag <tag_name>                      # Create a new tag
git tag -a <tag_name> -m "Message"      # Create an annotated tag
git push origin <tag_name>              # Push a tag to a remote repository
```

---

### **Undoing Changes**

```bash
git checkout -- <file>                  # Discard changes in a file
git reset <file>                        # Unstage a file
git reset --soft <commit_hash>          # Undo commits but keep changes staged
git reset --mixed <commit_hash>         # Undo commits and unstage changes
git reset --hard <commit_hash>          # Undo commits and discard all changes
git revert <commit_hash>                # Create a new commit that undoes a specific commit
```

---

### **Advanced Commands**

```bash
git rebase <branch_name>                # Reapply commits on top of another branch
git cherry-pick <commit_hash>           # Apply a specific commit to the current branch
git bisect                              # Find the commit that introduced a bug
git blame <file>                        # Show the commit that last modified each line of a file
git diff                                # Show changes between commits or working directory
```

---

### **Collaboration**

```bash
git push                               # Push changes to the remote repository
git pull                               # Pull changes from the remote repository
git fetch                              # Fetch changes without merging
git rebase <branch_name>               # Reapply commits on top of the fetched changes
```

---

### **Miscellaneous**

```bash
git archive                            # Create an archive of files
git shortlog                           # Summarize git log output
git describe                           # Describe a commit using tags
git ls-tree <branch_name>              # List files in a branch
git cat-file -p <hash>                 # Show the content of a blob, tree, or commit
```

Would you like explanations or examples for any specific commands?

**Git commands with detailed explanations and examples:**

---

### **Setup and Configuration**

#### `git config`

* Configure user details and other preferences.
* Example:

  ```bash
  git config --global user.name "Dinesh Chauhan"
  git config --global user.email "dinesh@example.com"
  ```

  These commands set your name and email globally, meaning they apply to all repositories.

#### `git config --list`

* Displays all configurations.
* Example:

  ```bash
  git config --list
  ```

  Output:

  ```
  user.name=Dinesh Chauhan
  user.email=dinesh@example.com
  ```

---

### **Repository Initialization**

#### `git init`

* Creates a new Git repository.
* Example:

  ```bash
  mkdir my_project
  cd my_project
  git init
  ```

  Output:

  ```
  Initialized empty Git repository in /path/to/my_project/.git/
  ```

#### `git clone`

* Clone an existing repository.
* Example:

  ```bash
  git clone https://github.com/example/repo.git
  ```

  This copies the repository to your local system.

---

### **Tracking and Committing Changes**

#### `git add`

* Stages files for commit.
* Example:

  ```bash
  git add file.txt
  git add .
  ```

  `file.txt` is staged for commit, and `.` stages all changes.

#### `git commit`

* Saves staged changes in the repository.
* Example:

  ```bash
  git commit -m "Added feature X"
  ```

  This records changes with a message.

#### `git status`

* Shows the status of your working directory.
* Example:

  ```bash
  git status
  ```

  Output:

  ```
  On branch main
  Changes to be committed:
    new file:   file.txt
  ```

#### `git log`

* Displays commit history.
* Example:

  ```bash
  git log
  ```

  Output:

  ```
  commit a1b2c3d4
  Author: Dinesh Chauhan <dinesh@example.com>
  Date:   Sat Jun 29 2025
      Added feature X
  ```

---

### **Branch Management**

#### `git branch`

* Lists, creates, or deletes branches.
* Example:

  ```bash
  git branch
  git branch feature-branch
  git branch -d feature-branch
  ```

  Output for `git branch`:

  ```
  * main
    feature-branch
  ```

#### `git checkout`

* Switches branches or restores files.
* Example:

  ```bash
  git checkout feature-branch
  git checkout -b new-feature
  ```

  This switches to `feature-branch` or creates and switches to `new-feature`.

#### `git merge`

* Merges another branch into the current branch.
* Example:

  ```bash
  git merge feature-branch
  ```

  This combines `feature-branch` into the current branch.

---

### **Remote Repositories**

#### `git remote`

* Manages remote repository connections.
* Example:

  ```bash
  git remote add origin https://github.com/example/repo.git
  git remote -v
  ```

  Output:

  ```
  origin  https://github.com/example/repo.git (fetch)
  origin  https://github.com/example/repo.git (push)
  ```

#### `git push`

* Sends commits to a remote repository.
* Example:

  ```bash
  git push -u origin main
  ```

#### `git pull`

* Fetches and merges changes from a remote repository.
* Example:

  ```bash
  git pull origin main
  ```

#### `git fetch`

* Fetches changes from a remote repository without merging.
* Example:

  ```bash
  git fetch origin
  ```

---

### **Undoing Changes**

#### `git reset`

* Unstages or resets changes.
* Example:

  ```bash
  git reset file.txt
  git reset --soft HEAD~1
  git reset --hard HEAD~1
  ```

  * `soft`: Keeps changes staged.
  * `hard`: Discards all changes.

#### `git checkout -- <file>`

* Discards changes in a file.
* Example:

  ```bash
  git checkout -- file.txt
  ```

#### `git revert`

* Creates a new commit to undo a specific commit.
* Example:

  ```bash
  git revert <commit_hash>
  ```

---

### **Stashing**

#### `git stash`

* Temporarily saves changes.
* Example:

  ```bash
  git stash
  git stash list
  git stash apply
  git stash drop
  ```

---

### **Tagging**

#### `git tag`

* Marks specific commits.
* Example:

  ```bash
  git tag v1.0
  git tag -a v1.0 -m "Version 1.0"
  git push origin v1.0
  ```

---

### **Viewing Changes**

#### `git diff`

* Shows differences between versions.
* Example:

  ```bash
  git diff
  git diff HEAD~1 HEAD
  ```

#### `git blame`

* Shows who modified each line of a file.
* Example:

  ```bash
  git blame file.txt
  ```

---

