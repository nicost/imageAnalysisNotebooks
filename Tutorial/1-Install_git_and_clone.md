# 1. Install git and clone this repository

## Goal of this section of the tutorial
[Git](https://git-scm.com/) is an incredibly powerful and widely used source code repository management tool. [Github](https://github.com) is a widely used hosting platform for git repositories that also adds lots of goodies such as automated code builds, ticketing systems and tools to make it easy to incorporate changes made by others (i.e. Pull Requests). Following the steps below you should be able to get a copy of this repository on your computer (clone the repo), be able to fork a repository (make a clone of a repository under your account on github), and create a Pull Request.

This tutorial assumes that you know how to open a terminal application on your computer and run some basic commands (such as `cd`, `ls` or `dir`).

## Create an account on Github
If you do not yet have a Github account, create one first. Note that you may well be allowed to join Github education, which gives you access to some tools that others need to pay for.

## Make sure that you have a git client on your computer
Git may already be installed on your computer. Test if this the case by typing `git --version` in your terminal. If it is not installed, download [the git client for your operating system](https://git-scm.com/downloads) and follow the installation instructions.

### Configure Git (First-time setup)
After installing Git, you should configure your name and email address:
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

## (Optional) Fork this repository
On the [main page of this repository](https://github.com/nicost/imageAnalysisNotebooks) click the "Fork" button. This creates your own copy of this repository and lets you save changes independent of what happens in the main repository.

## Clone this repository (or your fork)
To clone [the repository](https://github.com/nicost/imageAnalysisNotebooks.git) click on the green "Code" button. Copy the HTTPS link shown there:
```
https://github.com/nicost/imageAnalysisNotebooks.git
```
In your terminal, go to a convenient location (I keep my repositories in the directory "projects" inside my home directory, so that is where I go), type:
```bash
git clone https://github.com/nicost/imageAnalysisNotebooks.git
```

If you forked the repository, use the green button on your fork to get the correct URL.

This should give you a copy of the git repository on your local computer. Navigate into the cloned directory:
```bash
cd imageAnalysisNotebooks
```

## Git basics

Now that you have your own copy of the git repository, you will want to make some changes and commit these changes. Here are the essential Git commands you'll use regularly:

### Check the status of your repository
The `git status` command shows you which files have been modified, which are staged for commit, and which are untracked:
```bash
git status
```

This command will show you:
- Files that have been modified but not staged
- Files that are staged and ready to be committed
- Untracked files (new files that Git doesn't know about yet)

### Add changes to the staging area
Before you can commit changes, you need to add them to the staging area. You can add individual files or all changes:

Add a specific file:
```bash
git add filename.txt
```

Add all modified files:
```bash
git add .
```

Add all files with a specific extension:
```bash
git add *.py
```

### Commit your changes
Once you've staged your changes, commit them with a descriptive message:
```bash
git commit -m "Add descriptive commit message here"
```

A good commit message should:
- Be concise but descriptive
- Use the imperative mood ("Add feature" not "Added feature")
- Explain what the commit does, not what you did

### View commit history
To see the history of commits:
```bash
git log
```

For a more compact view:
```bash
git log --oneline
```

### Pull changes from the remote repository
Before starting work or pushing your changes, it's good practice to pull the latest changes from the remote repository:
```bash
git pull origin main
```

This command fetches changes from the remote repository and merges them into your current branch.

### Push your changes to GitHub
After committing your changes locally, push them to your GitHub repository:
```bash
git push origin main
```

If you're working on a different branch (see branching section below), replace `main` with your branch name.

## Working with branches

Branches allow you to work on different features or experiments without affecting the main codebase.

### Create and switch to a new branch
```bash
git checkout -b new-feature-branch
```

This creates a new branch called "new-feature-branch" and switches to it.

### Switch between existing branches
```bash
git checkout main
git checkout new-feature-branch
```

### List all branches
```bash
git branch
```

The current branch will be marked with an asterisk (*).

### Delete a branch
After merging a branch, you can delete it:
```bash
git branch -d branch-name
```

## Creating a Pull Request on GitHub

A Pull Request (PR) is a way to propose changes to a repository. Here's how to create one:

1. **Push your branch to GitHub** (if you haven't already):
   ```bash
   git push origin your-branch-name
   ```

2. **Navigate to the repository on GitHub** in your web browser.

3. **Click "Compare & pull request"** - GitHub usually shows this button when you've recently pushed a branch.

4. **Fill out the Pull Request form**:
   - Give your PR a descriptive title
   - Write a detailed description explaining what changes you made and why
   - Reference any related issues (e.g., "Fixes #123")

5. **Select the base branch** (usually `main`) and your feature branch.

6. **Click "Create pull request"**.

7. **Wait for review** - Repository maintainers will review your changes and may request modifications.

## Complete workflow example

Here's a typical workflow when contributing to a project:

```bash
# 1. Make sure you're on the main branch and pull latest changes
git checkout main
git pull origin main

# 2. Create a new branch for your feature
git checkout -b add-new-analysis

# 3. Make your changes to files
# (edit files using your preferred editor)

# 4. Check what files have been changed
git status

# 5. Add your changes to staging area
git add .

# 6. Commit your changes
git commit -m "Add new data analysis notebook"

# 7. Push your branch to GitHub
git push origin add-new-analysis

# 8. Go to GitHub and create a Pull Request
# (follow the steps in the previous section)
```

## Useful tips

- **Always pull before starting new work**: `git pull origin main`
- **Commit often** with small, logical changes
- **Use descriptive commit messages** that explain what and why
- **Don't commit sensitive information** like passwords or API keys
- **Use `.gitignore`** files to exclude files you don't want to track
- **Review your changes** before committing: `git diff`

## Common issues and solutions

**If you made changes to the wrong branch:**
```bash
git stash                    # Save your changes temporarily
git checkout correct-branch  # Switch to the right branch
git stash pop               # Apply your saved changes
```

**If you need to undo the last commit (but keep the changes):**
```bash
git reset --soft HEAD~1
```

**If you want to see what changed in a specific commit:**
```bash
git show commit-hash
```

This should get you started with the essential Git and GitHub workflow!
