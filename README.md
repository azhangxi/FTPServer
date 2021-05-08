# FTPServer
### Initialization ###
Do a "make" followed by "./CSftp PORTNUMBER".
The program will not work if the first argument is not a valid port number,
or if there is more than one argument. 
This will initiate the server and it will start to accept incoming connections. 
To connect, do "Telnet localhost PORTNUMBER" if run on the same computer as the server.

For each connection, it will create a thread. 
Only when the first connection finishes 
will the second connection be attended to, and so on.

### Commands Supported ###
- USER cs317
- QUIT
- TYPE A or TYPE I
- MODE S
- STRU F
- RETR filename
- PASV
- NLST

### Detailed instructions ###
Once connected, you can start your session with "USER cs317".
The only commands available prior to logging in are USER and QUIT.

Once logged in, the rest of the commands are available.
TYPE, MODE, and STRU will set the associated variables,
but will not affect the transfer commands.

PASV must be done before either NLST or RETR.
After PASV, open another client and do "Telnet localhost PASVPORT".
The new client will receive the information from NLST or RETR.

After NLST or RETR is done, the passive server will close.
You must do a PASV each time you want to do NLST or RETR.
The passive server will close even if the RETR was unsuccessful.

### Examples ###
For example, the following will work:

PASV
NLST
PASV
RETR test.txt

But the following will not work:

PASV
NLST
RETR test.txt

Finally, any commands that do not take parameters (QUIT, PASV, NLST) 
will simply ignore those parameters.
