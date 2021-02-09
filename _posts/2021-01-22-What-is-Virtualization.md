---
layout: post
title:  "What is Virtualization"
date:   2021-01-22 14:55:49 -0600
categories: Virtualization
---

Virtualization is the abstraction of the operating system away from the hardware so that other operating systems may reside on the same hardware as the original operating system.   The software that does the abstracting is called the hypervisor.   It is not an operating system of itself.   Instead, the hypervisor will gather the hardware logically and divide up that hardware as resources to the guest operating systems as needed.   No one operating system will utilize all of one hardware resource.

Before we get into the main players out there right now, we first need to cover another aspect of hypervisors.   There are currently 2 types of hypervisors:

* Type 1 hypervisors are installed directly on the hard drive and is booted from the BIOS/UEFI.
* Type 2 hypervisors are actually programs that runs on a conventional operating system (such as Microsoft’s Windows 10 or a Linux desktop distro).   When the main operating system is booted, the user is able to open the program will utilize the main computer’s hardware available to it to give to guest operating systems.   Once the program is loaded does the possibility of utilizing a guest operating system available.

There are a few players in both of these spaces that are available.   In the Type 1 category, we have [VMware’s vSphere (ESXi)](https://www.vmware.com/products/vsphere-hypervisor.html), [Microsoft’s Hyper-V](https://azure.microsoft.com/en-us/services/virtual-machines/), [Linux QEMU/KVM](https://www.linux-kvm.org/page/Main_Page), and [XenServer](https://xenserver.org/).

[VMWare’s vSphere (ESXi)](https://www.vmware.com/products/vsphere-hypervisor.html) is typically your most popular flavor as it has been in the game for a very long time.   It is capable of adding virtual hardware to the guest machines while the machines is still on, such as disk space, memory, and CPUs.   A critical feature if you cannot withstand down time but have applications that are starving for resources.   If you use the free version of ESXi, then you are restricted to just using their web interface, which blocks you from their API, and prevents you from being able to utilize other 3rd party applications for such things as automation, such as Terraform, or backups, such as Veeam or Unitrends.

[Microsoft Hyper-V](https://azure.microsoft.com/en-us/services/virtual-machines/) is right under VMware for the next contender because the companies are already familiar with Microsoft and Windows Server since Windows NT.   Hyper-V does not allow the addition of adding components to the guest operating systems while it is running, but does allow you to interface with the system by PowerShell and Windows Server Manager.   There is a [free version](https://docs.microsoft.com/en-us/windows-server/virtualization/hyper-v/hyper-v-server-2016) of Hyper-V where it is just the [hypervisor](https://web.https://www.microsoft.com/en-us/evalcenter/evaluate-hyper-v-server-2016) and no base Windows Server system.   If you were to install from Windows Server 2016, then it will be a 180-day trial and you are only limited to 2 instances of Windows.   The host operating system (which would be installed on the server from a CD), deploy Hyper-V, and the deploy your guest server.   I do not suggest the second, but recommend the first if you are going to deploy Hyper-V because of business costs.   If you own a computer with Windows 10 Pro, then you can easily turn your normal computer into a Type-1 hypervisor by enabling the Hyper-V role on your computer.   This changes how things work underneath the hood of Windows and, when you reboot, you are actually loading Hyper-V first, and then loading your original computer as a guest.

[QEMU/KVM](https://wiki.qemu.org/Features/KVM) is one of the varieties that Linux distributions offer.   Typically these are offered as part of the distribution of your choice by installing your favorite distribution first (minimal install is what is recommended), update (as usual), then `<groupinstall virtualization>` in accordance with your distribution of choice.   Typically the cost here is free, except for the labor/expertise that would be put into this project.   Support is also typically not apart of this solution, unless being purchased from a 3rd party or in-house.

[Xen](https://www.xenproject.org/) is its own hypervisor that was developed in conjunction with The Linux Foundation.   It is used more in cloud computing, but is still a hypervisor in its own right, totally free.

[XenServer](https://xenserver.org/) is its own type of hypervisor, typically supported within its own circles at XenServer.org, but not typically in the main Linux distribution circles.   It was forked (source code taking a different direction) after The Linux Foundation laid claim to Xen in 2013.   Citrix at one time had took advantage of XenServer as a marketing exploit and sold annual licenses on a per socket basis.

Type 2 Hypervisors are, as mentioned before, programs already installed on a host OS, such as Windows 10 or MacOS.   Examples of these includes:

# [VMware Workstation](https://www.vmware.com/products/workstation-pro.html)
You can download a trial of this and begin using it.   However, after the trial period is over, guest machines that are turned off at the point that the trial period is over or after can’t be booted.   In order to get around this problem, you would need to purchase a license from a reseller VMware.   Once purchased, guest machines can be powered on and off as you need.

# [Oracle VirtualBox](https://www.virtualbox.org/)
VirtualBox is typically best to begin learning the basics of virtualization and is free (only if you don’t have Windows 10 Pro).

There is no one technology or product better than the other.   Each depends on your situation.   Microsoft Hyper-V Server 2016 is free and allows you to deploy as many guest servers as you want and allows you to backup its guest machines, but does not have a direct GUI, like VMWare’s ESXi/vSphere has.   However, VMware’s ESXi/vSphere’s free offering does not allow you to interface with its API’s unless you purchase licenses.   Linux’s QEMU/KVM is totally free but requires familiarity with a Linux server distribution of choice (Fedora, Red Hat, Debian, Ubuntu, etc.).

Type 1 Hypervisors are typically recommended for production usage (companies using it to support other systems to make a profit) while Type 2 Hypervisors are typically used by people that are wanting to learn about virtualization or another operating system than the one typically on their main system, such as running a Fedora desktop OS on an Windows 10 box.