---
title: VM Installation and Configuration
layout: default
has_children: true
has_toc: false
nav_order: 2
---

# Configuring Your VM
{: .no_toc}
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## Prep Your Machine

{: .tip} 
These instructions (especially the software versions) are only applicable for Prof. Veenstra in Spring 2023. If you are viewing this in the future or for a different class or section, these instruction may be different, or require different software. Check with your instructor. 

Before you begin, make sure that you have downloaded the ubuntu image for your class and your architecture. This is ubuntu 22.10 x68_64 (also called amd64) or ubuntu 22.10 arm64. 

{: .warning}
**For Any system, You want the 22.10 Server versions**

- If you have an Apple silicon mac (M1, M2, etc), You will need to use the [arm64 versions](https://ubuntu.com/download/server/arm).
- If you have a Intel/AMD windows computer, you will need the [amd64 version](https://ubuntu.com/download/server). You will still need this if you have an Intel CPU. 
- If you have an Intel Mac, follow the windows instructions
- If your configuration is not one of these, please contact a Jess or TA during lab sections. 

You will also need quite a bit (probably 40gb) of free space. If you do not have any free space, make some now. 

## Install your vm software

[For Apple Silicon mac users](mac)

[For Other systems](windows)


{: .warning}
**DO NOT** try to use WSL. Other Virtual Machine platforms are possible, but not recommended or supported.


## Install ubuntu

[These instructions have been configured for Ubuntu 22.10 Server](ubuntu_2210server)

This list may be updated to include other versions later. 

## Powering off your VM

{: .warning}
Be sure to **NEVER** forcefully power off your vm. 

If you're using virtualbox, this means only using the "Send the shutdown signal" option, the "Save state" option (this is not the same thing as shutting down, and requires disk space), or using the terminal to shutdown. To shutdown your vm from the terminal (The only option using UTM), you can use `sudo shutdown -h now` in terminal. 

## Install required software and setup

We now have a virtual machine, but while we *can* use it right now, there are many tools that we need for this class, and some tools that we can use to simplify this process. 

### Required tools

This is *not* the definitive list of everything we need for this class. It is *only* what you need to get started with the first few assignments. As the class progresses, you will be given more software you will need to install. Thus, it is best that you familiarize yourself with [unix commands](unix_commands)

- ssh
- git
- clang
- clang-format

### Helpful additions
    
- idk yet

## See Also:

- [unix commands](/13s-wiki/unix_commands)
- [interfacing with your vm](interface)

