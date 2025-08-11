# Guide to Completing and Submitting Your Assignment

This guide walks you through the steps to clone the assignment repository, create a branch with your full name, complete your work, and submit it by pushing to your branch. Follow these instructions carefully to ensure your submission is successful.

## Prerequisites

- A GitHub account. If you don’t have one, sign up at [github.com](https://github.com).
- Git installed on your computer. Download and install from [git-scm.com](https://git-scm.com/downloads).
- Basic familiarity with Git commands (cloning, branching, committing, pushing).
- Access to the assignment repository (you’ll receive an invitation link from your instructor).

## Step-by-Step Instructions

### 1. Accept the Repository Invitation

- Your instructor will share a GitHub repository invitation link.
- Click the link and accept the invitation to gain access to the repository. You may need to log in to your GitHub account.
- Ensure you have at least **write** access to the repository (confirmed by your instructor).

### 2. Clone the Repository

- Open a terminal (or command prompt) on your computer.
- Copy the repository’s HTTPS or SSH URL from the GitHub repository page (e.g., `git@github.com:your-org/assignment-repo.git`).
- Run the following command to clone the repository to your local machine:

  ```
  git clone <repository-url>
  ```

  Example: `git clone git@github.com:your-org/assignment-repo.git`
- Navigate into the cloned repository folder:

  ```
  cd assignment-repo
  ```

### 3. Create a Branch with Your Full Name

- Create a new branch using your full name (e.g., `FirstName-LastName`). Replace spaces with hyphens if needed.
- Run the following command:

  ```
  git checkout -b FirstName-LastName
  ```

  Example: `git checkout -b Nirajan-Thakuri`
- Verify you’re on the new branch:

  ```
  git branch
  ```

  The branch with an asterisk (`*`) is the active branch.

### 4. Complete the Assignment

- Make changes to the files in the repository as required for the assignment.
- **Create a doc which contain all answer to the questions and also include screenshot of the output for the coding questions.**
- Save your changes in your local repository.

### 5. Commit Your Changes

- Check the status of your changes to see modified or new files:

  ```
  git status
  ```

- Add the files you want to commit:

  ```
  git add .
  ```

  (This adds all changed files. To add specific files, use `git add <filename>`.)
- Commit your changes with a meaningful message:

  ```
  git commit -m "Completed assignment by FirstName LastName"
  ```

  Example: `git commit -m "Completed assignment by Nirajan Thakuri"`

### 6. Push Your Branch to GitHub

- Push your branch to the remote repository on GitHub:

  ```
  git push origin FirstName-LastName
  ```

  Example: `git push origin Nirajan-Thakuri`

### 7. Verify Your Submission

- Visit the repository on GitHub (e.g., `https://github.com/your-org/assignment-repo`).
- Check the “Branches” tab to confirm your branch (`FirstName-LastName`) appears with your changes.
- Notify your instructor that you’ve submitted your work by pushing to your branch (if required).

## Troubleshooting

- **Permission Denied Error**: If you get a “permission denied” error when pushing, ensure you’ve accepted the repository invitation and have write access. Contact your instructor if the issue persists.
- **Branch Name Conflicts**: If someone else has the same name, add a unique identifier (e.g., `John-Doe-123`). Check with your instructor for naming conventions.

## Additional Notes

- Do **not** push to the `main` branch or modify other students’ branches.
- If you need to update your submission, make additional changes, commit, and push to the same branch.
- Contact your instructor if you encounter any issues or have questions.
