---
layout: post
title:  "What is Virtualization"
date:   2021-01-22 14:55:49 -0600
categories: Virtualization
---

<!-- wp:paragraph -->
<p>Virtualization is the abstraction of the operating system away from the hardware so that other operating systems may reside on the same hardware as the original operating system.&nbsp; &nbsp;The software that does the abstracting is called the hypervisor.&nbsp; &nbsp;It is not an operating system of itself.&nbsp; &nbsp;Instead, the hypervisor will gather the hardware logically and divide up that hardware as resources to the guest operating systems as needed.&nbsp; &nbsp;No one operating system will utilize all of one hardware resource.</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Before we get into the main players out there right now, we first need to cover another aspect of hypervisors.&nbsp; &nbsp;There are currently 2 types of hypervisors:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>Type 1 hypervisors are installed directly on the hard drive and is booted from the BIOS/UEFI.</li><li>Type 2 hypervisors are actually programs that runs on a conventional operating system (such as Microsoft’s Windows 10 or a Linux desktop distro).&nbsp; &nbsp;When the main operating system is booted, the user is able to open the program will utilize the main computer’s hardware available to it to give to guest operating systems.&nbsp; &nbsp;Once the program is loaded does the possibility of utilizing a guest operating system available.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>There are a few players in both of these spaces that are available.&nbsp; &nbsp;In the Type 1 category, we have&nbsp;<a href="https://www.vmware.com/products/vsphere-hypervisor.html" target="_blank" rel="noreferrer noopener">VMware’s vSphere (ESXi)</a>,&nbsp;<a href="https://azure.microsoft.com/en-us/services/virtual-machines/" target="_blank" rel="noreferrer noopener">Microsoft’s Hyper-V</a>,&nbsp;<a href="https://www.linux-kvm.org/page/Main_Page" target="_blank" rel="noreferrer noopener">Linux QEMU/KVM</a>, and&nbsp;<a href="https://xenserver.org/" target="_blank" rel="noreferrer noopener">XenServer</a>.</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li><a href="https://www.vmware.com/products/vsphere-hypervisor.html" target="_blank" rel="noreferrer noopener">VMWare’s vSphere (ESXi)</a>&nbsp;is typically your most popular flavor as it has been in the game for a very long time.&nbsp; &nbsp;It is capable of adding virtual hardware to the guest machines while the machines is still on, such as disk space, memory, and CPUs.&nbsp; &nbsp;A critical feature if you cannot withstand down time but have applications that are starving for resources.&nbsp; &nbsp;If you use the free version of ESXi, then you are restricted to just using their web interface, which blocks you from their API, and prevents you from being able to utilize other 3rd party applications for such things as automation, such as Terraform, or backups, such as Veeam or Unitrends.</li><li><a href="https://azure.microsoft.com/en-us/services/virtual-machines/" target="_blank" rel="noreferrer noopener">Microsoft Hyper-V</a> is right under VMware for the next contender because the companies are already familiar with Microsoft and Windows Server since Windows NT.&nbsp; &nbsp;Hyper-V does not allow the addition of adding components to the guest operating systems while it is running, but does allow you to interface with the system by PowerShell and Windows Server Manager.&nbsp; &nbsp;There is a&nbsp;<a href="//docs.microsoft.com/en-us/windows-server/virtualization/hyper-v/hyper-v-server-2016" target="_blank" rel="noreferrer noopener">free version</a>&nbsp;of Hyper-V where it is just the&nbsp;<a href="https://web.https://www.microsoft.com/en-us/evalcenter/evaluate-hyper-v-server-2016" target="_blank" rel="noreferrer noopener">hypervisor&nbsp;</a>and no base Windows Server system.&nbsp; &nbsp;If you were to install from Windows Server 2016, then it will be a 180-day trial and you are only limited to 2 instances of Windows.&nbsp; &nbsp;The host operating system (which would be installed on the server from a CD), deploy Hyper-V, and the deploy your guest server.&nbsp; &nbsp;I do not suggest the second, but recommend the first if you are going to deploy Hyper-V because of business costs.&nbsp; &nbsp;If you own a computer with Windows 10 Pro, then you can easily turn your normal computer into a Type-1 hypervisor by enabling the Hyper-V role on your computer.&nbsp; &nbsp;This changes how things work underneath the hood of Windows and, when you reboot, you are actually loading Hyper-V first, and then loading your original computer as a guest.</li><li><a href="https://web.archive.org/web/20190424203258/https://wiki.qemu.org/Features/KVM">QEMU/KVM</a>&nbsp;is one of the varieties that Linux distributions offer.&nbsp; &nbsp;Typically these are offered as part of the distribution of your choice by installing your favorite distribution first (minimal install is what is recommended), update (as usual), then “<em>groupinstall virtualization</em>” in accordance with your distribution of choice.&nbsp; &nbsp;Typically the cost here is free, except for the labor/expertise that would be put into this project.&nbsp; &nbsp;Support is also typically not apart of this solution, unless being purchased from a 3rd party or in-house.</li><li><a href="https://www.xenproject.org/" target="_blank" rel="noreferrer noopener">Xen&nbsp;</a>is its own hypervisor that was developed in conjunction with The Linux Foundation.&nbsp; &nbsp;It is used more in cloud computing, but is still a hypervisor in its own right, totally free</li><li><a href="https://xenserver.org/" target="_blank" rel="noreferrer noopener">XenServer</a>&nbsp;is its own type of hypervisor, typically supported within its own circles at XenServer.org, but not typically in the main Linux distribution circles.&nbsp; &nbsp;It was forked (source code taking a different direction) after The Linux Foundation laid claim to Xen in 2013.&nbsp; &nbsp;Citrix at one time had took advantage of XenServer as a marketing exploit and sold annual licenses on a per socket basis.</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Type 2 Hypervisors are, as mentioned before, programs already installed on a host OS, such as Windows 10 or MacOS.&nbsp; &nbsp;Examples of these includes:</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><a href="https://www.vmware.com/products/workstation-pro.html" data-type="URL" target="_blank" rel="noreferrer noopener">VMware Workstation</a></p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>You can download a trial of this and begin using it.&nbsp; &nbsp;However, after the trial period is over, guest machines that are turned off at the point that the trial period is over or after can’t be booted.&nbsp; &nbsp;In order to get around this problem, you would need to purchase a license from a reseller VMware.&nbsp; &nbsp;Once purchased, guest machines can be powered on and off as you need.&nbsp;&nbsp;</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p><a href="https://www.virtualbox.org/" data-type="URL" data-id="https://www.virtualbox.org/" target="_blank" rel="noreferrer noopener">Oracle VirtualBox</a></p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>VirtualBox is typically best to begin learning the basics of virtualization and is free (only if you don’t have Windows 10 Pro).</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>There is no one technology or product better than the other.&nbsp; Each depends on your situation.&nbsp; &nbsp;Microsoft Hyper-V Server 2016 is free and allows you to deploy as many guest servers as you want and allows you to backup its guest machines, but does not have a direct GUI, like VMWare’s ESXi/vSphere has.&nbsp; &nbsp;However, VMware’s ESXi/vSphere’s free offering does not allow you to interface with its API’s unless you purchase licenses.&nbsp; &nbsp;Linux’s QEMU/KVM is totally free but requires familiarity with a Linux server distribution of choice (Fedora, Red Hat, Debian, Ubuntu, etc.).</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Type 1 Hypervisors are typically recommended for production usage (companies using it to support other systems to make a profit with) while Type 2 Hypervisors are typically used by people that are wanting to learn about virtualization or another operating system than the one typically on their main system, such as running a Fedora desktop OS on an Windows 10 box.</p>
<!-- /wp:paragraph -->