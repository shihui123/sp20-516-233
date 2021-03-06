# Hyper-V Concepts sp20-516-233 Holly Zhang

## Requirements

### Operating System

Either of the following Windows 10 operating systems are needed to run Hyper-V 
[@hyper-v-requirements].

> * Microsoft Windows 10 Enterprise
> * Microsoft Windows 10 Pro
> * Microsoft Windows 10 EDU

### Hardware

Check whether Hyper-V is able to operate on the hardware by entering the 
following command in either Powershell or Command Prompt:

```bash
$ systeminfo
```
Scroll through the output until the section `Hyper-V Requirements:` is found. If 
all requirements have `Yes` next to them, then Hyper-V can be used once it is 
enabled [@hyper-v-requirements]. If the `Data Execution Prevention Available:` 
requirement says `No`, the system BIOS has to be adjusted. Make sure that 
`Hardware Enforced Data Execution Prevention` and `Virtualization Technology` 
are enabled in the system BIOS. It is possible that `Virtualization Technology` 
is listed under a different name depending on the manufacturer 
[@hyper-v-requirements]. 

## Windows Features

In Windows, Hyper-V can be accessed under Windows Features. Hyper-V is listed 
with two main features, `Hyper-V Management Tools` and `Hyper-V Platform`. 
Within these two features are two more sub-features. The following list shows 
how the features are structured:

> * Hyper-V
>   * Hyper-V Management Tools
>     * Hyper-V GUI Management Tools
>     * Hyper-V Module for Windows Powershell
>   * Hyper-V Platform
>     * Hyper-V Hypervisor
>     * Hyper-V Services

Knowing this structure will help with understanding the next sections. 

## Hyper-V management from CMD.EXE

### Enable Hyper-V

To enable Hyper-V from Command Prompt, first start Command Prompt as 
Administrator. Remember to save any work as this will require a system reboot. 
On the command line, enter the following command [@hyper-v-install]:

```bash
$ DISM /Online /Enable-Feature /All /FeatureName:Microsoft-Hyper-V
```
When prompted, restart the machine. Hyper-V will now be enabled on the machine.

### Disable Hyper-V

Before disabling Hyper-V, save any work on the machine since a system reboot 
will be required. Open Command Prompt as Administrator and enter the following 
command:

```bash
$ DISM /Online /Disable-Feature:Microsoft-Hyper-V
```
 
 When prompted, restart the machine to update the changes. This is for disabling 
 the Hyper-V Platform and its sub-features only.
 
## Hyper-V management from Powershell

### Enable Hyper-V

First start Powershell as Administrator. There are two ways to enable Hyper-V 
from Powershell. These commands will require a system reboot so save any work on 
the machine before continuing. Only choose one of the the following commands 
suggested from [@hyper-v-install]. 
 
```bash
$ Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

**OR**

```bash
$ DISM /Online /Enable-Feature /All /FeatureName:Microsoft-Hyper-V
```

### Disable Hyper-V

Make sure to save any work on the machine since this will require a system 
reboot. To disable Hyper-V, start Powershell as Administrator, and then enter 
one of the following commands.

```bash
$ Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V 
``` 

**OR**

```bash
$ DISM /Online /Disable-Feature:Microsoft-Hyper-V
```

Restart the machine when asked to in order for the changes to be made. This will 
disable the Hyper-V Platform and its sub-features.

### More Hyper-V Commands

To disable just the `Hyper-V Hypervisor`, use the following command :

```bash
$ Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-Hypervisor 
``` 

A more extensive list of Hyper-V commands on Powershell can be be found at: 
<https://docs.microsoft.com/en-us/powershell/module/hyper-v/?view=win10-ps>.

## Multipass Benchmark

### Windows 10 Pro and EDU

After enabling Hyper-V as shown in the previous section, Multipass can be now be 
downloaded from <https://multipass.run/>. Find the download button for Windows 
and press it to obtain the executable file. Then run the executable file to 
install Multipass.  

### Windows 10 Home

Hyper-V is not supported for Windows 10 Home [@hyper-v-intro]. In order to 
install Multipass, either Virtualbox needs to be installed or the operating 
system needs to be upgraded to Windows 10 Pro or EDU. The following two 
subsections show how to prepare the installation for Virtualbox on Windows Home 
or how to upgrade to Windows 10 Pro or EDU. 

#### Disable Hyper-V Before Virtualbox Installation

Since Windows 10 Home does not support Hyper-V, Virtualbox can be installed 
immediately at <https://www.virtualbox.org/wiki/Downloads>. However, if the 
operating system is Windows 10 Pro or Windows 10 EDU and Virtualbox is preferred 
instead of Hyper-V, make sure that Hyper-V has been disabled. The previous 
sections include commands to disable Hyper-V. 


#### Upgrade Windows 10 Home to Windows 10 Pro or EDU

For those who already have a Windows operating system but not Windows 10 Pro or 
EDU, downloading the Windows installer can be skipped. What is needed instead is 
a product key. When getting the product key, choose the 64-bit OS. A product key 
for Windows 10 Pro 64-bit can be obtained at 
<https://www.microsoft.com/en-us/store/b/windows?activetab=tab:shopwindows10>. 
Windows 10 EDU 64-bit is provided free of charge for 
Indiana University students at <https://iuware.iu.edu/Windows/Title/2977>.

Once the product key is obtained, navigate to `Settings >  Update & Security > 
Activation > change product key` [@hyper-v-intro]. Enter the new product key and 
press `Next`. This will update Windows to the new edition. After Windows 10 Pro 
or Windows 10 EDU is installed, enable Hyper-V as shown in the previous 
sections.
