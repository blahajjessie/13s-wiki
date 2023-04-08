---
title: The File System
layout: default
parent: Using Ubuntu
nav_order: 1
---

# Installing and Configuring Virtualbox 
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

# The unix File System

Like the operating systems you may be used to, Unix uses a tree based file structure. This means that every folder can either have files or folders contained within it (you will learn the formal definition of a tree later). This also means that you can't have things like a folder containing itself, or a file in two folders at the same time. While some of these can be done with links, this is irrelevant for the scope of this class. 

There are also some special files that are not actually files, but just appear to be files. 

## A file path
You may often see file paths like `/etc/`, `foo/bar`, or `foo/`. These all mean different things. 
Here is how to read a file path:
- If a file path begins with a forward slash `/`, it starts from the root directory
- If it begins with any other special folder, it starts from there (ex: `~/Documents` starts from `~` (home))
- A slash in the middle represents a folder. For example `/etc/ssh/` is the folder `ssh` inside the folder `etc` (inside the root folder)
- A slash at the end represents that we have a folder. 
## File Extensions

In most of the time you have spent with computers, many of the files you have dealt with have had different types and extensions. It is important to realize that these are simply abstractions and convenience tools. For example, you may expect all files of PDF format to end with `.pdf`. This is not the case. File extensions are not required at all, and are simply a way to tell a program what format a file is meant to be. 

It is also important to note that changing a file extension does not convert between formats. For example, you can not take a text (`.txt`) file and change the file extension to pdf (`.pdf`) and expect it to work.

File extensions are an important tool in keeping track of what the format of a file are, but to the computer mean nothing. Remember to make sure that your files contain data in the correct format to be read. 


## File permissions
TBD


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
The file `/dev/null/` is always empty when you try to read from it. If you try to write it, all the data you write will not be stored. This can be useful if you want to write from a dummy file. 

### random
The files `/dev/random` and `/dev/urandom` are the same thing in newer systems (although they used to be different). They will produce random(ish) bytes forever. Like `/dev/null`, you can not write to it. 

### zero
The file `/dev/zero` will always produce an infinite amount of zeros when you read from it. Like the above files, you can not write to them. 

## Executing a program
In UNIX convention, executable binaries (programs) do not use any file extension. This may be a bit jarring for Windows users especially, but it will start to make sense. While we could give our binaries an extension, we can also use the file permission numbers to specify that a file is meant to be executed. 

To execute a binary file, we simply type the path to the file. Because we have the special `.` folder, we can simply type `./<executable name>` to run the program. 

