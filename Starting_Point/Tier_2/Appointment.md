## Quick Links
[HTB - Starting Point](https://app.hackthebox.com/starting-point)  
[Appointment Walkthrough](blob:https://app.hackthebox.com/5d8c6c15-8958-408c-94be-1f8037e1cbfa) 

## Tasks
1. What does the acronym SQL stand for?
	1. *Answer*: Structured Query Language
2. What is one of the most common type of SQL vulnerabilities?
	1. *Answer*: SQL Injection
3. What does PII stand for?
	1. *Answer*: Personally Identifiable Information
4. What is the 2021 OWASP Top 10 classification for this vulnerability?
	1. *Answer*: A03:2021-Injection
5. What does Nmap report as the service and version that are running on port 80 of the target?
	1. *Answer*: Apache httpd 2.4.38 ((Debian))
6. What is the standard port used for the HTTPS protocol?
	1. *Answer*: 443
7. What is a folder called in web-application terminology?
	1. *Answer*: directory
8. What is the HTTP response code is given for 'Not Found' errors?
	1. *Answer*: 404
9. Gobuster is one tool used to brute force directories on a webserver. What switch do we use with Gobuster to specify we're looking to discover directories, and not subdomains?
	1. *Answer*: dir
10. What single character can be used to comment out the rest of a line in MySQL?
	1. *Answer*: #
11. If user input is not handled carefully, it could be interpreted as a comment. Use a comment to login as admin without knowing the password. What is the first word on the webpage returned?
	1. *Answer*: Congratulations
12. Submit root flag
	1. Ping the machine to verify connection
	2. Run scan on machine to check for open ports and services
		1. `nmap -sV -sC $TARGET`
		2. This shows that only port 80 is available
	3. Use *gobuster* to brute force check for directories and files on the web server
		1. `gobuster -h` 
		2. Clone a new wordlist (disconnect VPN): `git clone https://github.com/danielmiessler/SecLists.git`
		3. `gobuster dir --url http://$TARGET/ --wordlist ~/Tools/SecLists/directory-list-2.3-small.txt`
			1. This is time consuming and will fail, but is good practice
	4. Attempt some common default credential pairs in the login form
		1. This will fail as well, but again is good practice
		2. admin:admin
		3. guest:guest
		4. user:user
		5. root:root
		6. administrator:password
	6. Attempt a SQL injection attack
		1. In this case, we are trying to search for a user and interrupt the search for a password.
		2. Simply input the user as `admin'#` and input anything for the password (it can't be blank) and you should be presented with the flag page
	7. Copy and paste the flag into HTB
	8. Success: Machine Pwned