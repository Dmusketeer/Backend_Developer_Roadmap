## Introduction to Git

Git is a distributed version control system that enables multiple people to work on a project simultaneously without overwriting each other's changes. It's widely used in software development for tracking changes in source code during software development. Here's a brief overview of its core concepts and features:

### Core Concepts

1. **Repository (Repo):** A repository is a storage space where your project lives. It can be local to your machine or a remote server.

2. **Commit:** A commit is a snapshot of your repository at a specific point in time. It's a way to save your progress with a descriptive message.

3. **Branch:** Branches allow you to work on different versions of a project simultaneously. The `main` branch is the default branch in a repository.

4. **Merge:** Merging is the process of combining changes from different branches into one branch.

5. **Clone:** Cloning means creating a copy of an existing repository.

6. **Pull:** Pulling means fetching the latest changes from a remote repository and merging them into your local repository.

7. **Push:** Pushing means sending your local repository changes to a remote repository.

8. **Remote:** A remote is a version of your project that is hosted on the internet or network somewhere.

### Basic Workflow

1. **Initialize a Repository:**
   ```bash
   git init
   ```

2. **Clone a Repository:**
   ```bash
   git clone <repository_url>
   ```

3. **Check Status:**
   ```bash
   git status
   ```

4. **Stage Changes:**
   ```bash
   git add <file_name>
   git add .
   ```

5. **Commit Changes:**
   ```bash
   git commit -m "Commit message"
   ```

6. **Create a Branch:**
   ```bash
   git branch <branch_name>
   ```

7. **Switch to a Branch:**
   ```bash
   git checkout <branch_name>
   ```

8. **Merge Branches:**
   ```bash
   git merge <branch_name>
   ```

9. **Pull Changes:**
   ```bash
   git pull
   ```

10. **Push Changes:**
    ```bash
    git push
    ```

### Git Cheat Sheet

Here's a concise cheat sheet with the most commonly used Git commands:

#### Setup and Config

- **Set Username:**
  ```bash
  git config --global user.name "Your Name"
  ```

- **Set Email:**
  ```bash
  git config --global user.email "you@example.com"
  ```

- **Check Configuration:**
  ```bash
  git config --list
  ```

#### Creating and Initializing

- **Initialize a Repository:**
  ```bash
  git init
  ```

- **Clone a Repository:**
  ```bash
  git clone <repository_url>
  ```

#### Staging and Committing

- **Check Status:**
  ```bash
  git status
  ```

- **Stage Files:**
  ```bash
  git add <file_name>
  git add .
  ```

- **Commit Changes:**
  ```bash
  git commit -m "Commit message"
  ```

#### Branching and Merging

- **List Branches:**
  ```bash
  git branch
  ```

- **Create a Branch:**
  ```bash
  git branch <branch_name>
  ```

- **Switch to a Branch:**
  ```bash
  git checkout <branch_name>
  ```

- **Merge Branches:**
  ```bash
  git merge <branch_name>
  ```

- **Delete a Branch:**
  ```bash
  git branch -d <branch_name>
  ```

#### Remote Repositories

- **Add Remote Repository:**
  ```bash
  git remote add origin <repository_url>
  ```

- **View Remotes:**
  ```bash
  git remote -v
  ```

- **Remove Remote:**
  ```bash
  git remote remove <name>
  ```

#### Pushing and Pulling

- **Push to Remote Repository:**
  ```bash
  git push origin <branch_name>
  ```

- **Pull from Remote Repository:**
  ```bash
  git pull origin <branch_name>
  ```

#### Miscellaneous

- **Show Commit History:**
  ```bash
  git log
  ```

- **Show Commit History with Graph:**
  ```bash
  git log --graph --oneline
  ```

- **Show Changes:**
  ```bash
  git diff
  ```


## Git Branching 

Learning Git branching is crucial for effective collaboration and version control in software development. Branching allows you to work on different features or fixes independently from the main codebase. Here’s an overview of Git branching concepts and commands, along with some practical exercises to help you master branching.

### Git Branching Concepts

1. **Branch:**
   A branch in Git is a lightweight movable pointer to one of these commits. The default branch name in Git is `main` (or `master` in older repositories).

2. **HEAD:**
   `HEAD` is a pointer that represents your current working directory. Typically, `HEAD` points to the latest commit on the current branch.

3. **Checkout:**
   Switching between branches is done using the `git checkout` command.

4. **Merge:**
   Merging is the process of integrating changes from one branch into another.

5. **Rebase:**
   Rebasing is the process of moving or combining a sequence of commits to a new base commit.

### Basic Branching Commands

#### Create and Switch Branches

- **Create a new branch:**
  ```bash
  git branch <branch_name>
  ```

- **List branches:**
  ```bash
  git branch
  ```

- **Switch to a branch:**
  ```bash
  git checkout <branch_name>
  ```

- **Create and switch to a new branch:**
  ```bash
  git checkout -b <branch_name>
  ```

#### Merging Branches

- **Merge a branch into the current branch:**
  ```bash
  git merge <branch_name>
  ```

#### Deleting Branches

- **Delete a branch:**
  ```bash
  git branch -d <branch_name>
  ```

- **Force delete a branch:**
  ```bash
  git branch -D <branch_name>
  ```

#### Rebasing

- **Rebase the current branch onto another branch:**
  ```bash
  git rebase <branch_name>
  ```

### Practical Exercises

#### Exercise 1: Basic Branching

1. **Initialize a Git repository:**
   ```bash
   git init my_project
   cd my_project
   ```

2. **Create a file and commit:**
   ```bash
   echo "Hello World" > file.txt
   git add file.txt
   git commit -m "Initial commit"
   ```

3. **Create and switch to a new branch:**
   ```bash
   git checkout -b feature_branch
   ```

4. **Make changes and commit in the new branch:**
   ```bash
   echo "Feature work" >> file.txt
   git add file.txt
   git commit -m "Added feature work"
   ```

5. **Switch back to the main branch:**
   ```bash
   git checkout main
   ```

6. **Merge the feature branch into the main branch:**
   ```bash
   git merge feature_branch
   ```

#### Exercise 2: Handling Conflicts

1. **Create a new branch and make conflicting changes:**
   ```bash
   git checkout -b conflicting_branch
   echo "Conflicting change" >> file.txt
   git add file.txt
   git commit -m "Made a conflicting change"
   ```

2. **Switch back to the main branch and make another conflicting change:**
   ```bash
   git checkout main
   echo "Another conflicting change" >> file.txt
   git add file.txt
   git commit -m "Made another conflicting change"
   ```

3. **Attempt to merge the conflicting branch into the main branch:**
   ```bash
   git merge conflicting_branch
   ```

4. **Resolve the merge conflicts by editing the file and then:**
   ```bash
   git add file.txt
   git commit -m "Resolved merge conflict"
   ```

#### Exercise 3: Rebasing

1. **Create a new branch and make changes:**
   ```bash
   git checkout -b rebase_branch
   echo "Rebase work" >> file.txt
   git add file.txt
   git commit -m "Work to be rebased"
   ```

2. **Switch back to the main branch and make changes:**
   ```bash
   git checkout main
   echo "Main branch work" >> file.txt
   git add file.txt
   git commit -m "Work on main branch"
   ```

3. **Rebase the feature branch onto the main branch:**
   ```bash
   git checkout rebase_branch
   git rebase main
   ```

### Visual Learning Tool

To better understand Git branching, you can use the interactive tool "Learn Git Branching," which provides visual and interactive exercises for mastering Git commands and concepts. You can access it at [Learn Git Branching](https://learngitbranching.js.org/).
