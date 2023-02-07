## Quick Links
[HTB - Starting Point](https://app.hackthebox.com/starting-point)  
[Crocodile Walkthrough](blob:https://app.hackthebox.com/5248eb6f-6584-44cf-aa83-f5873a79047e) 

## Tasks
1. What Nmap scanning switch employs the use of default scripts during a scan?
	1. *Answer*: -sC
2. What service version is found to be running on port 21?
	1. *Answer*: vsftpd 3.03
3. What FTP code is returned to us for the "Anonymous FTP login allowed" message?
	1. *Answer*: 230
4. After connecting to the FTP server using the ftp client, what username do we provide when prompted to log in anonymously?
	1. *Answer*: anonymous
5. After connecting to the FTP server anonymously, what command can we use to download the files we find on the FTP server?
	1. *Answer*: get
6. What is one of the higher-privilege sounding usernames in 'allowed.userlist' that we download from the FTP server?
	1. *Answer*: admin
7. What version of Apache HTTP Server is running on the target host?
	1. *Answer*: httpd 2.4.41 ((Ubuntu))
8. What switch can we use with Gobuster to specify we are looking for specific filetypes?
	1. *Answer*: -x
9. Which PHP file can we identify with directory brute force that will provide the opportunity to authenticate to the web service?
	1. *Answer*: login.php
10. Submit root flag
	1. Ping the machine to verify connectivity
	2. Run an nmap scan to check for open ports and running services
		1. `sudo nmap -sC -sV $TARGET` 
	3. Connect to FTP to browse and pull files
		1. `ftp $TARGET` - using the *anonymous* user
		2. `ls` to view the files
		3. `get <file-name>` to download the file
	4. View the contents of the files with:
		1. `cat <file-name>`
	5. Run *gobuster* to find an authentication page to test the discovered auth
		1. `gobuster dir --url http://$TARGET/ --wordlist ~/Tools/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt -x php,html`
		2. Returns: `/index.html`, `/login.php`, `/assets`
	6. Try the passwords obtained earlier with the *admin* account to access the admin pane and retrieve the flag
	7. Copy and Paste the flag into HTB
	8. Success: Machine Pwned!