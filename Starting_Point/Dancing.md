## Quick Links
[HTB - Starting Point](https://app.hackthebox.com/starting-point)  
[Dancing Walkthrough](blob:https://app.hackthebox.com/2f78ca43-f96d-43ba-90e2-f44c38715bcc) 

## Preparation
1. Connect to the *Starting Point* VPN. See the [[Preparation]] documentation for instructions.
2. Spawn the *Dancing* machine in the *Starting Point* list.
3. Set a variable for the target machine's IP
	1. `export TARGET=<ip_address_of_target>`
	2. `echo $TARGET`
	3. `ping $TARGET` 

## Tasks
1. What does the 3-letter acronym SMB stand for?
	1. *Answer*: Server Message Block
2. What port does SMB use to operate at?
	1. *Answer*: 445 TCP
3. What is the service name for port 445 that came up in our Nmap scan?
	1. *Answer*: microsoft-ds
4. What is the 'flag' or 'switch' we can use with the SMB tool to 'list' the contents of the share?
	1. *Answer*: -L
5. How many shares are there on Dancing?
	1. *Answer*: 4
6. What is the name of the share we are able to access in the end with a blank password?
	1. *Answer*: WorkShares
7. What is the command we can use within the SMB shell to download the files we find?
	1. *Answer*: 
8. Submit root flag
	1. To obtain the root flag, combine the steps above:
		1. Run the `ping $TARGET` command to test connection
		2. Run the `nmap -sV $TARGET` to scan the target machine
		3. Verify installation of *smbclient*: `sudo apt-get install smbclient`
		4. List the shares on the target machine: `smbclient -L $TARGET` 
			1. The `-h` flag will show help for *smbclient*
			2. The -L flag lists the shares
		5. Attempt to login to each share:
			1. `smbclient \\\\$TARGET\\ADMIN$`
			2. `smbclient \\\\$TARGET\\C$` 
			3. `smbclient \\\\$TARGET\\WorkShares` - success
		6. Use the `ls` command to search through the directories in the share
			1. Note: use `help` to list all the commands used in smb
		7. Once the flag is found, use `get <name_of_file>` to pull the file to the directory location where the `smbclient` command was completed
		8. Use `cat <name_of_file>` to display the flag
		9. Success: Machine Pwned!