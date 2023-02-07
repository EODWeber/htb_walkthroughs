## Quick Links
[HTB - Starting Point](https://app.hackthebox.com/starting-point)  
[Synced Walkthrough](blob:https://app.hackthebox.com/6639cd6d-c389-41c7-b3d6-d0e011d71a37) 

## Preparation
1. Connect to the *Starting Point* VPN. See the [[Preparation]] documentation for instructions.
2. Spawn the *Dancing* machine in the *Starting Point* list.
3. Set a variable for the target machine's IP
	1. `export TARGET=<ip_address_of_target>`
	2. `echo $TARGET`
	3. `ping $TARGET` 

## Tasks
1. What is the default port for rsync?
	1. *Answer*: 873
2. How many TCP ports are open on the remote host?
	1. *Answer*: 1
3. What is the protocol version used by rsync on the remote machine?
	1. *Answer*: 31
4. What is the most common command name on Linux to interact with rsync?
	1. *Answer*: rsync
5. What credentials do you have to pass to rsync in order to use anonymous authentication? anonymous:anonymous, anonymous, None, rsync:rsync
	1. *Answer*: None
6. What is the option to only list shares and files on rsync? (No need to include the leading -- characters)
	1. *Answer*: list-only
7. Submit root flag
	1. Ping the target to confirm connection
	2. Run an nmap scan to check for open ports and running services
		1. `nmap -p- -r --min-rate=100 $TARGET` 
	3. Rsync is installed by default. Run it against the target to see what directories are available to the anonymous user:
		1. `rsync --list-only $TARGET::` 
		2. This shows a share called *public* which is listed as an *Anonymous Share* 
	4. List what is inside the *public* share:
		1. `rsync --list-only $TARGET::public` 
		2. This shows there is a *flag.txt* file in the public share
	5. Move the flag file to your machine
		1. Syntax: `rsync <username>@<target>::<path> <destination>`
		2. Example: `rsync $TARGET::public/flag.txt ~/Desktop/flag.txt` 
	6. View, copy, and paste the flag into HTB:
		1. `cat flag.txt`
	7. Success: Machine Pwned!