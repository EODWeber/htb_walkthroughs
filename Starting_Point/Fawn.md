## Quick Links
[HTB - Starting Point](https://app.hackthebox.com/starting-point)  
[Fawn Walkthrough](blob:https://app.hackthebox.com/b45927ab-95ed-4ea7-901c-319931c2dce6) 

## Preparation
1. Connect to the *Starting Point* VPN. See the [[Preparation]] documentation for instructions.
2. Spawn the *Fawn* machine in the *Starting Point* list.
3. Set a variable for the target machine's IP
	1. `export TARGET=<ip_address_of_target>`
	2. `echo $TARGET`
	3. `ping $TARGET` 

## Tasks
1. What does the 3-letter acronym FTP stand for?
	1. *Answer*: File Transfer Protocol
2. Which port does the FTP service listen on usually?
	1. *Answer*: 21
3. What acronym is used for the secure version of FTP?
	1. *Answer*: SFTP
4. What is the command we can use to send an ICMP echo request to test our connection to the target?
	1. *Answer*: Ping
5. From your scans, what version is FTP running on the target?
	1. *Answer*: vsftpd 3.0.3
6. From your scans, what OS type is running on the target?
	1. *Answer*: Unix
7. What is the command we need to run in order to display the 'ftp' client help menu?
	1. *Answer*: `ftp -h`
8. What is username that is used over FTP when you want to log in without having an account?
	1. *Answer*: anonymous
	2. Password for *anonymous* user can be anything
9. What is the response code we get for the FTP message 'Login successful'?
	1. *Answer*:
10. There are a couple of commands we can use to list the files and directories available on the FTP server. One is dir. What is the other that is a common way to list files on a Linux system.
	1. *Answer*:
11. What is the command used to download the file we found on the FTP server?
	1. *Answer*:
12. Submit root flag
	1. To obtain the root flag, follow the guidance of the questions above:
		1. Check that the connection to the machine is working with `ping $TARGET`
		2. Run `nmap $TARGET` to get the open ports
			1. You'll see that `21/tcp` is open and that the `ftp` service is using the port
		3. We need to get more information from the `nmap` command. This can be done by using the `-sV` flag, which will get the version: `nmap -sV $TARGET` 
			1. The output adds a *VERSION* column which provides the answer to quesiton 5 above.
			2. We also get the additional info for what OS is running: *Unix*
		4. Check for *ftp*. Install it if the command is not found.
			1. `ftp -h` 
			2. Disconnect from the HTB VPN. 
			3. Install: `sudo apt-get install ftp -y` 
				1. You may need to do `update` and/or `upgrade` 
			4. Don't forget to reconnect to the VPN.
			5. Then check the version again.
		5. Use *ftp* to connect to the target machine
			1. `ftp $TARGET`
			2. Use *anonymous* as the username
			3. Use anything as the password. Example: *anon123* 
		6. Use `help` to list the commands for ftp once connected
		7. To list the files in the current directory, use `ls`
		8. To download a file, use `get <name_of_file`
			1. Note: this file will download to the directory where the *ftp* command was used
		9. Use the `exit` command to leave *ftp*
		10. View the contents of the file with `cat <filename>`
			1. Copy and paste the value of the flag into HTB
			2. Congrats: Machine Pwned!