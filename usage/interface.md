---
title: Interfacing with your VM
layout: default
parent: Using Ubuntu
nav_order: 2
---

# Interfacing with your VM
{: .no_toc}

## Table of contents
{: .no_toc .text-delta}

1. TOC
{:toc}
## Connecting from your host machine terminal

First, to make sure that all of our configuration is correct, let's try connecting to our virtual machine from our host terminal. Begin by starting your virtual machine. If you have the option (virtualbox), use a headless start. This means that your virtual machine is running in the background, but is producing no display output of its own. We need a program to connect to it and use it.

Now, we can use `ssh` (Secure SHell) to connect to our VM. SSH is a program that enables remote access to a computer. Hopefully, your guest OS is already configured for ssh connections and port forwarding is set up. If not, go back to the [installation steps](/vm_setup/) now.

First, on your host OS (not the VM), open a terminal emulator. On Mac, the `terminal` app will be fine.

- On Windows 10, windows terminal is recommended (Not to be confused with windows command prompt or Windows Powershell, _obviously_). You can open it by searching for `wt`
- On Windows 11, Windows terminal is the default, and recommended.
- On mac os, the built in terminal is called `terminal`
- On Linux, you know what you're doing.

Basic Usage of the `ssh` command is simple. ssh requires a few arguments:

- the username (you set this when you installed ubuntu)
- the server address (`localhost`, or your current local ip)
- the port number (if you followed the guide, its 2222)

We can also see the usage of the `ssh` command by just typing `ssh` into your terminal. It will print all possible flags and options.

To connect to our virtual machine, we need to run `ssh <user>@localhost -p <port>`

## Logging in

You should now see a prompt asking you for your password. Type in the password you set when you created your account on the VM, and press enter (you will not see anything as you type). Your terminal may change a bit, and you are now logged into your Virtual machine via SSH.

You have access to any files and programs on your virtual machine. To log out at any time, you can press `^d` (this is the same on a mac, not command), or type `exit` or `logout`.

## Setting up ssh key-based authentication on your host machine

{: .tip}
Be sure that you're doing this on your host machine! to be sure, press `^d`

First, you need to generate ssh keys. Both Windows (any modern version) and Mac OS have `ssh-keygen` installed. Therefore, we can just run it to generate an ssh keypair on our host machine. When it asks where to save the file, just press enter without typing anything to accept the default location. Then, we need to copy the public key (and only the public key) to our guest OS.

<details>
<summary>Mac OS and Linux</summary>

We can use the <code>ssh-copy-id</code> command to do this!

<br><br>

<code>ssh-copy-id -p 2222 &lt;VM username&gt;@localhost </code>
<br>

</details>

<details>
<summary>Windows</summary>
<ul>
<li>Make sure you're in your windows home folder. This is <code>C:\Users\Username</code> <br>
If you are somewhere else, you can enter that folder by typing <code>cd C:\Users\username</code>
</li>

<li>First, we must use <code>scp</code> to copy your id_rsa.pub file to linux. <br> 
You can do that by using the scp command as follows (in your windows home folder): <br>
<code>scp -P 2222 .ssh/id_rsa.pub &lt;VM_username&gt;@localhost:~ </code><br>
Note that the <code>-P</code> flag is capitalized, unlike in ssh where it's lowercase. 
</li>

<li> Then, ssh into your linux vm as shown in "Logging in"</li>
<li> Finally type <code> cat id_rsa.pub >> .ssh/authorized_keys</code> to copy your rsa public key to the authorized keys file on your VM.</li>
<li> You can now delete the file  <code>~/id_rsa.pub</code> </li>
</ul>

</details>

## Creating an SSH profile

To make it more convenient to connect to your vm, we can add your virtual machine to your SSH profiles. The ssh command stores profiles in `~/.ssh/config` (this is a plain text file with no extension). Creating this file is kinda hard in windows, but you can do so by typing `notepad .ssh/config` (again, in your home folder) Windows will ask you if you want to make a new file, which you do. 

On macOS, we can use vim to make the same file `vim ~/.ssh/config`. The `.ssh/config` file does not exist by default. It must be created.

Then, we can add the following to the file

    Host <ssh_profile_name>
        Hostname localhost
        Port 2222
        User <username>

Then, save and quit. You should now be able to connect to your vm (assuming that it's running) with `ssh <ssh_profile_name>` (you can change vm to whatever you set it to in your config file!).

An explanation of the config file:

- The name following "Host" (`<ssh_profile_name>`) is what your host machine will call your vm. You can set this to whatever you'd like.
- Hostname is the ip address of your vm. In this case, it is running on `localhost`
- Port is the port that you have forwarded
- Username is the username on your vm account

{: .note} 
Windows users need to do one more step, see below!

<details>
<summary>Renaming config.txt</summary>
Chances are, windows saved <code>config</code> incorrectly. You have to go back and change that

<ul>
<li>Make sure you're in your windows home folder. This is <code>C:\Users\Username</code> <br>
If you are somewhere else, you can enter that folder by typing <code>cd C:\Users\username</code>
</li>

<li>Make sure you are using windows PowerShell, not command prompt. If you are using windows terminal (as you should be), it can open a window of either one. Be sure to use powershell (it has a blue icon) </li>

<li>We now have to rename <code>config.txt</code> to <code> config</code>. Use <code>mv .ssh/config.txt .ssh/config</code>
</li>

<li> Just to make sure, type <code>ls .ssh</code></li>
</ul>

</details>

## Using SCP

{: .note}
Avoid using scp on files with spaces in the filename!

Although windows users have already used SCP once now, here is a guide to scp!
The SCP command's usage is `scp <source> <destination>`.

{: .note}
All these commands should be run on your host machine, not your VM (not even in a host terminal that is connected to your VM via ssh). This is because we've only set up SSH access _from your host to your VM_, not the other way around. It would be possible to set it up so you can SSH into your host from your VM, and then you could run scp commands on the VM, but it's not necessary to do that so we won't cover it here.

Because we have our SSH profile setup, we can use the name of the profile instead of `<username>@<host_ip>:<filename> -P <port>` (Note that scp uses `-P` instead of `-p` like ssh)

{: .note}
In all of these instructions, `<ssh_profile_name>` is the name of the profile you created in the section above. You could also specify the username, address, and port, but it is a lot more convenient to use an ssh profile.

If we want to transfer from our host to our guest, we can use the path to our file as our source, and our destination will be `<ssh_profile_name>:<path>`

If we want to transfer from the guest to the host you can reverse the source (now your vm) and the destination (now your host OS)

For example, to copy a file from `~/Downloads/asgn.pdf` to your vm, the command would be

`scp ~/Downloads/asgn.pdf <ssh_profile_name>:~`

and to move `~/readme.md` From your Vm to your Host (to `~/Documents/readme.md`)

`scp <ssh_profile_name>:~readme.md ~/Documents/readme.md`
