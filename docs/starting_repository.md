# Starting a Git Repository

This section explains two simple ways to start a Git repository: **starting on GitHub** (remote) or **starting locally** on your computer. Both methods lead to the same Git workflow, where you can track changes, collaborate, and manage your project. Let's break it down step by step.

---

## Option 1: Start on GitHub (Remote)

This approach is great if you want to create the repository online first and then bring it to your computer.

### Step 1: Create a Repository on GitHub

1. **Log in to GitHub**: Go to [github.com](https://github.com) and sign in. If you don’t have an account, sign up for free.
2. **Create a New Repository**:
      - Click the **+** icon in the top-right corner and select **New repository**.
      - Give your repository a name (e.g., `my-project`).
      - Choose whether it’s **Public** (anyone can see it) or **Private** (only you and collaborators can see it).
      - Optionally, add a description, a README file, or a `.gitignore` file (to ignore certain files like logs or temporary files).
      - Click **Create repository**.
3. **Copy the Repository URL**: After creating the repository, you’ll see a URL like `https://github.com/your-username/my-project.git` or `git@github.com:your-username/my-project.git` for ssh. Copy it for the next step.

### Step 2: Clone the Repository to Your Computer

1. **Open a Terminal or Command Prompt**:
      - On Windows, use Git Bash (install Git from [git-scm.com](https://git-scm.com) if you haven’t).
      - On macOS or Linux, use the built-in terminal.
2. **Navigate to Your Desired Folder**:
      - Use the `cd` command to go to the folder where you want the repository. For example:

         ```bash
         cd ~/Desktop
         ```

3. **Clone the Repository**:
      - Run the following command, replacing `REPO_URL` with the URL you copied:

         ```bash
         git clone REPO_URL
         ```

         Example: `git clone git@github.com:your-username/my-project.git`
      - This creates a folder named `my-project` on your computer with the repository files.

4. **Navigate to the Repository Folder**:
      - Move into the cloned repository:

         ```bash
         cd my-project
         ```

### Step 3: Start Working

- Add files, edit them, and use Git commands like `git add`, `git commit`, and `git push` to save changes and send them to GitHub.
- Example workflow:

```bash
git add .
git commit -m "Initial commit"
git push origin main
```

---

## Option 2: Start Locally

This approach is ideal if you already have a project on your computer and want to version-control it with Git and connect it to GitHub.

### Step 1: Initialize a Git Repository on Your Computer

1. **Open a Terminal or Command Prompt**:
      - Make sure Git is installed (download from [git-scm.com](https://git-scm.com) if needed).
2. **Navigate to Your Project Folder**:
      - Go to the folder containing your project files. For example:

         ```bash
         cd ~/Desktop/my-project
         ```

3. **Initialize the Git Repository**:
      - Run the following command to turn the folder into a Git repository:

         ```bash
         git init
         ```

      - This creates a hidden `.git` folder to track changes.

4. **Add Your Files**:
      - Stage all files in the folder:

         ```bash
         git add .
         ```

      - Commit the files to the repository:

         ```bash
         git commit -m "Initial commit"
         ```

### Step 2: Connect to GitHub

1. **Create a Repository on GitHub**:
      - Go to [github.com](https://github.com) and create a new repository (as described in Option 1, Step 1).
      - **Important**: Do **not** initialize the repository with a README, `.gitignore`, or license, as your local repository already has files.

2. **Link Your Local Repository to GitHub**:
      - Copy the repository URL (e.g., `git@github.com:your-username/my-project.git`).
      - In your terminal, run:

         ```bash
         git remote add origin REPO_URL
         ```

      Example: `git remote add origin git@github.com:your-username/my-project.git`

3. **Push Your Local Repository to GitHub**:
      - Send your local commits to GitHub:

         ```bash
         git push -u origin main
         ```

      - The `-u` flag sets the default branch (usually `main`) for future pushes.

### Step 3: Start Working

- Your local repository is now connected to GitHub. Use commands like `git add`, `git commit`, and `git push` to manage changes.
- Example:

```bash
git add .
git commit -m "Added new feature"
git push origin main
```

---

## Both Lead to the Same Workflow

Whether you start on GitHub or locally, you end up with:

- A **local repository** on your computer for working on files.
- A **remote repository** on GitHub for backup, collaboration, and sharing.

### Basic Git Commands to Know

- `git add .`: Stages all changed files for a commit.
- `git commit -m "message"`: Saves changes with a descriptive message.
- `git push origin main`: Sends your commits to GitHub.
- `git pull`: Fetches and merges updates from GitHub to your local repository.
- `git status`: Shows the current state of your repository (e.g., changed files).

### Basic workflow

![Basic workflow](https://github.com/nirajan10/C-notes/blob/main/images/git_workflow.png?raw=true)
[Reference for the image](https://medium.com/@humera.rk/top-25-basic-git-commands-to-know-as-a-software-tester-sdet-46d82335fba3)

### Tips for Beginners

- **Commit Often**: Save your work frequently with meaningful commit messages.
- **Check Git Status**: Use `git status` to see what’s happening in your repository.
- **Backup on GitHub**: Regularly push your changes to GitHub to avoid losing work.
- **Learn More**: Explore branching, merging, and collaboration as you get comfortable with Git.

Now you’re ready to start version-controlling your projects with Git and GitHub!
