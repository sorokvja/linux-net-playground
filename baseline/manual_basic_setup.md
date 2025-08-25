# Basic Setup
## Introduction 
**The Basic Setup** manual describes... the basic setup required to follow next steps described, including lab_001 and others. To be ready, you need  to create 3 virtual machines using [VirtualBox](https://www.virtualbox.org/) virtualization software. The virtual machines required are: 
1. [OPNsense](https://opnsense.org/) - an open source firewall and routing platform
2. [openSUSE Leap 15.6 xfce](https://www.opensuse.org/#Leap) - a workstation for experiments 
3. [Ubuntu Server 24.04](https://ubuntu.com/server) - a server where software will be installed

Of course any other known distro a user is familiar with could be chosen instead of the listed ones, as well as the setup may seem too complicated. Here are the main reasons why author made the choises:
- Ubuntu was chosen mostly because it is quite popular and beginner friendly, also some experience with apt package manager can be handy in the future. 
- Author runs openSUSE on a daily basis and is quite familiar with the distro and its capabilities, also loves zypper package manager. Moreover, xfce is convenient and resourse friendly DE that can be chosen as the default option during the installation process, with no extra steps required. 
- OPNsense... Two options were considered - OPNsense and pfSense, the first one was chosen because it seemed at the moment it is more newcomers friendly, more modern, security focused and with more frequent updates.
- VirtualBox was chosen as a user friendly software supported by both Linux and Windows host OSs and, depending on a host OS Linux distro, can be easily installable and maintainable.  
- Though it is possible to simiplify the setup by using only two VMs - a server and a workstation, or even more extreme option with one VM (server) communicating with host OS, author believes that using and configuring a router is a handy experience by itself, and involvement of host OS in scope of labs and experiments with VMs is something one should escape, whenever it is possible. 

Creation of virtual machines (VM) with VirtualBox is straightforward and user friendly process in general, hence it won't be described here in details. If questions appear, please refer to the official sources of VirtualBox and the related guest OSs, which are OPNsense, openSUSE and Ubuntu (Google and AI could be helpful as well). Instead, some inmportant notes on the VM configuration will be provided below. It is also strongly suggested to:
1. proceed with the same order VMs are described below,
2. disable the "Unattended guest OS installation" feature when each VM is created,
3. create a separate virtual hard disk per a VM with "Pre-allocate Full Size" option enabled.
If you are not following the suggestions or choosing other guest OSs of your own taste, author assumes you know what you are doing and will be fine. 

## Network topology
To be added...

## VM Configuration 
### HW Resources Assigned
It depends on both the purpose of VM itself and the host hardware specs, how many CPU cores or RAM to assign per a VM. Also remember to ensure there are always some "free" resources not assigned to any VM in order host OS can perform its functions. Generally speaking, without any guarantees, these could be initial settings one can experiment with: 
VM|CPU Cores|RAM, MB|Video Memory, MB|Storage, GB|
|-|---------|---|------------|-------|
|OPNsense|2|2048|16|25|
|openSUSE Leap 15.6 xfce|4|3072|128|30|
|Ubuntu Server 24.04|4|3072|16|30|

### VirtualBox
First step is to create a new Host-only Network, VirtualBox GUI can be used to do it:
1. File --> Tools --> Network (or press CTRL + H), by default "Host-only Networks" tab should be open
2. Create a new network for the basic setup, the network name will be assigned automatically:
    1. Default Adapter configuration usually works just fine, but one might consider to adjust it manually or choose the option "Configure Adapter Automatically" 
    2. If either default or automated configuration is chosen, usually "Enable Server" option in "DHCP Server" tab must be enabled as well
    3. For now, let's assume you know what you are doing if you choose an option "Configure Adapter Manually", author uses this manual setup: IPv4 Network Mask: 255.255.255.252; DHCP Server: disabled

### OPNsense VM
1. Create a new VM, but do not launch it yet. 
2. Open OPNsense VM settings, proceed to Network
3. Ensure three network adapters are enabled:
    1. NAT
    2. Host-only Adapter (name - choose the one you created recently, i.e., "vboxnet0"; promiscuous mode = "Deny")
    3. Internal Network (name = "lab_srv_net"; promiscuous mode = "Deny")
    4. Internal Network (name = "lab_ws_net"; promiscuous mode = "Deny")
4. Launch VM and proceed with the guest OS installation
5. Reboot, if required, login as a root
6. Choose an option "1) Assign interfaces" (interface order may differ, follow the OPNsense's actual order):
    1. Skip LAGGs (enter "N")
    2. Skip VLANs (enter "N")
    3. Assign WAN (compare NIC MAC with the one assigned to the Adapter 1 in VB, attached to NAT)
        1. Enter the WAN interface name (e.g., em0)
    4. Assign LAN (compare NIC MAC with the one assigned to the Adapter 2 in VB, attached to Host-only Adapter)
        1. Enter the LAN interface name (e.g., em1)
    5. Assign OPT1 (compare NIC MAC with the one assigned to the Adapter 3 in VB, attached to Internal Network)
        1. Enter the Optional interface 1 name (e.g., em2)
    6. Assign OPT2 (compare NIC MAC with the one assigned to the Adapter 4 in VB, attached to Internal Network)
        1. Enter the Optional interface 2 name (e.g., em3)
    8. Then do not enter anything and press "Enter"
    9. Type "y" if you are sure you did it right and press "Enter" one more time
    10. **Optional step**, proceed if option "Configure Adapter Manually" was chosen previously in VirtualBox and DHCP Server is disabled:
        1. Choose an option "2) Set interface IP address"
        2. Choose LAN
        3. Configure IPv4 address LAN interface via DHCP? Choose "N"
        4. Enter the new LAN IPv4 address 
        5. Enter the new LAN IPv4 subnet bit count 
        6. Next step asks for the new LAN IPv4 upstream gateway address, do not enter anything and just press "Enter"
        7. Skip IPv6 settings, read and choose accordingly other options if asked
7. Enter an option "6) Reboot system"
8. Login as a root, ensure OPNsense VM has access to the Internet, choose an option "7) Ping host":
    1. Enter "8.8.8.8", see results 
    2. Repeat, but this time instead of "8.8.8.8" enter "www.google.com", see results

### Host OS
OPNsense - Initial Configuration via the Dashboard and 
1. Open a web browser on your PC. In place of URL, enter IP address shown to you by OPNsense on OPNsense VM's screen (e.g., https://192.168.1.1)
2. Login as a "root"
3. Follow the Configuration Wizard (if not asked automatically, try find in System --> Configuration --> Wizard). In most cases you should be fine with the default options, except the following:
    1. General information: update your timezone, no other changes are mandatory
    2. Network [WAN]: Type - DHCP, Block RFC1918 Private Networks - UNcheck.
    3. Network [LAN]: Configure DHCP server - disable (DHCP is running in VirtualBox itself for this network, or might not be needed at all in case of manual network configuration in VirtualBox, enable this only if you know what you are doing)

Securing LAN network:
1. **To be added**

Enable OPT1 and OPT2 interfaces:
1. **To be added**
    
### openSUSE Leap 15.6 xfce
1. Create a new VM, but do not launch it yet. 
2. Open VM settings, proceed to Network
3. Ensure only one network adapter is enabled:
    1. Internal Network (name = "lab_ws_net"; promiscuous mode = "Deny")
4. Launch VM and proceed with the guest OS installation
5. Reboot, if required, login as a user your created during the installation
6. If not installed automatically, proceed with installation of VirtualBox Guest Additions (usually available via VirtualBox's User Interface **for a running VM**: Devices --> Insert Guest Additions CD Image... or/ and Devices --> Upgrade Guest Additions...), reboot if required
7. Ensure openSUSE Leap VM has access to the Internet - in the web browser open www.google.com web page, it should properly load 

### Ubuntu Server 24.04
1. Create a new VM, but do not launch it yet. 
2. Open VM settings, proceed to Network
3. Ensure only one network adapter is enabled:
    1. Internal Network (name = "lab_srv_net"; promiscuous mode = "Allow VMs")
4. Launch VM and proceed with the guest OS installation:
    1. Do not forget to enable OpenSSH server installation when "Installation Wizard" will ask you if it's needed
5. Reboot, if required, login as a user your created during the installation
6. Ensure Ubuntu Server VM has access to the Internet: type "ping -c 4 8.8.8.8", see results 

## Next steps
Now you are ready to proceed to [manual_basic_connection](https://github.com/sorokvja/linux-net-playground/blob/main/baseline/manual_basic_connection.md).  
