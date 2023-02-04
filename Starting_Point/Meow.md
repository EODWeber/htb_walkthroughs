## Quick Links
[Meow Walkthrough - HTB](blob:https://app.hackthebox.com/2c5bbd81-7479-4cb2-b11c-f8451831980a) 

## Preparation
1. Connect to the *Starting Point VPN*. L. ok for help in the [[Preparation]] documentation.
2. Start the target machine.
	1. Navigate to the [HTB - Starting Point](https://app.hackthebox.com/starting-point).
	2. Expand the *Meow* machine. 
	3. Click *Spawn Machine* button
		1. Note the *IP Address* of the machine

## Tasks
1. What does the acronym VM stand for?
	1. *ANSWER*: Virtual Machine
2. What tool do we use to interact with the operating system in order to issue commands via the command line, such as the one to start our VPN connection? It's also known as a console or shell.
	1. *ANSWER*: Terminal
3. What service do we use to form our VPN connection into HTB labs?
	1. *ANSWER*: OpenVPN
4. What is the abbreviated name for a 'tunnel interface' in the output of your VPN boot-up sequence output?
	1. *ANSWER*: tun
5. What tool do we use to test our connection to the target with an ICMP echo request?
	1. *ANSWER*: nmap
6. What service do we identify on port 23/tcp during our scans?
	1. *ANSWER*: telnet
7. What username is able to log into the target over telnet with a blank password?
	1. *ANSWER*: root
8. Submit root flag
	1. To obtain the root flag, you must combine the steps from above.
		1. Open Terminal
		2. Establish connection to VPN
		3. Check for open ports on the target machine
			1. `nmap <IP of Spawned Machine> 
			2. This reveals open port *23/tcp*
		4. Use *telnet* to connect to the machine
			1. `telnet <IP of Spawned Machine>
		5. Enter the name of the `root` user
	2. Once access is granted, list the files in the root directory
		1. `ls`
		2. You'll see a file named *flag.txt*
	3. List the contents of the file with *cat* command
		1. `cat flag.txt`
	4. Copy and paste the value into HTB
	5. Success: Machine Pwned