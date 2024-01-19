---
layout: post
title:  "Git for the Impatient"
date:   2024-01-17 12:44:36 -0300
categories: git github howto
---
### A Simple Git How-To

![Git-GitHub logo](/assets/img/git-github.jpeg "Git-GitHub logo")

## Create a new repository on GitHub

- To begin, sign in to your user account on *GitHub*.
- In the upper right corner, click the `+` sign icon, then choose **New repository**. This will take you to a page where you can enter a repository name (this tutorial uses `test-repo` as the repository name), description, and choose to initialize with a README (a good idea!).
- It is a good idea to add a `.gitignore` file by selecting one of the languages from the drop down menu, though for this tutorial it will not be necessary.
- Similarly, in practice you should choose a license to that people know whether and how they can use your code.
- Once you have entered a repository name and made your selection, select **Create repository**, and you will be taken to your new repository web page.

## Clone your repository to your local machine

Next, clone your newly created repository from GitHub to your local computer. From your repository page on GitHub, click the green button labeled **Clone or download**, and in the “Clone with HTTPs” section, copy the URL for your repository.

Next, on your local machine, open your bash shell and change your current working directory to the location where you would like to clone your repository. Note that here we are using a bash command - `cd` (change directory).

For example, on a Unix based system, if you wanted to have your repository in your `Documents` folder, you change directories as follows:

```
cd Documents
```

Once you have navigated to the directory where you want to put your repository, you can use:

```
git clone https://github.com/URL-TO-REPO-HERE
```

The `git clone` command copies your repository from GitHub to your local computer. Note that this is a git specific command.

```
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY
```

When you run `git clone repo-path-here`, You should see output like:

```
Cloning into 'test-repo'...
remote: Counting objects: 5, done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 5 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (5/5), done.
Checking connectivity... done.
```

Note: The repository name and output numbers that you see on your computer, representing the total file size, etc, may differ from the example provided above.

To verify that your repository now exists locally, type `ls` in your terminal. The ls command lists the files & folders available in your current directory. You should see a directory with the same name as the repository that you created previously on GitHub.

## Tracking changes with `git add` and `git commit`

Next use cd to change directories using the syntax:

```
cd my-repo-name
```

Replace my-repo-name with the folder name of your repo (this should be your repo name - e.g. 14ers-git)

```
cd test-repo
```

If you list all the files in this directory (using `ls -a`), you should see all of the files that exist in your GitHub repository:

```
ls -a

.git  .gitignore  LICENSE  README.md
```
Alternatively, we can view the local repository in the finder (Mac), a Windows Explorer (Windows) window, or GUI file browser (Linux).

Simply open your file browser and navigate to the new local repo.

**Important Tip:** The `.git` element is listed when you use the `ls -a` command shows up is actually a directory which will keep track of your changes (the commits that you make) in git. **Warning:** Do not edit the files in this directory manually!

Using either method, we can see that the file structure of our cloned repo mirrors the file structure of our forked GitHub repo.

## Edit a file in your repo

Next, open up your favorite text editor and make a few edits to the `README.md` file. Save your changes.

Once you are happy with your changes and have saved them, go back to your terminal window and type `git status` and hit return to execute the command.

```
git status

On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

The output from `git status` indicates that you have modified the file `README.md`. To keep track of this change to this file, you need to

1. `add` the changes, then
2. `commit` the changes.

### Add and commit changes

You will use the add and commit functions to add and commit changes that you make to git.

1.    `git add`: takes a modified file in your working directory and places the modified version in a staging area.
2.    `git commit`: takes everything from the staging area and makes a permanent snapshot of the current state of your repository that is associated with a unique identifier.

These two commands make up the bulk of many workflows that use git for version control.

### Add files

You can add an individual file or groups of files to git tracking. To add a single file, use

```
git add file-name-here-with-extension
```

To add the `README.md` file that you just modified, you’d use:

```
git add README.md
```

To add ALL of the files that you have edited at the same time, you can use:

```
git add --all
```

Use `git add --all` with caution. You do not want to accidentally add things like credential files, `.DS_Store` files, or history files.

### Commit files

Once you are ready to make a snapshot of the current state of your repository, you can use `git commit`. The git commit command requires a **commit message** that describes the snapshot / changes that you made in that commit.

A commit message should outline what changed and why. These messages

1. help collaborators and your future self understand what was changed and why
2. allow you and your collaborators to find (and undo if necessary) changes that were previously made.

If you are not committing a lot of changes, you can create a short one line commit message using the `-m` flag:

```
git commit -m "Editing the README to try out git add/commit"
```

Alternatively, if you are committing many changes, or a small number of changes that require explanation, you’ll want to write a detailed multi-line commit message using a text editor.

If you have configured git to use your favorite text editor (via `git config --global core.editor your-fav-editor-here`), then you can open that editor to write your commit message using the `git commit` command:

```
git commit
```

Once you save your commit message and exit the text editor, the file that you created will contain your commit message.

### Challenge

Make changes to files in your git repo. These changes may includes

- adding new files to the repo
- adding content to the files (Text)
- adding new directories to your repo

For each change, practice using

- git add to stage the change, and
- git commit to take a snapshot of your repository

After you’ve made a few commits, check out the output of the `git log` command. You should see the history of your repository, including all of the commit messages!

```
git log

commit 778a307bcc8350bddba47e96a940acafed55f5d8
Author: Fred Flinstone <flinstone@bedrock.com>
Date:   Tue Sep 19 18:38:28 2017 -0600

    adding a file in a subdirectory

commit f2b0ff9af905fa2792bf012982e10f0214148c70
Author: Fred Flinstone <flinstone@bedrock.com>
Date:   Tue Sep 19 16:50:59 2017 -0600

    fixing typo

commit e52dceab576c3b2491af25b5774cc56e65a40635
Author: Fred Flinstone <flinstone@bedrock.com>
Date:   Tue Sep 19 10:27:05 2017 -0600

    Initial commit
```

An interesting shortcut to save time is that `git commit -a` means the same thing as `git add -u && git commit`.

It's not the same as `git add .` as this would add *untracked files* that aren't being *ignored*, `git add -u` only stages changes (including deletions) to *already tracked files*.

The `.gitignore` file tells Git which files to ignore when committing your project to the GitHub repository. gitignore is located in the root directory of your repo.

The `.gitignore` file itself is a plain text document. Here’s an example `.gitignore` file:

```
# Binaries for programs and plugins
*.exe
*.exe~
*.dll
*.so
*.dylib
# Test binary, built with `go test -c`
*.test
# Output of the go coverage tool, specifically when used with LiteIDE
*.out
# Dependency directories (remove the comment below to include it)
vendor/ 
```

You may want to ignore certain files for multiple reasons:

- The files contain sensitive data.
- The files are system specific and do not need to exist on every machine’s copy.
- Temporary files such as compiled code.

## Push changes to GitHub

So far we have only modified our local copy of the repository. To add the changes to your git repo files on your computer to the version of your repository on GitHub, you need to **push** them GitHub.

You can push your changes to GitHub with:

```
git push
```

You will then be prompted for your GitHub user name and password. After you’ve pushed your commits, visit your repository on GitHub and notice that your changes are reflected there, and also that you have access to the full commit history for your repository!

**ERRATA:** Recently, GitHub has replaced authentication with passwords to a more secure method using **tokens**. See below.

## Personal Access Token

First, you need to create a [personal access token](https://help.github.com/articles/creating-an-access-token-for-command-line-use/) (PAT). Now, when you *push* your commits GitHub will then ask for your PAT instead of your password.

```
$ git push https://github.com/user-or-organisation/myrepo.git
Username: <my-username>
Password: <my-personal-access-token>
```

PAT is much more secure and has an expiration date as well. You can even have different PATs for different computers.

## Actually using the token

One drawback is that the PAT is really hard to remember and it is not something you want to keep inside a plaintext file. You can automate the authentication like this:

- If you already have the repository cloned locally

```
git remote add origin https://[TOKEN]@github.com/[REPO-OWNER]/[REPO-NAME]`

git push
```

- If you are cloning a new repository

```
git clone https://[TOKEN]@github.com/[REPO-OWNER]/[REPO-NAME]
```

(Replace the square brackets and what's between them with your corresponding details. The part after the the `@` is the same as the repository url without https://)

*"Oh, so one goes and put a private information in the clear, in an URL, for every sniffer and router to see. And bash history... nice."*

## Another way to save your credentials in Git

**Attention**: This method saves the credentials in plaintext on your PC's disk. Everyone on your computer can access it, e.g. malicious NPM modules.

Run

```
git config --global credential.helper store
```

then

```
git pull
```

provide a username and password and those details will then be remembered later. The credentials are stored in a file on the disk, with the disk permissions of "just user readable/writable" but still in plaintext.

If you want to change the password later

```
git pull
```

Will fail, because the password is incorrect, git then removes the offending user+password from the `~/.git-credentials` file, so now re-run

```
git pull
```

to provide a new password so it works as earlier.

**Note:** `git clone` copies all files to the local machine, while `git pull` only copies the modified files to the local machine. `git clone` creates a connection between both repositories, while `git pull` requires a connection to be made before it can work.
