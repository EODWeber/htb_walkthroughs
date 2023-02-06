## Quick Links
[HTB - Starting Point](https://app.hackthebox.com/starting-point)  
[Dancing Walkthrough](blob:https://app.hackthebox.com/9a446180-85e3-41db-9165-c6869fe7b25d) 

## Preparation
1. Connect to the *Starting Point* VPN. See the [[Preparation]] documentation for instructions.
2. Spawn the *Dancing* machine in the *Starting Point* list.
3. Set a variable for the target machine's IP
	1. `export TARGET=<ip_address_of_target>`
	2. `echo $TARGET`
	3. `ping $TARGET` 

## Tasks
1. Which TCP port is open on the machine?
	1. *Answer*: 6379
2. Which service is running on the port that is open on the machine?
	1. *Answer*: redis
3. What type of database is Redis? Choose from the following options: (i) In-memory Database, (ii) Traditional Database
	1. *Answer*: In-Memory Database
4. Which command-line utility is used to interact with the Redis server? Enter the program name you would enter into the terminal without any arguments.
	1. *Answer*: redis-clire
5. Which flag is used with the Redis command-line utility to specify the hostname?
	1. *Answer*: -h
6. Once connected to a Redis server, which command is used to obtain the information and statistics about the Redis server?
	1. *Answer*: info
7. What is the version of the Redis server being used on the target machine?
	1. *Answer*: 5.0.7
8. Which command is used to select the desired database in Redis?
	1. *Answer*: select
9. How many keys are present inside the database with index 0?
	1. *Answer*: 4
10. Which command is used to obtain all the keys in a database?
	1. *Answer*: keys *
11. Submit root flag
	1. Run `ping $TARGET` to verify connection to machine
	2. Run `nmap -p- -r -sV $TARGET` to check for open ports and services
		1. Note: running without the `-p-` flag will return no results, but a message that indicates an open port
		2. Running with the `-p-` flag takes much longer to run. Using the `-r` flag helps to speed up the command
	3. The open port is *6379/tcp* and is running *redis*
	4. To connect to the *redis server*: `redis-cli -h $TARGET`
	5. Once connected, use `info` to view information about the server
	6. Look for the *Keyspace* section. This is where the databases are listed. In this example, look for *db0*
	7. To select the database, use `select 0` 
	8. To view the keys, use `keys *` 
	9. To view the contents of a key, use `get <key_name>` 
		1. In this case, `get flag` 
	10. Copy the flag value into HTB
	11. Congrats: Machine Pwned!