# Git Quick Start Guide

## Introduction to Git

### What is Git?
Git is a distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

### Why Use Git?
- **Version Control**: Track changes to your codebase over time.
- **Collaboration**: Work with others on the same codebase simultaneously.
- **Backup and Restore**: Easily revert to previous versions of your project.

### Basic Git Terminology
- **Repository**: A storage location for your project, containing all files and the history of changes.
- **Branch**: A separate line of development within a repository.
- **Commit**: A snapshot of your project at a specific point in time.
- **Merge**: Combining changes from different branches.
- **Rebase**: Reapplying commits on top of another base commit.
- **Stash**: Temporarily storing changes without committing them.
- **Fetch**: Downloading changes from a remote repository without applying them.

## Getting Started

### Installing Git
Follow the installation instructions for your operating system from the official Git website: [Git Downloads](https://git-scm.com/downloads)

### Configuring Git
Set up your Git environment with your user details:
```sh
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### Initializing a Git Repository
Set up a projects directory on your local machine:
```sh
mkdir projects
cd projects
```

## Cloning and Forking Repositories

### Cloning a Repository
Using HTTPS:
```sh
git clone https://github.com/username/repo_name.git
```

Using SSH:
```sh
git clone git@github.com:username/repo_name.git
```

### Creating and Pushing to a New Repository
```sh
mkdir repo_name
cd repo_name
git init
git remote add origin git@github.com:username/repo_name.git
git add .
git commit -m "Initial commit"
git push -u origin main
```

## Basic Git Commands

### Branch Management

#### Creating and Switching Branches
Create and switch to a new branch:
```sh
git switch -c feature_branch
```

Push the new branch to the remote and track it:
```sh
git push -u origin feature_branch
```

Switch to an existing remote branch:
```sh
git switch branch_name
```

Using `git checkout`:
```sh
git fetch origin
git checkout -b branch_name origin/branch_name
```

#### Deleting Branches
Delete a local branch:
```sh
git branch -d branch_name
```

Delete a remote branch:
```sh
git push origin --delete branch_name
```

### Comparing Changes

#### Between Branches
Compare changes between branches:
```sh
git diff main..feature_branch
```

#### Between Commits
Compare changes between commits:
```sh
git diff commit_hash1..commit_hash2
```

#### Between Current Branch and Another Branch
Compare changes between the current branch and another branch:
```sh
git diff branch_name
```

### Viewing Commit History and Details

#### Viewing Commit History
View the commit history:
```sh
git log
```

View a specific commit:
```sh
git show commit_hash
```

### Fetching Changes

#### Using `git fetch`
`git fetch` is used to download changes from a remote repository without applying them to your working directory. This is useful for reviewing changes before integrating them into your local repository.

1. **Fetching Changes**:
   ```sh
   git fetch
   ```

2. **Benefits of `git fetch`**:
   - **Safe Preview**: Fetching changes allows you to review updates from the remote repository without affecting your working directory.
   - **Conflict Prevention**: By fetching changes first, you can merge or rebase the updates more safely, reducing the risk of conflicts.
   - **Detailed Comparison**: `git fetch` provides an opportunity to compare your local branch with the remote branch to understand the differences before applying any changes.
   - **Granular Control**: Fetch changes for specific branches without updating all branches.

### Examples of `git fetch`

#### Scenario 1: Syncing with the Remote Repository
You’ve been working on a feature branch for a few days. Meanwhile, your team has made several changes to the `main` branch. Before you integrate these changes, you want to review them.

```sh
# Fetch the latest changes from the remote repository
git fetch

# Check the differences between your local main and the remote main
git diff main origin/main
```

#### Scenario 2: Fetching Changes for a Specific Branch
You’re only interested in the changes made to a specific branch, such as `develop`.

```sh
# Fetch the latest changes for the 'develop' branch only
git fetch origin develop

# Check the differences between your local develop and the remote develop
git diff develop origin/develop
```

#### Scenario 3: Listing All Remote Branches
You want to see all the branches available on the remote repository that you do not have locally.

```sh
# Fetch the latest changes and list all branches on the remote
git fetch
git branch -r
```

#### Scenario 4: Updating Tracking Branches without Merging
You want to update your tracking branches without merging changes into your working directory.

```sh
# Fetch the latest changes for all branches without merging
git fetch

# View changes in a specific branch
git log origin/feature_branch
```

#### Scenario 5: Rebasing a Feature Branch
You want to rebase your feature branch on top of the latest `main` branch without affecting your working directory initially.

```sh
# Fetch the latest changes
git fetch

# Rebase your feature branch onto the updated main branch
git switch feature_branch
git rebase origin/main
```

#### Scenario 6: Preparing for Merge Conflict Resolution
You suspect that there might be conflicts between your feature branch and the `main` branch. Fetch the latest changes to review and prepare for conflict resolution.

```sh
# Fetch the latest changes from the remote repository
git fetch

# Check for potential conflicts
git diff main origin/main

# Merge or rebase after reviewing the changes
git switch feature_branch
git merge origin/main
# OR
git rebase origin/main
```

### Merging and Rebasing

#### Merge Multiple Commits as a Single Commit
Squash merge a branch into the main branch:
```sh
git checkout main
git merge --squash feature_branch
```

#### Rebase a Branch
Rebase is a way of integrating changes from one branch into another. It rewrites the commit history by applying your changes on top of the base branch. This can create a cleaner, more linear commit history.

1. **When to Use `git rebase`**:
   - To keep a linear project history.
   - To integrate changes from the main branch into your feature branch before merging.

2. **Why Issues Arise with Rebase**:
   - **Conflicts**: When rebasing, you might encounter conflicts if the same lines of code were changed differently in the branches being rebased.
   - **History Rewriting**: Rebase rewrites commit history, which can be problematic if other developers are working on the same branch.

3. **Rebasing a Branch**:
   ```sh
   git switch feature_branch
   git pull --rebase origin main
   ```

4. **Resolve Conflicts (if any)**:
   - If conflicts occur, Git will pause rebasing and allow you to resolve the conflicts manually.
   - After resolving conflicts, continue the rebase process:
     ```sh
     git rebase --continue
     ```

5. **Set Rebase as the Default Behavior for `git pull`**:
   ```sh
   git config --global pull.rebase true
   ```

### Stashing Changes

#### Save and Retrieve Stashes
Save changes to a stash:
```sh
git stash save "Description of changes"
```

List stashes:
```sh
git stash list
```

Apply and remove stash:
```sh
git stash pop
```

Apply without removing:
```sh
git stash apply
```

### Tagging

#### Tagging for Releases
Tag the current commit:
```sh
git tag -a v1.0.1 -m "Release v1.0.1"
git push origin v1.0.1
```

### Cleaning Up

#### Remove Untracked Files and Directories

`git clean` is used to remove untracked files and directories from your working directory. Untracked files are those that are not being tracked by Git, meaning they are not staged for commit and are not part of the version history.

##### Why `git clean` is Useful:

1. **Cleaning Up the Working Directory**:
   - Over time, as you work on a project, you may create temporary files, build artifacts, or other files that are not meant to be committed to the repository. These files can clutter your working directory.
   - Running `git clean` helps you clean up these unwanted files and maintain a tidy working environment.

2. **Resetting the Working Directory to a Known State**:
   - If you are switching between branches or working on multiple features, you may want to ensure that your working directory is clean and free of any leftover files from previous work.
   - This is particularly useful before switching branches or starting a new feature, as it ensures that no untracked files interfere with your work.

3. **Ensuring Consistent Builds**:
   - In projects

 with build processes, leftover build artifacts from previous builds can sometimes cause issues. Running `git clean` before building ensures that only the necessary files are present, leading to consistent and reliable builds.

##### How to Use `git clean`:

1. **Dry Run**:
   - Before actually removing any files, you can perform a dry run to see which files would be removed.
   ```sh
   git clean -n
   ```

2. **Remove Untracked Files**:
   - To remove untracked files, use the `-f` (force) option. Git requires the force option to prevent accidental deletion of files.
   ```sh
   git clean -f
   ```

3. **Remove Untracked Directories**:
   - By default, `git clean` does not remove untracked directories. To remove untracked directories as well, use the `-d` option.
   ```sh
   git clean -fd
   ```

4. **Interactive Mode**:
   - You can also run `git clean` in interactive mode to selectively remove files. This is useful if you want to review each file before deleting it.
   ```sh
   git clean -i
   ```

### Examples

1. **Perform a Dry Run**:
   ```sh
   git clean -n
   ```
   Output:
   ```
   Would remove file1.txt
   Would remove temp/
   ```

2. **Remove Untracked Files**:
   ```sh
   git clean -f
   ```

3. **Remove Untracked Files and Directories**:
   ```sh
   git clean -fd
   ```

4. **Interactive Clean**:
   ```sh
   git clean -i
   ```
   - This will prompt you for each file or directory, allowing you to confirm whether to remove it.

### Resetting and Reverting

#### Reset to a Previous Commit
Hard reset to a specific commit:
```sh
git reset --hard commit_hash
```

Reset to the last commit:
```sh
git reset --hard
```

### Changing Remote URL

#### Change the Remote URL of a Branch
To change the URL of the remote repository your branch is tracking:
1. **View Existing Remotes**:
   ```sh
   git remote -v
   ```

2. **Set a New URL for the Remote**:
   ```sh
   git remote set-url origin new_url
   ```

3. **Verify the Change**:
   ```sh
   git remote -v
   ```

### Useful Commands

1. **Viewing Commit History**:
   ```sh
   git log
   ```

2. **Checking Status**:
   ```sh
   git status
   ```

3. **Adding Changes**:
   ```sh
   git add .
   ```

4. **Committing Changes**:
   ```sh
   git commit -m "Commit message"
   ```

5. **Pulling Changes from Remote**:
   ```sh
   git pull
   ```

6. **Pushing Changes to Remote**:
   ```sh
   git push
   ```

7. **Viewing Remote Repositories**:
   ```sh
   git remote -v
   ```

8. **Removing Files from Staging Area**:
   ```sh
   git reset HEAD file_name
   ```

9. **Showing the Difference Between Staged and Unstaged Changes**:
   ```sh
   git diff
   ```

10. **Showing the Difference Between Staged Changes and the Last Commit**:
    ```sh
    git diff --staged
    ```

11. **View Commit Details**:
    ```sh
    git show commit_hash
    ```

### Git Workflows

#### Basic Git Workflow

1. **Clone the Repository**:
   ```sh
   git clone https://github.com/username/repo_name.git
   ```

2. **Create a New Branch**:
   ```sh
   git switch -c feature_branch
   ```

3. **Make Changes and Commit**:
   ```sh
   git add .
   git commit -m "Add new feature"
   ```

4. **Push the Branch to Remote**:
   ```sh
   git push -u origin feature_branch
   ```

5. **Open a Merge Request (Pull Request)**:
   - Go to the repository on GitLab or GitHub and open a Merge Request (or Pull Request) to merge `feature_branch` into `main`.

6. **Review and Merge**:
   - Once the code is reviewed and approved, merge the changes into the `main` branch.

7. **Update Local Repository**:
   ```sh
   git switch main
   git pull
   ```

### Simplified Release Management Flow

This workflow is simpler than GitFlow and involves fewer branches, making it easier for teams to manage their projects.

1. **Main Branch**:
   - This branch contains the latest stable code. All releases are tagged on this branch.

2. **Develop Branch**:
   - This branch is used for ongoing development. All feature branches are merged into `develop`.

3. **Feature Branches**:
   - These branches are created for specific features or tasks. Once the feature is complete, it is merged into `develop`.
   ```sh
   git switch -c feature_branch
   ```

4. **Release Branches**:
   - When preparing for a release, create a release branch from `develop`.
   ```sh
   git switch -c release_branch develop
   ```
   - Finalize the release in the release branch by performing final tests and bug fixes.

5. **Merging Release into Main**:
   - Once the release branch is stable, merge it into `main` and tag the release.
   ```sh
   git switch main
   git merge release_branch
   git tag -a v1.0.0 -m "Release v1.0.0"
   git push origin main --tags
   ```

6. **Merging Release Back into Develop**:
   - After merging into `main`, merge the release branch back into `develop` to ensure that all changes are included in future development.
   ```sh
   git switch develop
   git merge release_branch
   ```

### Summary
By understanding and using these Git commands and workflows, you can effectively manage your codebase, collaborate with others, and maintain a clean and organized project history. Using a simplified release management flow with main, develop, feature, and release branches, you can ensure smooth and efficient development and release processes.
