## Quick Links
[HTB - Starting Point](https://app.hackthebox.com/starting-point)  
[Sequel Walkthrough](blob:https://app.hackthebox.com/200d9f06-6f6b-4147-bf80-29728f3300f8) 

## Tasks
1. During our scan, which port do we find serving MySQL?
	1. *Answer*: 3306
2. What community-developed MySQL version is the target running?
	1. *Answer*: MariaDB
3. When using the MySQL command line client, what switch do we need to use in order to specify a login username?
	1. *Answer*: -u
4. Which username allows us to log into this MariaDB instance without providing a password?
	1. *Answer*: root
5. In SQL, what symbol can we use to specify within the query that we want to display everything inside a table?
	1. *Answer*: *
6. In SQL, what symbol do we need to end each query with?
	1. *Answer*: ;
7. There are three databases in this MySQL instance that are common across all MySQL instances. What is the name of the fourth that's unique to this host?
	1. *Answer*: htb
8. Submit root flag
	1. Ping the target to verify connectivity
	2. Run an nmap scan
		1. `sudo nmap -sC -sV $TARGET` 
	3. Disconnect from VPN and install *MySQL Tools* 
		1. `sudo apt update && sudo apt install mysql*` 
		2. `mysql --help`
	4. Authenticate into the remote SQL server
		1. `mysql -h $TARGET -u root` 
		2. Test connection with: `show databases;`
	5. Select the *htb* database
		1. `use htb`
	6. Show the tables, then show the contents of each table:
		1. `show tables;` - outputs *config* and *users* tables
		2. `select * from config;` - shows the flag
	7. Copy and paste the flag to HTB.
	8. Success: Machine Pwned!