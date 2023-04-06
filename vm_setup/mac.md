---
title: UTM for Apple Silicon Mac
layout: default
parent: VM Installation and Configuration
nav_order: 2
---

# Setting up UTM


## Download UTM

Visit the website for UTM and download the latest version
![download](imgs/mac_inst/dw_utm.png)

## Install 

- Install UTM as you would any other Mac Application. Then, open it

## Create a new VM

### Press "Create VM"
![create](imgs/mac_inst/create_vm.png)

### Make sure it is "Virtualized" not "Emulated
![virtualize](imgs/mac_inst/virt.png)

### Add the ISO file that you downloaded. 

Unlike me, **make sure that you are using the ARM64 version**
![iso](imgs/mac_inst/iso.png)


### Configure your storage, ram and CPU Cores
- you *should* increase your ram to at least 4gb, or more if you have any to spare
- you *should not* change the cores
- you *should* allocate at least 32 gb for your virtual disk file
![lots](imgs/mac_inst/stor_sz.png)

### Press next on other options
- leave the shared directory page untouched

## Setup Port forwarding and SSH
- Open network settings

### [Return back to main setup](index)

