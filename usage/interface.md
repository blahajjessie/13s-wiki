---
title: Interfacing with your VM
layout: default
parent: Using Ubuntu
nav_order: 2
---

# Installing and Configuring Virtualbox 
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Connecting from your host machine terminal

First, to make sure that all of our configuration is correct, let's try connecting to our virtual machine from our host terminal. Begin by starting your virtual machine. If you have the option (virtualbox), use a headless start. This means that your virtual machine is running in the background, but is producing no display output of its own. We need a program to connect to it and use it. 

Now, we can use `ssh` (Secure SHell) to connect to our VM. SSH is a program that enables remote access to a computer. Hopefully, your guest OS is already configured for ssh connections and port forwarding is set up. If not, go back to the [installation steps](/13s-wiki/vm_setup/) now. 

First, on your host OS (not the VM), open a terminal emulator. On Mac, the `terminal` app will be fine. 
- On Windows 10, windows terminal is recommended (Not to be confused with windows command prompt or Windows Powershell, *obviously*). You can open it by searching for `wt` 
- On Windows 11, Windows terminal is the default, and recommended. 
- On mac os, the built in terminal is called `terminal`
- On Linux, you know what you're doing. 


Basic Usage of the `ssh` command is simple. ssh requires a few arguments: 
- the username (you set this in your )
- the server address (localhost, or your current local ip)
- the port number (if you followed the guide, its 2222)