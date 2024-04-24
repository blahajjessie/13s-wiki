---
title: For Students with Loaner Laptops
layout: default
parent: VM Installation and Configuration
nav_order: 99
---

# For Students with Loaner Laptops

If you're on this page, it's because you've borrowed one of our laptops that has VirtualBox already set up. If that's not you, [go back to the main page](index) and follow the instructions for whichever type of personal computer you have.

## Logging in

You should log into Windows with the "Student" account. The password is `SlugStudent1!`.

## Starting your virtual machine

- Open VirtualBox
- Double-click the VM called "CSE 13S" to launch it

## Logging into your virtual machine

While you could log in from the VM window after your VM boots, it's more convenient to log in with SSH.

- Open Windows Terminal
- Type `ssh vm`

From here on, commands you run will run on the VM. To return to Windows, type `exit`.

## Using your virtual machine

To shut down the VM, hit close on the VM window and it will give you three options. **Make sure to choose "Save the machine state" or "Send the shutdown signal. Never choose "Power off the machine."** Make sure to shut down the VM before you shut down Windows.

All packages you need for CSE 13S should already be installed on the VM, but if you need to install something else you can use [the APT commands](/usage/unix_commands) to install it. That will ask for your password on the VM, which is the same as the password to your Windows account.

To do any coursework for CSE 13S, you'll need to clone your Git repository. [Follow these steps to do so](/usage/git_setup#ssh-keys-and-cloning-your-repository).

You should also read everything else under "Using Ubuntu" in the sidebar to make sure you're familiar with how to navigate the VM.
