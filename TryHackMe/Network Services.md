# Understanding SMB
## What is SMB?
SMB - Server Message Block Protocol - is a client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network. [source](https://searchnetworking.techtarget.com/definition/Server-Message-Block-Protocol)
Servers make file systems and other resources (printers, named pipes, APIs) available to clients on the network. Client computers may have their own hard disks, but they also want access to the shared file systems and printers on the servers.
The SMB protocol is known as a response-request protocol, meaning that it transmits multiple messages between the client and server to establish a connection. Clients connect to servers using TCP/IP (actually NetBIOS over TCP/IP as specified in RFC1001 and RFC1002), NetBEUI or IPX/SPX.

## How does SMB work?

![](https://i.imgur.com/XMnru12.png)
Once they have established a connection, clients can then send commands (SMBs) to the server that allow them to access shares, open files, read and write files, and generally do all the sort of things that you want to do with a file system. However, in the case of SMB, these things are done over the network.
## What runs SMB?
Microsoft Windows operating systems since Windows 95 have included client and server SMB protocol support. Samba, an open source server that supports the SMB protocol, was released for Unix systems.
# Understanding Telnet
## What is Telnet?
Telnet is an application protocol which allows you, with the use of a telnet client, to connect to and execute commands on a remote machine that's hosting a telnet server.
The telnet client will establish a connection with the server. The client will then become a virtual terminal- allowing you to interact with the remote host.
## Replacement
Telnet sends all messages in clear text and has no specific security mechanisms. Thus, in many applications and services, Telnet has been replaced by SSH in most implementations.
## How does Telnet work?
The user connects to the server by using the Telnet protocol, which means entering "telnet" into a command prompt. The user then executes commands on the server by using specific Telnet commands in the Telnet prompt. You can connect to a telnet server with the following syntax: "telnet [ip]  [port]"

---
# Understanding NFS
## What is NFS?
NFS stands for "Network File System" and allows a system to share directories and files with others over a network. By using NFS, users and programs can access files on remote systems almost as if they were local files. It does this by mounting all, or a portion of a file system on a server. The portion of the file system that is mounted can be accessed by clients with whatever privileges are assigned to each file.
## How does NFS work?
We don't need to understand the technical exchange in too much detail to be able to exploit NFS effectively- however if this is something that interests you, I would recommend this resource: [https://docs.oracle.com/cd/E19683-01/816-4882/6mb2ipq7l/index.html](https://docs.oracle.com/cd/E19683-01/816-4882/6mb2ipq7l/index.html)

First, the client will request to mount a directory from a remote host on a local directory just the same way it can mount a physical device. The mount service will then act to connect to the relevant mount daemon using RPC.

The server checks if the user has permission to mount whatever directory has been requested. It will then return a file handle which uniquely identifies each file and directory that is on the server.

If someone wants to access a file using NFS, an RPC call is placed to NFSD (the NFS daemon) on the server. This call takes parameters such as:
-  The file handle
-  The name of the file to be accessed
-  The user's, user ID
-  The user's group ID  
These are used in determining access rights to the specified file. This is what controls user permissions, I.E read and write of files.  

## What runs NFS?
Using the NFS protocol, you can transfer files between computers running Windows and other non-Windows operating systems, such as Linux, MacOS or UNIX.

A computer running Windows Server can act as an NFS file server for other non-Windows client computers. Likewise, NFS allows a Windows-based computer running Windows Server to access files stored on a non-Windows NFS server.

**More Information:**
Here are some resources that explain the technical implementation, and working of, NFS in more detail than I have covered here.
[https://www.datto.com/blog/what-is-nfs-file-share/](https://www.datto.com/blog/wat-is-nfs-file-share/)  
[http://nfs.sourceforge.net/](http://nfs.sourceforge.net/)
[https://wiki.archlinux.org/index.php/NFS](https://wiki.archlinux.org/index.php/NFS)