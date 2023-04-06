---
title: VM Installation and Configuration
layout: default
has_children: true
has_toc: false
---



## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


1. ## Prep your machiine
    Before you begin, make sure that you have downloaded the ubuntu image for your class and your architecture. For **Spring 2023 CSE13s With Prof. Veenstra** This is ubuntu 22.10 x68_64 (also called amd64) or ubuntu 22.10 arm64. If you are viewing this in the future or for a different class or section, these instruction may be different, or require different sofware. Check with your instructor. 

    **For Any system, You want the 22.10 Server versions**

    - If you have an Apple silicon mac (M1, M2, etc), You will need to use the [arm64 versions](https://ubuntu.com/download/server/arm).**Be sure to use the 22.10 (not 22.04) Server version**
    - If you have a Intel/AMD windows computer, you will need the (amd64 version)[https://ubuntu.com/download/server]. You will still need this if you have an Intel CPU. **Be sure to use the 22.10 (not 22.04) Server version**
    - If you have an Intel Mac, follow the windows instructions
    - If your configuration is not one of these, please contact a Jess or TA during lab sections. 

    You will also need quite a bit (probably 40gb) of free space. If you do not have any free space, make some now. 

2. ## Install your vm software

    [For Apple Silicon mac users](mac)

    [For Other systems](windows)


3. ## Install ubuntu
    - Press "yes" a bunch
    ### Turn off LVM
    - Make sure to Turn off LVM!
    - Again, **UNCHECK** "Setup this disk as an LVM group"
    ![lvm_no](/13s-wiki/vm_setup/imgs/ubuntu_steps/disk.png)

    - press "Yes" or "ok" a bunch
    - Check the "Install openssh server" option
    - Setup a username and password. These can be anything you want
    - You can set the server name to anything you want
    - press "yes" some more

4. ## Powering off your VM

    Be sure to *NEVER* forcefully power off your vm. 
    If you're using virtualbox, this means only using the "Send the shutdown signal" option, the "Save state" option (this is not the same thing as shutting down, and requires disk space), or using the terminal to shutdown. To shutdown your vm from the terminal (The only option using UTM), you can use `sudo shutdown -h now` in terminal. 

4. ## Install required sofware and setup

    We now have a virtual machine, but while we *can* use it right now, there are many tools that we need for this class, and some tools that we can use to simplify this process. 
    ### Required tools:
    This is *not* the definiative list of everything we need for this class. It is *only* what you need to get started with the first few assignments. As the class progresses, you will be given more software you will need to install. Thus, it is best that you familarize yourself with [unix commands](unix_commands)

    - ssh
    - git
    - clang
    - clang-format


    ### Helpful additions:


## See Also:

    - [unix commands](unix_commands)
    - interfacing with your vm
