BeetRoot &mdash; utility for getting root via SSH
======================================

Beetroot is an SSH utility that automates the process of logging into multiple servers and obtaining root permissions using su or sudo. 

Usage:
------

`br host [command]`

Or:

`br hostfile [command]`

Examples:
---------

To get a root shell on host:

    br yourhost

To exit from the shell, either press `Ctrl-]` or type exit twice.
    
To run command on host:

    br yourhost command

Example: list the contents of the /etc directory: `br myserver ls -l /etc`

Beetroot exits automatically once the command completes.
    
To run command on multiple hosts:

    br hostfile command

Example: count how many httpd processes are running on each web server:

    br ~/hosts/prod-webservers.txt 'echo -n "$HOSTNAME: "; pgrep httpd | wc -l' | grep -v BEETROOT


If the first parameter is a valid file, BeetRoot will read it to obtain a list of hosts to run the command on.
In the example above, `~/hosts/prod-webservers.txt` contains a list of webserver hostnames, one on each line.


To get a shell on multiple hosts use `br hostfile`

Example: `br ~/hosts/prod-webservers.txt`

This command will log into the first server and give you a root shell. Once you log out of this shell, it will automatically log into the next one.

Credentials file:
-----------------

The credentials are read from `~/.ssh/beetroot.creds`
    
This must be a whitespace delimited text file. The fields are:

1. Username
2. Password or * to prompt
3. Type, can be login, su or sudo or any combination separated by commas
4. Regexp matching the hostnames this credential will be used for

See `beetroot.creds.example` for some example lines.

It is recommended that you restrict the permissions on your credentials file for your user only, by running the following command:

    chmod 600 ~/.ssh/beetroot.creds
