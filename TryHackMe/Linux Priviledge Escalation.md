# Enumeration
- `hostname`
  The `hostname` command will return the hostname of the target machine
- `uname -a`
  Will print system information giving us additional detail about the kernel used by the system
- /proc/version
  The proc filesystem (procfs) provides information about the target system processes
- /etc/issue
  Systems can also be identified by looking at the `/etc/issue` file. This file usually contains some information about the operating system but can easily be customized or changed.
- `ps`
	The `ps` command is an effective way to see the running processes on a Linux system. Typing `ps` on your terminal will show processes for the current shell.\
	The output of the `ps` (Process Status) will show the following;
	- PID: The process ID (unique to the process)
	- TTY: Terminal type used by the user
	- Time: Amount of CPU time used by the process (this is NOT the time this process has been running for)
	- CMD: The command or executable running (will NOT display any command line parameter)
- `env`
  The `env` command will show environmental variables.
- `sudo -l`
  The target system may be configured to allow users to run some (or all) commands with root privileges. The `sudo -l` command can be used to list all commands your user can run using `sudo`.
- `ls`
  While looking for potential privilege escalation vectors, please remember to always use the `ls` command with the `-la` parameter. The example below shows how the “secret.txt” file can easily be missed using the `ls` or `ls -l` commands.
- `id`
  The `id` command will provide a general overview of the user’s privilege level and group memberships.
- /etc/passwd
  Reading the `/etc/passwd` file can be an easy way to discover users on the system.
  ![[Pasted image 20241118212638.png]]
  ![[Pasted image 20241118212704.png]]
- `history`
  Looking at earlier commands with the `history` command can give us some idea about the target system and, albeit rarely, have stored information such as passwords or usernames.
- `ifconfig`
  The `ifconfig` command will give us information about the network interfaces of the system
- `nestat`
  The `netstat` command can be used with several different options to gather information on existing connections.
   -  netstat -a`: shows all listening ports and established connections.
   - `netstat -at` or `netstat -au` can also be used to list TCP or UDP protocols respectively.
   - `netstat -l`: list ports in “listening” mode. These ports are open and ready to accept incoming connections. This can be used with the “t” option to list only ports that are listening using the TCP protocol (below)
- `find`
  - `find / -type f -perm 0777`: find files with the 777 permissions (files readable, writable, and executable by all users)
- `find / -perm a=x`: find executable files
- `find /home -user frank`: find all files for user “frank” under “/home”
- `find / -mtime 10`: find files that were modified in the last 10 days
- `find / -atime 10`: find files that were accessed in the last 10 day
- `find / -cmin -60`: find files changed within the last hour (60 minutes)
- `find / -amin -60`: find files accesses within the last hour (60 minutes)
- `find / -size 50M`: find files with a 50 MB size
	- `find / -writable -type d 2>/dev/null` : Find world-writeable folders
- `find / -perm -222 -type d 2>/dev/null`: Find world-writeable folders
- `find / -perm -o w -type d 2>/dev/null`: Find world-writeable folders
  - `find / -perm -o x -type d 2>/dev/null` : Find world-executable folders
