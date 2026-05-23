# CS3663-network
VirtualBox network used for the CS3663 Principles of TCP/IP class

Install VirtualBox
1. Check System Requirements
Before installing, ensure your computer meets the basics:
+ Processor: x86-64 compatible (Intel or AMD).
+ Memory: At least 4GB of RAM (8GB+ recommended so you can share it with the guest OS).
+ BIOS/UEFI: Ensure Virtualization Technology (VT-x or AMD-V) is enabled in your BIOS settings.
2. Download the Installer
+ Go to the official VirtualBox website.
+ Under the VirtualBox binaries section, select the "platform package" that matches your computer( Windows hosts, macOS hosts (Intel or Apple Silicon), Linux distributions)
3. Run the Installation
The process is straightforward for most users:

For Windows:
+ Double-click the downloaded .exe file.
+ Click Next through the setup prompts.
+ Note: Your network connection may drop briefly. This is normal, as VirtualBox installs a virtual network driver.
+ Click Install and then Finish.

For macOS:
+ Open the downloaded .dmg file.
+ Double-click the VirtualBox.pkg icon in the window that appears.
+ Follow the prompts. You may need to go to System Settings > Privacy & Security to "Allow" Oracle to run if the system blocks it.

For Linux:


4. Install the Extension Pack (Highly Recommended)
The Extension Pack adds support for USB 2.0/3.0 devices, webcam sharing, and disk encryption.
+ On the same download page, look for the VirtualBox Extension Pack.
+ Download the "All supported platforms" file.
+ Open VirtualBox, go to File > Tools > Extension Pack Manager (or simply double-click the downloaded file).
+ Click Install and accept the license terms.

5. Ready to Go
You are now ready to create your first Virtual Machine! You will just need an ISO file (an image of an operating system, like Ubuntu or Windows 11) to get started.

Tip: If you see an error like "VT-x is disabled in BIOS," you must restart your computer, enter the BIOS, and enable Virtualization.


Create the base Windows 11 virtual machine
1. Prerequisites
Windows 11 ISO: Download the official ISO file from iTechTics. Look for the latest stable build (e.g., 24H2).  https://www.itechtics.com/windows-11-download-iso/
License Key: While you can install Windows without a key initially, you’ll need one to personalize the OS. You can often find a $10 Windows 11 Pro license on StackSocial, which is a great budget-friendly option for home labs.  https://www.stacksocial.com/sales/microsoft-windows-11-pro-10
2. Create the Virtual Machine
Open VirtualBox and click New.
Name and Operating System:
Name: WindowsBase
ISO Image: Click the dropdown and select the ISO file you downloaded.
Edition: Select "Windows 11 " (to match your StackSocial key).
uncheck Proceed with Unattended Installation if you want to walk through the manual setup.
Hardware Configuration:
Base Memory: At least 4096 MB (8GB is recommended if your host has enough).
Processors: At least 2 CPUs.
Enable EFI: Ensure this box is checked.
Virtual Hard Disk:
Set the size to at least 64 GB (80 GB+ is safer for updates).
3. Handle TPM and Secure Boot
Modern versions of VirtualBox (7.0+) include a "Virtual TPM" and "Secure Boot" option.

Before starting the VM, go to Settings > System.
Under the Motherboard tab, ensure TPM 2.0 is selected.
Under Processor, ensure Enable PAE/NX is checked.
4. Install Windows 11
Select your VM and click Start.
Boot from ISO: When you see "Press any key to boot from CD or DVD," quickly press a key.
Bypass Requirements (If needed): If you get a "This PC can't run Windows 11" error, press Shift + F10 to open a command prompt and type:
reg add HKLM\System\Setup\LabConfig /v BypassTPMCheck /t REG_DWORD /d 1
reg add HKLM\System\Setup\LabConfig /v BypassSecureBootCheck /t REG_DWORD /d 1
Follow the on-screen prompts. When asked for a product key, click "I don't have a product key" to finish the installation first; you can enter your StackSocial key later in settings. For the operating system, I recommend Windows 11 Pro.
Windows takes a long time to install, so I would just   install the Linux machines at the same time.

5. Final Steps: Guest Additions
Once Windows 11 is on the desktop, go to the VirtualBox menu:

Click Devices > Insert Guest Additions CD Image.
Open File Explorer in the VM, go to the CD drive, and run the installer. This enables full-screen mode, shared clipboards, and better performance.
This video provides a visual step-by-step walkthrough of the installation process, including how to handle hardware requirements and guest additions: Windows 11 VirtualBox installation tutorial
