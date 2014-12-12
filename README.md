BeetRoot -- utility for getting root via SSH
======================================

Beetroot is an SSH utility that automates the process of logging into multiple servers and obtaining root permissions using su or sudo. 

Usage:
------

To run command on host:

    br *host* *command*

    Example: `br noisyserver ls -l /etc`
    
To get a root shell on host:

   `br *host*
    
To run command on multiple hosts:

    beetroot *hostfile* *command*

    Example: `br ~/hosts/prod-webservers.txt uptime`

If the first parameter is a valid file, BeetRoot will read it to obtain a list of hosts to run the command on.
In the example above, ~/hosts/prod-webservers.txt contains a list of webserver hostnames, one on each line.

Credentials file:
-----------------

The credentials are read from ~/.ssh/beetroot.creds
    
This must be a whitespace delimited text file. The fields are:

    1. Username
    2. Password or * to prompt
    3. Type, can be login, su or sudo or any combination separated by commas
    4. Regexp matching the hostnames this credential will be used for

See beetroot.creds.example for some example lines.
