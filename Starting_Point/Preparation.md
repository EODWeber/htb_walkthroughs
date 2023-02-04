**Hack the Box** (HTB) is a service which uses virtual machines and networks to teach hacking. The service requires a VPN connection and an operating system which contains the tools needed for hacking.

HTB provides a virtual machine they call Pwnbox which can be hosted and accessed through their service. However, this box is expensive, and can instead be installed as a VM on a local machine. The instance is based on ParrotOS, which is built upon Ubuntu 64-bit.

Once the VM is installed, a Virtual Private Network (VPN) must be established between Pwnbox and the HTB network in order to access their environments.

This document is a walkthrough for completing the preparations to connect to the HTB services.

## TOC
[[#Quick Links]]  
[[#VM Configuration]]  
	[[#Install Pwnbox]]  
	[[#Install VPN]]  

## Quick Links
[Hack the Box Website - Home](https://app.hackthebox.com/home)  
[ParrotOS - Home](https://parrotsec.org/)  
[ParrotOS - Downloads](https://parrotsec.org/download)  
[VMWare Fusion Player](https://vmware.com/products/fusion/fusion-evaluation.html)  
[VMWare Fusion - Customer Connect](https://customerconnect.vmware.com/evalcenter?p=fusion-player-personal-13)  

## VM Configuration
To install virtual machines, your host machine needs to have a type 2 hypervisor software. Availability may vary depending on Operating System (OS), but we chose to use [VM Ware Fusion Player](https://www.vmware.com/products/fusion/fusion-evaluation.html) which is available with a free personal use license (registration required). If you've registered already, use  [Customer Connect](https://customerconnect.vmware.com/evalcenter?p=fusion-player-personal-13) to get your license key or download the software.

### Install Pwnbox
1. Download the ISO file from the ParrotOS downloads page. There are multiple versions, but I recommend the Hack the Box version which is the same instance provided in their hosted Pwnbox system.
2. Once the ISO is obtained, open VMWare and build a VM using the ParrotOS ISO file.
	1. The only setting that isn't default is to select *Linux > Ubuntu 64-bit* for the OS.
	2. VMWare may yell about *Disable Side Channel Mitigations*. If this happens, power off the VM, open the VM settings, navigate to advanced, and check the box for the setting at the bottom.
3. Turn on the VM. With Fusion, there is a play icon in the main window. Click that and it'll start the VM.
4. Once the VM loads, a menu will be presented to install. Install the VM.
5. After installation, you'll be presented with a desktop which contains a few files. Look for the install file and run it. This will prompt to create a user and setup the system.
6. After installation the system will automatically reboot and prompt for login.

### Install VPN
1. Obtain the VPN configuration from HTB.
	1. Click the <span style=color:red>red</span> *Connect to HTB* button in the top right of the [HTB Website](https://app.hackthebox.com/home).
	2. Select the VPN instance you want to connect to. If this is your first time, connect to *Starting Point*.
	3. Because you've installed your own VM, select the *OpenVPN* option.
	4. There are 2 dropdowns. The top one is region, the bottom is a server. Select the options that best suit your needs and location.
	5. Select a port option. I haven't noticed a specific need for selecting one or the other.
	6. Click the *Download VPN* button. This will provide an OpenVPN configuration file.
2. Import the file to your VM
	1. Drag the OpenVPN configuration file from your host machine to the Pwnbox VM Desktop.
		1. You can move this config to any location as long as you remember where it is.
	2. Open terminal and import the configuration into Network Manager.
		1. `nmcli connection import type openvpn file ~/path/to/.ovpn/file`
3. Connect to the VPN.
	1. Check that the connection was imported.
		1. Click the network icon in the top right.
		2.  Selct the *VPN Connections* dropdown. 
		3. Click the VPN connection to connect to HTB. This may take a few moments to complete the connection
	2. Verify the connection in HTB
		1. On the [HTB Website](https://app.hackthebox.com/home), there will now be a <span style=color:green>green</span> *VPN Icon* with the name of the VPN
		2. Your VM should also confirm the connection was successful
