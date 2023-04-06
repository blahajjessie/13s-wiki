---
title: UTM for Apple Silicon Mac
layout: default
parent: VM Installation and Configuration
nav_order: 2
---

# Setting up UTM

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Download UTM

Visit the website for UTM and download the latest version
![download](imgs/mac_inst/dw_utm.png)

## Install 

- Install UTM as you would any other Mac Application. Then, open it

## Create a new VM
1. Press "Create VM"
![create](imgs/mac_inst/create_vm.png)

2. Make sure it is "Virtualized" not "Emulated
![virtualize](imgs/mac_inst/virt.png)

3.  Add the ISO file that you downloaded. 

Unlike me, **make sure that you are using the ARM64 version**
![iso](imgs/mac_inst/iso.png)


4.  Configure your storage, ram and CPU Cores
- you *should* increase your ram to at least 4gb, or more if you have any to spare
- you *should not* change the cores
- you *should* allocate at least 32 gb for your virtual disk file
![lots](imgs/mac_inst/stor_sz.png)

5.  Press next on other options
- leave the shared directory page untouched

## Setup Port forwarding and SSH
- Open network settings

## [Return back to main setup](index)

## See also

- [Vm setup](index)
- [windows and intel mac instructions](windows)
- [Installing Ubuntu](ubutnu_2210server)

## Credits
- credit to gary for letting me use his computer to take all the screenshots
