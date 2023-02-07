## Quick Links
[HTB - Starting Point](https://app.hackthebox.com/starting-point)  
[Preignition Walkthrough](blob:https://app.hackthebox.com/59cb7b89-1522-4837-a0c8-c11eb18316f1) 

## Preparation
1. Connect to the *Starting Point* VPN. See the [[Preparation]] documentation for instructions.
2. Spawn the *Dancing* machine in the *Starting Point* list.
3. Set a variable for the target machine's IP
	1. `export TARGET=<ip_address_of_target>`
	2. `echo $TARGET`
	3. `ping $TARGET` 

## Tasks
1. Directory Brute-forcing is a technique used to check a lot of paths on a web server to find hidden pages. Which is another name for this? (i) Local File Inclusion, (ii) dir busting, (iii) hash cracking.
	1. *Answer*: dir busting
2. What switch do we use for nmap's scan to specify that we want to perform version detection
	1. *Answer*: -sV
3. What does Nmap report is the service identified as running on port 80/tcp?
	1. *Answer*: http
4. What server name and version of service is running on port 80/tcp?
	1. *Answer*: nginx 1.14.2
5. What switch do we use to specify to Gobuster we want to perform dir busting specifically?
	1. *Answer*: dir
6. When using gobuster to dir bust, what switch do we add to make sure it finds PHP pages?
	1. *Answer*: -x php
	2. NOTE: For some reason, the full help list is not displaying
7. What page is found during our dir busting activities?
	1. *Answer*: admin.php
8. What is the HTTP status code reported by Gobuster for the discovered page?
	1. *Answer*: 200
9. Submit root flag
	1. Verify connection to target with *ping*
	2. Do an *nmap* scan of target
	3. Open a browser and navigate to the *$TARGET* IP address to see that the machine is hosting an *nginx web server*
	4. Install *gobuster* if not already installed
		1. Verify installation with `gobuster -h`
		2. Pwnbox comes with it pre-installed
	5. Run gobuster against the target
		1. `gobuster dir -w /usr/share/wordlists/dirb/common.txt -u $TARGET`
	6. Navigate to the target ip with the discovered /admin.php directory
	7. Since the server looks unconfigured, the default nginx auth can be used to get in: *admin/admin*
	8. This displays the flag in the browser. Copy and paste into HTB.
	9. Success: Machine Pwned!