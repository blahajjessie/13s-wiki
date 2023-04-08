---
title: Using Ubuntu
layout: default
has_children: true
has_toc: false
nav_order: 3
---

# Using Ubuntu
{: .no_toc}
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## About UNIX and the command line
Before the desktop, there was the terminal. Before the terminal, there was the [teleprinter](https://en.wikipedia.org/wiki/Teleprinter). Even modern computers have some remnants of the teletype and terminal. (try naming a folder `NUL` on Windows, for example)

In this class, you will be required to get familiarity with the command line and its utilities. You may also be asked to copy commands to your machine. Often, the instructions may vary due to your configuration. For example, an instruction might need you to replace something with your username, cruzid, or folder name. This is usually denoted by angle brackets in instructions. For example, if you are told to type `cd /home/<username>`, you should not type that in exactly. Instead, if your username is `jessicat`, you should type `cd /home/jessicat`. Because of this, and the fact that you should get familiar with UNIX commands, **you should not blindly copy paste commands.**

## The terminal prompt
When you open any logged in terminal, you will usually see a prompt. This will take many forms, but on an unmodified version of Ubuntu, it will be 
`username@hostname:~$`

Let's dissect that. 

First, your username. This is the name you used to log in to your computer and the name of your user account. Like any good operating system, Linux supports making multiple accounts on a single machine, and it is helpful to know which one you're logged into. 

Next is the hostname. This is what your computer calls itself. This is a good way to tell which computer/terminal you're logged into. If you have multiple linux systems to SSH into, it's very handy. 

After that is the tilde (`~`). Between the hostname and the dollar sign is the current working directory. Remember that a directory is the same thing as a folder. The (`~`) directory is a special directory in Unix, as it represents your home folder. In a desktop install, this would contain your Documents, Downloads, etc. This will change as you move through the file system, representing the directory you're in.

Finally, is the Dollar sign and a blinking cursor. This is where you type a command. If you ever see a dollar sign in a tutorial, do not type that into your terminal.

## Copying and Pasting
In the unix terminal, `ctrl` + c and `ctrl` + v do things you may not be used to. If you want to copy or paste on the terminal, you can use `ctrl` + `shift` + c/v. 

## Console Codes
As discussed above, keyboard shortcuts with the control key do things you may not expect. Here are a few that may be useful (and some that are not). It is also common to see `ctrl` written as `^`, so `ctrl` + c will be written as `^c`. Any other  parts of this guide will use this notation. 

- `^c` This is probably the most important one. `^c` will send the kill signal to whatever program is running. This will end the program. It is very useful if your program is stuck in an infinite loop. 
- `^d` This disconnects the terminal and closes it. When we run our programs it can also be used to signal `EOF` when reading from `stdin` (this probably looks like gibberish for now). 
- `^r` This enters reverse search mode. Whatever you type is used to search the history of commands you have run and it autocompletes the most recent result.
- 
- `^g` This makes a sound. That's it.

## Required Software
You will need the following packages for this class (for now)
If you know what you're doing, you can install them now. If you don't, wait until I finish the guide

- `git` (should already be installed)
- `clang`
- `make`
- `clang-format`
- `gdb`
- `valgrind`
- `vim`


## Getting git setup

First, ssh into your VM. Then, generate rsa keys, and upload them to gitlab.

You can now clone your git repo!


## Navigating the File system via terminal

## Installing Software


