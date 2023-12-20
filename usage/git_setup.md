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

