---
title: "Getting Started - Basics and Tools"
publishDate: 2025-07-28T13:00:00-06:00
toc: false
images: 
tags:
  - Azure
  - AZ-104
  - 75daysToAZ104
  - Module 1 - Prerequisites for Azure administrators
  - Azure Portal
  - Azure PowerShell
  - Powershell
  - Azure CLI
  - Azure Cloud Shell
  - Azure Mobile App
---

## Getting Started - Basics and Tools

## Introduction

So, where do we start?   How about we start with the basics and answer the following 2 questions in this post:

* What is Azure?
* How do we interact with Azure?

### [What is Azure?](https://learn.microsoft.com/en-us/training/modules/tour-azure-portal/1-introduction)

Microsoft's Azure is a cloud platform that provides compute, storage, and networking resources to build cloud-hosted applications.   These resources can span across many different resources, such as full Virtual Machines (VMs), containers, or cloud-native apps; additional virtual disks for virtual machines, file servers as a service, or SQL as a service; or VPN gateways, networking groups, or load balancers.   There are many choices, but what determines what resources you will use depends on what you are trying to accomplish.

## [Tools At Hand](https://learn.microsoft.com/en-us/training/modules/tour-azure-portal/2-azure-management)

Now that we know Azure is, how do we interact with it to create, utilize, and administer these resources?   That depends on what you are comfortable with and what you need to accomplish.

There are 4 tools that allows you to administer Azure resources:

* Azure Portal
* Azure PowerShell and/or Azure CLI
* Azure Cloud Shell
* Azure Mobile App

### Azure Portal

The [Azure Portal](https://portal.azure.com) is probably going to be the tool that you use the most.   It is a Graphical User Interface (GUI) typically used to carry out single tasks or to dig deeper into details of a resource or logs.  It can also be used to create resources through step-by-step procedures.   However, the Azure Portal does not natively allow you to automate repetitive tasks, such as creating multiple VMs.   The Azure Portal can be accessed from any modern, internet-connected web browser.

### Azure PowerShell & Azure CLI

Azure PowerShell and Azure CLI are 2 tools that accomplish the same task.   Depending on your background will determine which tool you grow more accustomed to.   Both tools allows you to automate repetitive tasks through scripts.

#### Azure PowerShell

[PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.5) natively comes from Microsoft's Windows Servers, ever since Windows Server 2003 SP1 with version 1.0.   Today, non-Azure PowerShell is at version 7.5.   PowerShell utilizes a ```Verb-Noun``` naming convention for its commands so that it is easier to understand what is happening in either the command line or in scripts.

```powershell
New-AzVM -ResourceGroupName "MyResourceGroup" -Name "TestVm" -Image "UbuntuLTS"
```

[Azure PowerShell](https://learn.microsoft.com/en-us/powershell/azure/?view=azps-14.2.0) is simply regular PowerShell with the Azure modules always updated and included in your session, if you are accessing Azure PowerShell from an Azure Cloud Shell session.   Azure PowerShell is a better tool in comparison to the Azure Portal for either more complex tasks with either the Command Line Interface (CLI) or through a PowerShell script (*.ps1 file format) or for automated/repetitive tasks through a PowerShell script.   It is more utilized by administrators with a Windows background for managing Azure resources as an iterative programming language, usually with some type of source control system, such as Git with GitHub, GitLab, or Azure Repositories.

Azure PowerShell can be utilized directly on your computer ([Windows](https://learn.microsoft.com/en-us/powershell/azure/install-azps-windows?view=azps-14.2.0), [MacOS](https://learn.microsoft.com/en-us/powershell/azure/install-azps-macos?view=azps-14.2.0), or [Linux](https://learn.microsoft.com/en-us/powershell/azure/install-azps-linux?view=azps-14.2.0)), if you already have PowerShell installed and the [Azure module imported](https://learn.microsoft.com/en-us/powershell/azure/install-azure-powershell?view=azps-14.2.0).

#### Azure CLI

[Azure CLI](https://learn.microsoft.com/en-us/cli/azure/?view=azure-cli-latest) is another option for Azure administrators that are coming from a Linux background is Azure CLI because has a different approach compared to Azure PowerShell.   The biggest difference between Azure CLI and Azure PowerShell is that Azure CLI utilizes commands and syntax that is similar to Linux's BASH shell and scripting.

```shell
az vm create --resource-group MyResourceGroup --name TestVm --image Ubuntu2204 --generate-ssh-keys
```

Both Azure CLI and Azure PowerShell are cross-platform ([Windows](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest), [MacOS](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-macos?view=azure-cli-latest), and [Linux](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?view=azure-cli-latest)), and can be utilized through an interactive shell or through a script to automate repetitive or complex commands.

### Azure Cloud Shell

[Azure Cloud Shell](https://azure.microsoft.com/en-us/get-started/azure-portal/cloud-shell/?msockid=2e6aa5289d1a6cd30f32b0bf991a6a59) is an interactive, browser-accessible shell used for managing Azure resources utilizing either Azure PowerShell or Azure CLI.   You must authenticate prior to using Azure Cloud Shell.

You can use Azure Cloud Shell either at <https://shell.azure.com> or through the Azure Mobile App, which is coming up next.

### Azure Mobile App

[Azure Mobile App](https://azure.microsoft.com/en-us/get-started/azure-portal/mobile-app/) is a mobile app tha can be installed on either [iOS](https://itunes.apple.com/us/app/microsoft-azure/id1219013620?ls=1&mt=8) or [Android](https://play.google.com/store/apps/details?id=com.microsoft.azure) and is used by the Azure administrator that is away from their computer but still able to manage and monitor their Azure resources.

Some of the features that the Azure Mobile App includes is:

* Checking the status and critical metrics of important resources and services
* Receive alerts concerning health issues of important resources and services
* Review the latest service issues and outages from the Azure platform
* The ability to Shutdown, Reboot, or Start VMs or web apps
* The ability to connect to the VM
* Manage permissions to resources based on the end user's role
* Access to the Azure Cloud Shell, as previously mentioned

## Conclusion

There are many tools and resources available at our disposal to use Azure.   The question is, what best suits you for how you work?  Is it going to be the Azure Portal with point-and-click functionality?   Is it going to be with Azure PowerShell or Azure CLI?   Or are you constantly on the go, utilizing the Azure Mobile App?
