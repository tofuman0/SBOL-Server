# Shutokou Battle Online Server
## Overview
Fans of the Toyko Xtreme Racer Series may not be aware that back in 2003-2005 Genki released an online PC version of the game. However this was only available to Japan.

As the game wasn't popular outside of Japan it seems that absolutely no documentation was made of how the game worked or any packet logs of the game were made. I reverse engineered the network protocol and have created a server that people are free to play on. It isn't quite 100% functional but playable.

## Downloading
Clone this repository with the recurse switch so that you obtain the Battle Server, DB Server and the libraries required: git clone https://github.com/tofuman0/SBOL-Server.git --recurse

## Building
The project includes compiled libraries and header files already so should build out of the box.

## Configuring
### DB Server
1. First configure the server by editing the config.json file. If this doesn't yet exist you can run the server and a default configuration file will be created. SQLite is the default database type so if you plan on using SQLite you can skip this step, but you can also configure MySQL if preferred.
2. Now create a battle server key. This is used to authenticate the battle server with the database server. To do this run the following command:

```
"SBOL DB Server.exe" -createkey
```

This will create serverkey.bin which will need to be copied over to the battle server's directory. It will also insert the key into the database.

3. Finally create a admin account using the following command:
```
"SBOL DB Server.exe" -createaccount USERNAME PASSWORD EMAIL 255
```
The 255 value is the permission flags. 255 grants full access. Use 0 for a standard user.
4. Run "SBOL DB Server.exe".
### Battle Server
1. Copy the serverkey.bin file generated from the database server into the battle server's folder.
2. Configure the battle server by editing the config.json file. If this doesn't yet exist you can run the server and a default configuration file will be created. By default it will connect to localhost.
3. Run "SBOL Battle Server.exe".
### Client
1. Edit the SERVER.INI file to connect to your server's IP address. The client requires 2 servers in this file. So you can enter your battle server IP address 2 times. This is because new accounts join the first server and when you switch join the main server after leaving the beginners course it will connect to the 2nd server in the file.
```
[SERVER01]
TYPE=0
ADDR=127.0.0.1
PORT=47701
SIDE=0

[SERVER02]
TYPE=0
ADDR=127.0.0.1
PORT=47701
SIDE=0
```
It doesn't matter what is in the square brakets so you are free to enter whatever you like there. By default SERVER01 and SERVER02 are used.
TYPE appears to exclude the server from connections when set to anything other than 0
ADDR is the battle server IP address
PORT is the battle server port
SIDE is unclear what this does but is set to 0 in the default file.