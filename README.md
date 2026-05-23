# CS3663-network
VirtualBox network used for the CS3663 Principles of TCP/IP class

## Install VirtualBox
### 1. Check System Requirements
Before installing, ensure your computer meets the basics:
+ Processor: x86-64 compatible (Intel or AMD).
+ Memory: At least 4GB of RAM (8GB+ recommended so you can share it with the guest OS).
+ BIOS/UEFI: Ensure Virtualization Technology (VT-x or AMD-V) is enabled in your BIOS settings.
### 2. Download the Installer
+ Go to the [official VirtualBox website](https://www.virtualbox.org/wiki/Downloads "Download VirtualBox").
+ Under the VirtualBox binaries section, select the "platform package" that matches your computer( Windows hosts, macOS hosts (Intel or Apple Silicon), Linux distributions)
### 3. Run the Installation
#### For Windows:
+ Double-click the downloaded .exe file.
+ Click Next through the setup prompts.
+ Note: Your network connection may drop briefly. This is normal, as VirtualBox installs a virtual network driver.
+ Click Install and then Finish.
#### For macOS:
+ Open the downloaded .dmg file.
+ Double-click the VirtualBox.pkg icon in the window that appears.
+ Follow the prompts. You may need to go to System Settings > Privacy & Security to "Allow" Oracle to run if the system blocks it.
#### For Linux:
+ Follow the instructions on [Download VirtualBox for Linux Hosts](https://www.virtualbox.org/wiki/Linux_Downloads "Download Virtualbox for Linux Hosts")
### 4. Install the Extension Pack (Highly Recommended)
The Extension Pack adds support for USB 2.0/3.0 devices, webcam sharing, and disk encryption.
+ On the same download page, look for the VirtualBox Extension Pack.
+ Download the "All supported platforms" file.
+ Open VirtualBox, go to File > Tools > Extension Pack Manager (or simply double-click the downloaded file).
+ Click Install and accept the license terms.
### 5. Ready to Go
You are now ready to create your first Virtual Machine! You will just need an ISO file (an image of an operating system, like Ubuntu or Windows 11) to get started.

Tip: If you see an error like "VT-x is disabled in BIOS," you must restart your computer, enter the BIOS, and enable Virtualization.


## Create the base Windows 11 virtual machine
### 1. Prerequisites
Windows 11 ISO: Download the official ISO file [from iTechTics](https://www.itechtics.com/windows-11-download-iso/ "Download Windows ISO"). Look for the latest stable build (e.g., 24H2).  
License Key: While you can install Windows without a key initially, you’ll need one to personalize the OS. You can often find a $10 Windows 11 Pro license on StackSocial, which is a great budget-friendly option for home labs. The key for Windows 11 Pro is [at this link](https://www.stacksocial.com/sales/microsoft-windows-11-pro-10 "Windows 11 Pro key") 
### 2. Create the Virtual Machine
+ Open VirtualBox and click New.
+ Name: WindowsBase
+ ISO Image: Click the dropdown and select the ISO file you downloaded.
+ Edition: Select "Windows 11 " (to match your StackSocial key).
+ uncheck Proceed with Unattended Installation if you want to walk through the manual setup.
+ Hardware Configuration:
   + Base Memory: At least 4096 MB (8GB is recommended if your host has enough).
   + Processors: At least 2 CPUs.
   + Enable EFI: Ensure this box is checked.
   + Virtual Hard Disk: Set the size to at least 64 GB (80 GB+ is safer for updates).
### 3. Handle TPM and Secure Boot
Modern versions of VirtualBox (7.0+) include a "Virtual TPM" and "Secure Boot" option. 
+ Before starting the VM, go to Settings > System.
+ Under the Motherboard tab, ensure TPM 2.0 is selected.
+ Under Processor, ensure Enable PAE/NX is checked.
### 4. Install Windows 11
+ Select your VM and click Start.
+ Boot from ISO: When you see "Press any key to boot from CD or DVD," quickly press a key.
+ Bypass Requirements (If needed): If you get a "This PC can't run Windows 11" error, press Shift + F10 to open a command prompt and type:
```
reg add HKLM\System\Setup\LabConfig /v BypassTPMCheck /t REG_DWORD /d 1
reg add HKLM\System\Setup\LabConfig /v BypassSecureBootCheck /t REG_DWORD /d 1
```
+ Follow the on-screen prompts. When asked for a product key, click "I don't have a product key" to finish the installation first; you can enter your StackSocial key later in settings. For the operating system, I recommend Windows 11 Pro.
+ Windows takes a long time to install, so I would just   install the Linux machines at the same time.
+ When asked for the name: WindowsBase.
+ How would you like to set up this device? Set up for personal use.
+ If you don't have a Microsoft account, just create one. Get a confirmation code on your email, and create a PIN. 
+ I just deselect all privacy settings. 
+ Use skip / not now 
+ Wait for installation to finish. You will be logged in with your Microsoft account.
### 5. Final Steps: Guest Additions
Once Windows 11 is on the desktop, go to the VirtualBox menu:
+ Click Devices > Insert Guest Additions CD Image.
+ Open File Explorer in the VM, go to the CD drive, and run the installer. This enables full-screen mode, shared clipboards, and better performance. On my Windows machine with 64 bit processor, I used VBoxWindowsAdditions-amd64.
+ This video provides a visual step-by-step walkthrough of the installation process, including how to handle hardware requirements and guest additions: Windows 11 VirtualBox installation tutorial

## Create the base Ubuntu virtual machine
1. create the Ubuntu Server base
+ Download Ubuntu Server. I used Ubuntu 26.04 LTS from [Get Ubuntu Server] (https://ubuntu.com/download/server "Get ubuntu server")
+ Create the Ubuntu base VM. In VirtualBox: New. Give it the name ubuntu.
![first screen with vm name](/images/ubuntu01.png "first screen with vm name")
+ Use your NSU username (email without @nsuok.edu) and as password cybersecurity as specified in the syllabus.
![second screen with username and password](/images/ubuntu02.png "second screen with username and password")
+ You can leave the memory at 2 GB or you can increase it to 4 GB (4096 MB) if you have enough memory on your machine (like 16 GB)
![third screen with memory and CPUs](/images/ubuntu03.png "third screen with memory and CPUs")
+ Leave the virtual hard disk size as is. By default, VirtualBox only uses what is needed so actual use is much lower.
![fourth screen with virtual hard disk](/images/ubuntu04.png "fourth screen with virtual hard disk")
+ Just let it run and it will do its work. The screen will appear to hang but if you look closely, you will see the  command prompt for root at the bottom.  Simply type reboot , Enter, and the system will reboot to the login.
![installation finished at command line](/images/ubuntu05.png "installation finished at command line")
+ Log in with your NSU username and password cybersecurity.
![log in screen](/images/ubuntu06.png "log in screen")
+ You are now logged in.
![ready to start](/images/ubuntu07.png "ready to start")
+ Enable the shared clipboard between VM and host.
![enable the shared clipboard](/images/ubuntu08.png "enable the shared clipboard")
+ Enable drag and drop between VM and host.
![enable drag and drop between vm and host](/images/ubuntu09.png "enable drag and drop")
+ Install traceroute, SSH, and net-tools. You will probably need to provide your password cybersecurity.
```
sudo apt-get install traceroute 
sudo apt-get install net-tools
sudo apt-get install openssh-server
systemctl status ssh  
sudo systemctl start  ssh
sudo systemctl enable ssh
systemctl status ssh  
```
+ After that last status command, you should see that your SSH server is active, running, and enabled.
![SSH server is installed](/images/ubuntu10.png "SSH server is installed")
+ Install a lightweight desktop (the regular desktop is too resource heavy, and the server does not have a desktop by default). This will take a little while to download.
```
sudo apt-get update 
sudo apt-get install lubuntu-desktop
```
![installing the desktop](/images/ubuntu11.png "installing the desktop")
+ Answer y, wait to  finish, then check the python version
```
python3 --version
```
+ Install pip (python package installer) with
```
sudo apt install python3-pip
```
+ Close the base virtual machine.  
```
shutdown now
```
+ If it does not want to shut down, just close the VM window with the X top right.




