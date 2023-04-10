---
title: Unix Commands
layout: default
parent: Using Ubuntu
nav_order: 3
---

# Using the Command Line
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Basic Command usage
Unix is primarily designed to be used via a terminal. This is also supposed to include getting help and documentation. Because web based documentation is out of the picture, most programs include help messages and manual pages. You can always consult those for help. This page will not cover how to navigate files and the file system in UNIX. 

{: .tip}
It is *very* hard to learn how to use something by reading a guide. Try these commands yourself.


## Getting Help


## The `man` pages
`man` is short for manual. The manual pages are divided into chapters, each of which explain how to use various parts of the system. 

`alias woman=man` if you want to be funny

## `echo`
The `echo` command writes any text following it to the terminal

Try running `echo hello`

## `sudo`
`sudo` is short for "Super User DO". It is a way of running a command as the root user (administrator) without being logged into the administrator account. By default, the root account is disabled, and you can only access it by running commands with `sudo`. 

To use the `sudo` command, your user account must be in the `sudoers` group. Your first user account will be in the group by default, any other accounts may not be. 

`sudo` is dangerous. You can very easily wreck your whole VM if you use it wrong. Be careful when you type any command that starts with `sudo`. 

To test the sudo command, you can run 

`sudo whoami`

the `whoami` command returns the username of the account which ran the command. If you run `whoami` as sudo, you may notice that this will return `root`

On the other hand, if you run `whoami`, it will return your username, not root.


## `apt`
`apt` is a wrapper for `apt-get`. For most of your usage of debian based linux distributions (like ubuntu), you will want to use apt. 
### `apt update`


### `apt upgrade`


### `apt install`

### `apt remove`


## Combining Commands

While all of these commands aren't very powerful on their own, they become a lot more powerful when you can chain them together. 

### The pipe
the pipe (`|`) operator takes the output of one command and sends it to the next one. Tru running `echo hello | 

### Redirects
Most commands in bash have some input and some output. 

### 
