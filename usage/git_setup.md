---
title: Using Git
layout: default
parent: Using Ubuntu
nav_order: 5
---

## Cloning your git repository

First, ssh into your VM. The instructions for this are in the [interface section](interface). 

Once you are in your vm, you need to generate ssh keys so you can prove to gitlab that your computer should be allowed to access your account. To do this, run `ssh-keygen`. You do not need to modify any options. 

You should now see 2 new files in the `~/.ssh` folder. These will be called `id_rsa` and `id_rsa.pub`. The file in `id_rsa` is your private key. Do not upload this anywhere, ever. The file `id_rsa.pub` is your public key. This file does not need to be kept secure. It should be in the form 

    ssh-rsa <many random characters> username@hostname


{: warn} 
Do not let anyone see your private key. Make sure you upload `id_rsa.pub` to gitlab, not `id_rsa`


To prove ownership of your gitlab account, you need to upload your public key. Navigate to preferences in gitlab, and open the "ssh keys" page. Press "Add new key" and paste the contents of your public key into gitlab. You may change the key title if you wish, but you do not need to modify any other settings. 

You can now clone your git repo! Use `git clone <repo url>`

# More git usage

Basic git usage beyond this is shown in your Assignment 0 page. 