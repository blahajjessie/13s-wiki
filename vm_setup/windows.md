---
title: VirtualBox Setup
layout: default
parent: VM Installation and Configuration
nav_order: 1
---

# Installing and Configuring Virtualbox 

1. ## Download virtualbox

2. ## Creating a VM
- Press "New"
- Give it a name (like 13s)
- Change the type to Linux
- Change the version to "Other Linux (64 bit)

3. ## Configure Your Resources
- Inrcease the memory, to at least 4GB and ideally 8GB
- If you have a system with many cores (more than 4), increase the Processors.
    - If possible, increase the processors to at least 2

4. ## Configure Disks
- Leave the "Create a virtual hard disk file" option checked
- Increase the disk size. If you can, 32GB is reccomended, and should be enough. Try to keep it above 24GB.

5. ## Double check your options and press "Finish"

6. ## Add the iso to the system
    - Open settings for your new vm
    - go to Storage
    - In IDE Controller Settings, find "Empty" with a CD icon
    - Check the "Live CD" box
    - Press the CD button, under attributes in the optical drive section. 
    - Press "Choose a disk file"
    - Navigate to your Ubuntu Image, and add that to your VM

7. ## Configure Port forwarding (Optional, but *highly* reccomended)
    - Go to the network settings
    - For "Network 1", Press "Advanced"
    - Press "Port Forwarding"
    - Press the green "+" icon in the top right 
    - Change Host port to "2222" and Guest port to "22"
    - Press "OK"

      
8. ## Press Start
