# CSCE 438 - HW2: An Improved Chat Room Service
###Vincent Velarde, Kyle Rowland
February 2017

###Files: [fb.proto](https://github.com/vinvelarde/CSCE438-HW2/blob/master/fb.proto), [fbc.cpp](https://github.com/vinvelarde/CSCE438-HW2/blob/master/fbc.cpp), [fbsd.cpp](https://github.com/vinvelarde/CSCE438-HW2/blob/master/fbsd.cpp), [Makefile](https://github.com/vinvelarde/CSCE438-HW2/blob/master/Makefile)

###Notes:
  - This project roughly mimicks the functionality of Twitter
  - See comment block at the head of each source file for additional information
  

###Compiling and Running the Program:
- Use "make all" to compile and "make clean" to clear everything but source files
- Run server with "./server <port>"
- Run client with "./client <hostname> <port> <username>"

##Functionality Overview:
###Client Code - [fbc.cpp](https://github.com/vinvelarde/CSCE438-HW2/blob/master/fbc.cpp): 
Connects to server and waits for user to issue commands, then takes some action based on the command:
- If user issues LIST command, the "List (User) returns (stream user)" RPC is called.
- If the user issues JOIN or LEAVE command, the "Following (Action) returns (SendMsg)" RPC is called.
- If the user issues CHAT command, the client leaves command mode and enters chat mode. In chat mode the "Msg (SendMSG) returns (SendMSG)"    RPC is called for any input.

###Server Code - [fbsd.cpp](https://github.com/vinvelarde/CSCE438-HW2/blob/master/fbsd.cpp):
Starts server and waits for client input.
- When new user joins the server, their username will be checked against a list of all users. If the name doesn't already exist, it will be added.
- Each client will have a text file containing their messages and the messages of the users they follow.
- Client messages will be written to the files of all their followers
- When a client switches to chat mode they will be sent the past 20 messages from their file
