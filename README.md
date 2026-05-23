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
