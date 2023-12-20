---
title: Using Git
layout: default
parent: Using Ubuntu
nav_order: 5
has_toc: true
---

# Using Git
{: .no_toc}

## Table of contents

{: .no_toc .text-delta }

1. TOC
{:toc}

## SSH keys and cloning your repository

First, ssh into your VM. The instructions for this are in the [interface section](interface). 

Once you are in your VM, you need to generate ssh keys so you can prove to GitLab that your computer should be allowed to access your account.

To generate a ssh key pair, run `ssh-keygen` in terminal. You do not need to modify any options.

You should now see 2 new files in the `~/.ssh` folder. These will be called `id_rsa` and `id_rsa.pub`. The file in `id_rsa` is your private key. Do not upload this anywhere, ever. The file `id_rsa.pub` is your public key. This file does not need to be kept secure. It should be in the form of:

    ssh-rsa <many random characters> username@hostname


{: .warning} 
Do not let anyone see your private key. Only copy the contents of `id_rsa.pub`, **not** `id_rsa`.


To prove ownership of your GitLab account, you need to add your public key to the allowed keys. Navigate to the Preferences menu in GitLab, then to "SSH Keys". Press "Add new key" and paste the contents of your public key. You may change the key title if you wish, but you do not need to modify any other settings. 

You can now clone your git repo! Navigate to your repository and press the "Clone" button. Press the clipboard button associated wtih the "Clone with SSH" option. 

Use `git clone <repo url>` with the SSH url in your terminal.

## More on Git

by Sneha De

{: .no_toc}

## TL;DR: The Git Workflow

For most of your assignments and projects that you do individually, all you have to remember is:

```bash
git add <file1> <file2> …
git commit -m "committing!"
git push [origin main]
```

1. Adding (there is no "deleting", "adding" in `git` means staging a change) files with changes (creation, modification, renaming, deletion, etc.)
2. Commit the staged changes with a message
3. Pushing the commit onto the remote.  

{. .tip}
The two optional parameters are the remote name and the branch to push, I recommend specifying these each time to prevent errors. `git push origin main` says push local commits onto the remote called `origin` on the branch called `main`.

## Under the hood

* A Git **repository** is a home for code and is identifiable by the `.git` folder. **Do not** mess with anything inside `.git` unless you know what you're doing!
    * The settings within `.git` are modified through `git config` commands.
* A **commit** is a snapshot of your repo at a point in time. Developers often commit after substantial progress as a checkpoint in their work. Please commit often, especially when you make a breakthrough.
    * In their most simplest form, commits are in linear, chronological order. 
    * That is, if you make changes to fileA at timeA, then later make changes to fileB at timeB, the commit made at timeA does not have the latest changes to fileB. Meanwhile, the commit made at timeB will also include information in timeA, plus any new changes.
* Every commit has a 40-character **has** associated with it.
    * These are unique identiifers of a particular commit and is what you will be expected to submit onto Canvas.
    * Obtained via the Code -> Commits and then clicking the appropriate clipboard for a commit, or via `git log`.
* A **remote** is the *online* version of your *local* (i.e, what you see in your file directory) repository.
    * Remotes are often named, such as the classic `origin` which is the usual default.
    * The only part of the git process that requires an Internet connection is pushing onto the remote. This means you can *always* work and commit locally, and then push everything later.

The following diagram shows the relationship between the **working directory** (where you are currently coding in), the **staging area** (the preparation for a commit), the **local repository** (where your commits are), and the **remote repository** (the online location).

<img src="assets/git-workflow-diagram.svg" alt="diagram depicting the git workflow"/>

* A **branch** can be thought of as a parallel version of your repo.
    * This is crucial in collaborating and also in product environments where the `main` branch is reserved for fully-functional and deployed work.
    * For school assignments, it is okay to only use the `main` branch.

## Commands
