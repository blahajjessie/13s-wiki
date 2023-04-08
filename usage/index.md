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


## File Extensions

In most of the time you have spent with computers, many of the files you have dealt with have had different types and extensions. It is important to realize that these are simply abstractions and convenience tools. For example, you may expect all files of PDF format to end with `.pdf`. This is not the case. File extensions are not required at all, and are simply a way to tell a program what format a file is meant to be. 

It is also important to note that changing a file extension does not convert between formats. For example, you can not take a text (`.txt`) file and change the file extension to pdf (`.pdf`) and expect it to work.

File extensions are an important tool in keeping track of what the format of a file are, but to the computer mean nothing. Remember to make sure that your files contain data in the correct format to be read. 

## Executing a program
In UNIX convention, executable binaries (programs) do not use any file extension. This may be a bit jarring for Windows users especially, but it will start to make sense. While we could give our binaries an extension, we can also use the file permission numbers to specify that a file is meant to be executed. 

## File permissions
TBD

## The file system
Like the operating systems you may be used to, Unix uses a tree based file structure. This means that every folder can either have files or folders contained within it (you will learn the formal definition of a tree later). This also means that you can't have things like a folder containing itself, or a file in two folders at the same time. While some of these can be done with links, this is irrelevant for the scope of this class. 

There are also some special files that are not actually files, but just appear to be files. 

## Special folders
These are some special folders that you can use when navigating your file system. These are really handy when moving things around or back and forth. 

### Root
The very first folder in the UNIX file system is called the root folder. This folder is represented by `/`. All folders on all disks are contained in this subfolder somehow. 

### Home
The user's home directory is represented by `~`. This directory usually located in `/home/<username>`

### `.` and `..`
the files `.` ("dot") and `..` ("dot dot") represent the current directory and the parent directory respectively. 

For example, if your current working directory is `~/foo/bar`, `.` would be `bar`, while `..` would be `foo`.

## Special files

### null

### random / urandom

### zero

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


