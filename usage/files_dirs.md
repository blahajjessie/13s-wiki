---
title: Navigating the File system
layout: default
parent: Using Ubuntu
nav_order: 4
---

# Using the file system Via Command Line

{: .no_toc}

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## `pwd`
`pwd` is short for Print Working directory. This command shows what folder you are currently in. 

Try running `pwd` now, to see what directory you are in. 

## `cd`
This is short for Change Directory. running cd with a file path (or a relative file path) allows a user to change the folder that they are currently in. 

Are you in your home directory? run `cd ..` until you hit the root directory!

Lets go back to the home directory the fast way! run `cd ~`

Feel free to mess around more with `cd`!

## `ls`

How do we know what's in the folder wee're in? The `ls` command lists the files and folders in a directory. 

Try running `ls` to what's in your current directory!



### Advanced usage of `ls`

We can also use `ls` to find the contents of directories that are not the current directory. run `ls /` to see what else is in the root directory!

It is also possible to make hidden files and folders. Try running `ls -a ~` to see what else is in your home directory! By default, `ls` ignores files and folders that begin with `.`. You can show them by using the `-a` flag. 

More advanced usage of `ls` can be found by running `man ls`

## `cat`
`cat` shows the content of a file. For longer files, it might be helpful to use `less`

## `mkdir`
MaKe DIRectory

## `touch`
Creates a file

## `rm`
{: .warn}
The `rm` command is dangerous! Make sure you know what you're removing. There is no undo!

`rm -r` can be used to delete a folder and its contents

## `cp`
given a file (or folder) and a destination, it copies the file to the destination

## `mv`
given a file (or folder) and a destination, it moves the file to the destination

## `vim`
Vim is a text editor that runs in the terminal. To open a file in vim type `vim <filename>`. You can also type a filename that doesn't exist to create a new file. Vim does not use the mouse (without extra configuration), and so everything you do is only using keyboard. You can find many vim cheatsheets on line, but the basics are as follows:

There are many modes in vim. The most important are "normal mode" and "insert mode". Normal mode allows you to enter commands to edit the text. This includes things like find and replace, deleting multiple lines, or moving to a line number. Insert mode allows you to add text to the file, like your'e used to, but to navigate, you must use the arrow keys. 

When you start vim, you are in normal mode. To enter insert mode, press `i`. 

### Exiting vim
To exit vim, first enter normal mode by pressing `esc`. Then to exit, you can type `:q` and press enter. If you have made no changes to the file, it will exit. If you have mad changes, you must chose to save the changes, or discard them. To quit and discard changes, you can type `:q!`. The exclamation mark forces vim to quit, discarding changes. 

To save changes at any point, you can type `:w` in normal mode. You can also save and close by typing `:wq`.




## See also
- [the unix file system](filesys)
- [interfacing with your virtual machine](interface)
- the man pages