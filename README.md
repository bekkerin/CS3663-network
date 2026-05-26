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

## Setting up the network.
We are going to set up a network with two routers(Router01 and Router02), both connected to two clients (ClientA1, ClientA2, ClientB1, and ClientB2). We will use the following types of network connections:
+ internal network: creates a completely isolated virtual cable between specified VMs. VMs on the same named internal network can see each other , but they have no access to the host machine or the "real" internet.
+ host-only adapter: creates a private network between the physical host and the VMs. We use it as a "management network" with tools like Secure Shell (SSH) so you can easily work with your virtual machines.
+ NAT: allows the specific VM to access the outside internet using the host's internet connection.
+ later on, we will also use a bridged adapter when we want to connect to the host's WiFi adapter when we work with wireless.

|Virtual Machine|Adapter Slot|Adapter Type|Name/Network|Purpose|
|---------------|------------|------------|------------|-------|
|ClientA1	|Adapter 1	|Internal Network	|LAN_A	|Connects to Router01|
|ClientA2	|Adapter 1	|Internal Network	|LAN_A	|Connects to Router01|
|Router01	|Adapter 1	|Internal Network	|LAN_A	|Gateway for ClientA1|
||Adapter 2	|Internal Network	|Transit_Link	|Dynamic OSPF |Link to Router02
||Adapter 3	|NAT	|Built-in	|Isolated Internet for updates/FRR|
||	Adapter 4	|Host-Only	|VirtualBox Host-only Ethernet Adapter (or similar)|SSH Management from Host|
|Router02  | Adapter 1 | Internal Network | Transit link | Dynamic OSPF Link to Router01|
||	Adapter 2	|Internal Network	|LAN_B	|Gateway for ClientB1|
||	Adapter 3	|NAT	|Built-in	|Isolated Internet for updates/FRR|
||	Adapter 4	|Host-Only	|VirtualBox Host-only Ethernet Adapter (or similar)|SSH Management from Host| 
|ClientB1	|Adapter 1	|Internal Network	|LAN_B	|Connects to Router02|
|ClientB2	|Adapter 1	|Internal Network	|LAN_B	|Connects to Router02|

IP addresses will be assigned as follows:
Network A (LAN_A - Subnet: 192.168.10.0/24)
+ Router01 (Adapter 1): 192.168.10.1
+ ClientA1: 192.168.10.10 (Gateway: 192.168.10.1)
+ ClientA2: 192.168.10.11 (Gateway: 192.168.10.1)

Transit Link (Subnet: 10.1.1.0/30)
+ Router01 (Adapter 2): 10.1.1.1
+ Router02 (Adapter 1): 10.1.1.2

Network B (LAN_B - Subnet: 192.168.20.0/24)
+ Router02 (Adapter 2): 192.168.20.1
+ ClientB1: 192.168.20.10 (Gateway: 192.168.20.1)
+ ClientB2: 192.168.20.11 (Gateway: 192.168.20.1)

## Cloning the ubuntu VMs
We will be using clones to minimize memory and disk space use. Right click on ubuntu

![first screen with vm name](/images/ubuntu12.png "first screen with vm name")
+ Create the clone ClientA1, ClientA2, ClientB1, ClientB2, Router01, and Router02. All should be linked clones and new MAC adddresses for all network adapters should be generated.Make sure you clone them from ubuntu, not one of the other clones. 
ubuntu13
+ You will now see six clones.
ubuntu14
+ Highlight the six clones, right click on the group, and move them to a new group.
ubuntu15
+ Right click the group name and rename the group to CS3663. You can use this to start your whole network as a group later.
ubuntu16
+ All clones have four network adapters, and we will set them according to the tables above. Right click on the VM. Go to Settings. CLick on Network. Use the proper adapter tab and make the changes. Don't forget to enable adapters 2,3, and 4 if you use them. This is what it looks like for ClientA1.
ubuntu17
+ Because we cloned the VMs, they now all have the same name. Change them so your terminal prompt tells you exactly where you are. Start all six clones and log in with your password cybersecurity.
ubuntu18
+ Open a terminal with Start button - System Tools - QTerminal.
ubuntu19
+ For each VM, change the hostname and check it. For ClientA1:
```
sudo hostnamectl set-hostname clientA1
hostname
```
ubuntu20
+ Reset the Machine IDs. When you clone the VMs, they all thave the same product ID/ machine ID. This will confuse the Dynamic Host Control Protocol (DHCP)server for NAT and host-only adapters. For each clone, generate a new unique ID. You can also check the new ID with the nano command(nano closes with CTRL+X). Reboot the machines.
```
sudo rm /etc/machine-id
sudo dbus-uuidgen --ensure=/etc/machine-id
nano /etc/machine-id
sudo reboot
```

## Mapping the interface names and configuring IP addresses
Because VirtualBox maps adapters dynamically, we need to know what Linux named them. On each machine, run:
```
ip link show
```
+ All clients have a loopback adapter (lo) and one ethernet adapter enp0s3.
ubuntu22
+ Both routers have a loopback adapter, and four ethernet adapters (enp0s3, enp0s8, enp0s9, and enp0s10).
ubuntu23
+ Ubuntu Server uses Netplan to manage networking. You will modify /etc/netplan/00-installer-config.yaml on each machine. Use this code to rewrite the yaml files.
```
sudo nano /etc/netplan/00-installer-config.yaml 
```
+ Here is the original file (commented out at top) with the new content for ClientA1.
ubuntu24
```
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: false
      addresses: [192.168.10.10/24]
      routes:
        - to: default
          via: 192.168.10.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
```
+ Use CTRL+X to exit, Y to save the modified buffer, Enter to keep the same file name. Activate the configuration with
```
sudo netplan apply
```
+ For ClientA2 change the address to 192.168.10.11/24, for ClientB1 change the IP to 192.168.20.10/24 and the gateway to 102.168.20.1, for CLientB2 change the IP to 192.168.20.11/24 and the gateway to 192.168.20.1. 
+ For Router01:
```
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3: # Your LAN_A Adapter
      dhcp4: false
      addresses: [192.168.10.1/24]
    enp0s8: # Your Transit_Link Adapter
      dhcp4: false
      addresses: [10.1.1.1/30]
    enp0s9: # Your NAT Adapter
      dhcp4: true
    enp0s10: # Your Host-Only Adapter
      dhcp4: true
```
+ Use CTRL+X to exit, Y to save the modified buffer, Enter to keep the same file name. Activate the configuration with
```
sudo netplan apply
```
+ For Router02:
```
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3: # Your Transit_Link Adapter
      dhcp4: false
      addresses: [10.1.1.2/30]
    enp0s8: # Your LAN_B Adapter
      dhcp4: false
      addresses: [192.168.20.1/24]
    enp0s9: # Your NAT Adapter
      dhcp4: true
    enp0s10: # Your Host-Only Adapter
      dhcp4: true
```
+ Use CTRL+X to exit, Y to save the modified buffer, Enter to keep the same file name. Activate the configuration with
```
sudo netplan apply
```
## Check local connectivity
+ Verify the local connections work:
Ping ClientA2 (192.168.10.11) from ClientA1 (192.168.10.10). (Tests LAN_A switching).
```
ping -c 5 192.168.10.11
```
Ping Router01 (192.168.10.1) from ClientA1. (Tests local gateway connectivity).
```
ping -c 5 192.168.10.1
```
Ping Router02 (10.1.1.2) from Router01 (10.1.1.1). (Tests the Transit_Link).
```
ping -c 5 10.1.1.2
```

## Enable IP forwarding on both routers
+ Right now, if Router01 gets a packet from ClientA1 that is meant for ClientB1, it will drop it. We need to tell the Linux kernel to forward traffic between interfaces. Run this on Router01 and Router02:
```
sudo sysctl -w net.ipv4.ip_forward=1
```
Make the change permanent. Create a new configuration file:
```
sudo nano /etc/sysctl.d/99-routing.conf
```
add this line to the file:
```
net.ipv4.ip_forward=1
```
Save and exit the file (Ctrl+O, Enter, Ctrl+X). Load the new configuration file:
```
sudo sysctl --system
```
You should see a wall of text scroll by, with a line at the very bottom confirming that your 99-routing.conf was read and net.ipv4.ip_forward = 1 was applied.

## Connect the routers to SSH 
Optional, but it will make it much easier to update the routers. You can copy and paste commands from this tutorial to Powershell.
+ Run ip addr show on the routers to find the IP assigned to your Host-Only interface (it usually looks like 192.168.56.X).
+ On my Router01, loopback was 27.0.0.1, enp0s3 was 192.168.10.1, enp0s8 was  10.1.1.1, enp0s9 was 10.0.4.15, and enp0s10 was 192.168.56.103. On Router 02, enp0s10 was  192.168.56.104.
ubuntu25
+ Open the terminal or PowerShell on your physical host computer and log into the routers. In my case, for Router01
```
ssh bekkerin@192.168.56.103
```
+ Router02:
```
ssh bekkerin@192.168.56.104
```
In both cases, I had to add the VM to known hosts.
ubuntu26

## Install FRRouting on both routers
+ Since both routers  are  connected to NAT, they can reach the  public internet to pull down packages. For both routers, copy and paste this code to the SSH terminal:
```
sudo apt update
sudo apt install frr -y
```

## Enable the OSPF Daemon
+ By default, FRR installs with all routing protocols disabled. We need to explicitly turn OSPF on. On both routers, open the daemons configuration file:
```
sudo nano /etc/frr/daemons
```
+ Look for the line that says ospfd=no and change it to:
```
ospfd=yes
```
+ Save and exit (Ctrl+X, Yes, Enter). Restart the FRR  service to apply the change.
```
sudo systemctl restart frr
systemctl status frr
```
+ Close the status with the letter q for quit.

## Configure OSPF via the Cisco-style CLI
+ Enter the interactive FRR engine to configure our routing tables.
+ On Router01: 
```
sudo vtysh
``` 
+ You will see the prompt change to Router01#.
ubuntu27
+ Run the following sequence (avoid copy/paste because sometimes it included the terminal prompt):
```
Router01# configure terminal
Router01(config)# router ospf
Router01(config-router)# router-id 1.1.1.1
Router01(config-router)# network 192.168.10.0/24 area 0
Router01(config-router)# network 10.1.1.0/30 area 0
Router01(config-router)# exit
Router01(config)# exit
Router01# write memory
exit
```
+ For Router02, after sudo vtysh, the code is:
```
Router02# configure terminal
Router02(config)# router ospf
Router02(config-router)# router-id 2.2.2.2
Router02(config-router)# network 192.168.20.0/24 area 0
Router02(config-router)# network 10.1.1.0/30 area 0
Router02(config-router)# exit
Router02(config)# exit
Router02# write memory
exit
```
+ This is my Router02 output:
ubuntu28

## Testing the lab
Enter the interactive  engine for both routers with 
```
sudo vtysh
```
+ On Router01, type
```
Router01# show ip ospf neighbor
```
+ You should see 2.2.2.2 listed in a state of FULL/DR or FULL/BDR  (Designated Router / Backup Designated Router). This means OSPF has successfully synchronized databases.
+ Check the routing table. Still on Router01, type: 
```
Router01# show ip route
```
+ Look for a line starting with a capital O. It should show that it dynamically learned about 192.168.20.0/24 (LAN_B) through Router02.
+ Go to ClientA1's console and try to ping ClientB2 all the way on the other side of the network:
```
ping -c 5 192.168.20.11
```
ubuntu29












