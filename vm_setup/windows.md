---
title: VirtualBox Setup
layout: default
parent: VM Installation and Configuration
nav_order: 1
---

# Installing and Configuring Virtualbox 
{: .no_toc}

## Table of contents
{: .no_toc .text-delta}

1. TOC
{:toc}

## Download <a href="https://www.virtualbox.org/wiki/Downloads" target="_blank">Virtualbox</a>

### Enable virtualization
{: .warning}
If you're on a windows/linux computer make sure that you have Virtualization on in your bios settings. See steps below for info

<details closed>
<summary>Linux</summary>

<ul>
<li> run `systemctl reboot --firmware-setup` </li> 
<li> look around your BIOS, and turn on virtualization</li>
<li> this will be called: VT-x, AMD-V, SVM, or hardware virtualization</li>
</ul>

</details>

<details closed>
<summary>Windows</summary>
<br>
To Check if you have virtualization enabled: 
<ul>

<li>Open task manager</li>
<li>go to advanced -> performance -> cpu</li>
<li>check if Virtualization is enabled</li>
<li>If it is, you do not need to continue </li>
</ul>
<br>
To Enable Virtualization
<ul>
<li> Open the windows menu, and press the power options</li> 
<li> hold `shift` and press restart</li> 
<li>you should then enter a windows boot menu, go to advanced options</li> 
<li> go to "reboot into UEFI settings"</li> 
<li> look around your BIOS, and turn on virtualization</li> 
<li> this will be called: VT-x, AMD-V, SVM, or hardware virtualization </li> 
</ul>
 </details> 

 Users of Mac's do not need to worry about this.

## Creating a VM
- Press "New"
- Give it a name (like 13s)
- Change the type to Linux
- Change the version to "Other Linux (64 bit)" or "Ubuntu 22.04 Jammy Jellyfish" (it does not matter)

## Configure Your Resources
- Increase the memory, to at least 4GB and ideally 8GB
- If you have a system with many cores (more than 4), increase the Processors.
    - If possible, increase the processors to at least 2

## Configure Disks
- Leave the "Create a virtual hard disk file" option checked
- Increase the disk size. If you can, 32GB is recommended, and should be enough. Try to keep it above 24GB.

- Double check your options and press "Finish"

## Add the iso to the system
- Open settings for your new vm
- go to Storage
- In IDE Controller Settings, find "Empty" with a CD icon
- Check the "Live CD" box
- Press the CD button, under attributes in the optical drive section. 
- Press "Choose a disk file"
- Navigate to your Ubuntu Image, and add that to your VM

## Configure Port forwarding

### About Port forwarding and SSH
- ssh: **S**ecure **Sh**ell
- Host OS: the OS that is running on your computer (Mac or Windows)
- Guest OS: The os that we are running in our virtual machine. 

Port forwarding allows us to access services running on our guest OS (Virtual machine) on our Host OS (computer). The service we will be using the most is `ssh`, which will be critical in this course, and probably later in life also. SSH runs on port 22 by default, but can be configured to use anything. Because we may want to run SSH on both our host and guest OSes, we can not use port 22 for our host OS ssh port. Therefore, we will use 2222, a (usually) open port that is often used as a backup for SSH. 

### Instructions 
- Open VirtualBox, select your virtual machine on the left side, and click the Settings icon to open configuration options for that virtual machine.
- Go to the network settings
- For "Adapter 1", Press "Advanced"
- Press "Port Forwarding"
- Press the green "+" icon in the top right 
- Change Host port to "2222" and Guest port to "22"
- Press "OK"

      
## Press Start

## [Return back to main setup](index)
