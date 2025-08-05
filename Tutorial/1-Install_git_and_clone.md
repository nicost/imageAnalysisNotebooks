# 1. Install git and clone this repository

## Goal of this section of the tutorial
[Git](https://git-scm.com/) is an incredibly powerful and widely used source code repository management tool.  [Github](https://github.com) is a widely used hosting platform for git repositories that also adds lots of goodies such as automated code builds, ticketing systems and tools to make it easy to incorporate changes made by others (i.e. Pull Requests).   Following the steps below you should be able to get a copy of this repository on your computer (clone the repo), be able to fork a repository (make a clone of a repository under your account on github), and create a Pull Request.
This tutorial assumes that you know how to open a terminal application on your computer and run some basic commands (such as `cd`, `ls` or `dir`).

## Create an account on Github
If you do not yet have a Github account, create one first.  Note that you may well be allowed to join Github education, which gives you access to some tools that others need to pay for.

## Make sure that you have a git client on your computer
Git may already be installed on your computer.  Test if this the case by typing `git -v` in your terminal.   If it is not installed, download [the git client for your operating system](https://git-scm.com/downloads) and follow the installation instructions.

## (Optional) Fork this repository
On the [main page of this repository](https://github.com/nicost/imageAnalysisNotebooks) click the "Fork" button.  This creates your own copy of this repository and lets you save changes independent of what happens in the main repository.

## Clone this repository (or your fork)
To clone [the repository](https://github.com/nicost/imageAnalysisNotebooks.git) click on the green "Code" button.  Copy the HTTPS link shown there:
```
 https://github.com/nicost/imageAnalysisNotebooks.git
 ```
 In your terminal, go to a convenient location (I keep my repositories in the directory "projects" inside my home directory, so that is where I go), type:
 ```
 git clone
 ```
 and paste the link you got from the green button.

 If you forked the repository, use the green button on your fork.

 This should give you a copy of the git repository on your local computer


## Git basics
Now that you have your own copy of the git repository, you will want to make some changes and commit these changes.
