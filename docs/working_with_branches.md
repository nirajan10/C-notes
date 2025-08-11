# Working with Branches

This section provides a beginner-friendly overview of working with branches in Git, covering key concepts and commands to help you manage your codebase effectively.

## Branches

Branches in Git allow you to work on different versions of your project simultaneously. Think of a branch as a separate workspace where you can make changes without affecting the main codebase (often called the `main` or `master` branch). This is useful for:

- Developing new features
- Fixing bugs
- Experimenting without risking the main project

Each branch is independent, so you can switch between them to work on different tasks. For example, you might have a `feature-login` branch for adding a login system and a `bugfix-header` branch for fixing a header issue.

![Branches](https://github.com/nirajan10/C-notes/blob/main/images/branches.png?raw=true)

## Commands

Here are the essential Git commands for working with branches. These commands are run in your terminal or command prompt within your project directory.

- **Create a new branch**:

```bash
git branch branch-name
```

  Creates a new branch called `branch-name` but doesn’t switch to it.

- **Switch to a branch**:

```bash
git checkout branch-name
```

  Switches your working directory to the specified branch.

- **Create and switch to a new branch in one command**:

```bash
git checkout -b branch-name
```

  Combines creating and switching to a new branch.

- **List all branches**:

```bash
git branch
```

  Shows all branches in your repository. The current branch is marked with an asterisk (`*`).

- **Delete a branch** (only after it’s merged or no longer needed):

```bash
git branch -d branch-name
```

  Deletes the specified branch. Use `-D` instead of `-d` to force delete an unmerged branch (use with caution).

- **View remote branches**:

```bash
git branch -r
```

  Lists branches on the remote repository.

## Merging Changes

Merging combines changes from one branch into another. There are two common ways to merge: locally or through a pull request (PR).

### Local Merging

To merge changes from one branch into another (e.g., merging a feature branch into `main`):

1. Switch to the target branch (e.g., `main`):

      ```bash
      git checkout main
      ```

2. Merge the feature branch into `main`:

      ```bash
      git merge feature-branch
      ```

3. If there are no conflicts, Git will combine the changes. You can then push the updated `main` branch to the remote repository:

      ```bash
      git push origin main
      ```

### Merging Through a Pull Request (PR)

In team projects, pull requests are used to review and merge changes on platforms like GitHub, GitLab, or Bitbucket. Here’s how it works:

1. Push your branch to the remote repository:

      ```bash
      git push origin feature-branch
      ```

2. On the platform (e.g., GitHub), create a pull request from `feature-branch` to `main`.
![pull request](https://github.com/nirajan10/C-notes/blob/main/images/pull-request.png?raw=true)
3. Team members review the PR, suggest changes, or approve it.
4. Once approved, merge the PR through the platform’s interface (often with options like "Merge," "Squash and merge," or "Rebase and merge").
5. After merging, delete the branch on the remote repository (optional but keeps things clean):

      ```bash
      git push origin --delete feature-branch
      ```

## Pulling Updates

To keep your local branches up-to-date with the remote repository, you need to pull changes. This is especially important before starting new work or merging.

- **Pull updates for the current branch**:

  ```bash
  git pull origin branch-name
  ```

  Fetches and merges changes from the remote branch into your local branch.

  **Note:** pull = fetch + merge (If the pull doesn't work, use fetch and merge, also useful for checking differences before merging)

- **Fetch updates without merging**:

  ```bash
  git fetch origin
  ```

  Downloads changes from the remote repository but doesn’t merge them. Useful to check what’s new before merging.

- **Merge updates without merging**:

  ```bash
  git merge origin/branch-name
  ```

  Merge changes from the remote repository.

For example, before working on `main`, run:

```bash
git checkout main
git pull origin main
```

This ensures your local `main` branch has the latest changes from the remote repository.

## Handling Merge Conflicts

Merge conflicts occur when Git can’t automatically combine changes from two branches (e.g., if the same line in a file was edited differently in both branches). Here’s how to resolve them:

1. **Identify the conflict**:
   When you run `git merge` or `git pull` and a conflict occurs, Git pauses and shows a message like:

         CONFLICT (content): Merge conflict in file.txt

2. **Open the conflicting files**:
   Git marks conflicts in the affected files with conflict markers:

         <<<<<<< HEAD
         Your changes
         =======
         Changes from the other branch
         >>>>>>> branch-name

3. **Resolve the conflict**:
      - Edit the file to keep the desired changes (or combine both).
      - Remove the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).
      - Save the file.

4. **Mark the conflict as resolved**:

      ```bash
      git add file.txt
      ```

5. **Complete the merge**:

      ```bash
      git commit
      ```

      Git will use a default commit message for the merge, or you can edit it.

6. **Push the changes** (if merging into a remote branch):

      ```bash
      git push origin branch-name
      ```

**Tips for avoiding conflicts**:

- Pull updates frequently to stay in sync with the remote branch.
- Communicate with your team to avoid editing the same files simultaneously.
- Use smaller, focused branches to reduce the chance of conflicts.
