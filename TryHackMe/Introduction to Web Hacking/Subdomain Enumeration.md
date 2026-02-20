---
tags:
  - concept
  - tool
  - recon
  - web-app
link: https://tryhackme.com/room/subdomainenumeration
---
# SSL/TLS certificate
When an SSL/TLS (Secure Sockets Layer/Transport Layer Security) certificate is created for a domain by a CA (Certificate Authority), CA's take part in what's called "Certificate Transparency (CT) logs". These are publicly accessible logs of every SSL/TLS certificate created for a domain name. The purpose of Certificate Transparency logs is to stop malicious and accidentally made certificates from being used. We can use this service to our advantage to discover subdomains belonging to a domain, sites like [crt.sh](https://crt.sh) offer a searchable database of certificates that shows current and historical results.
# Search Engine
Search engines contain trillions of links to more than a billion websites, which can be an excellent resource for finding new subdomains. Using advanced search methods on websites like [Google](Content%20Discovery.md#Google%20Hacking%20/%20Dorking), such as the `site: filter`, can narrow the search results. For example, `site:*.domain.com -site:www.domain.com` would only contain results leading to the domain name domain.com but exclude any links to www.domain.com; therefore, it shows us only subdomain names belonging to domain.com.
# DNS Bruteforce
Bruteforce DNS (Domain Name System) enumeration is the method of trying tens, hundreds, thousands or even millions of different possible subdomains from a pre-defined list of commonly used subdomains. Because this method requires many requests, we automate it with tools to make the process quicker. Tools: dnsrecon, [Sublist3r](https://www.kali.org/tools/sublist3r/)
# Virtual Hosts
Some subdomains aren't always hosted in publically accessible DNS results, such as development versions of a web application or administration portals. Instead, the DNS record could be kept on a private DNS server or recorded on the developer's machines in their **/etc/hosts** file (or **c:\windows\system32\drivers\etc\hosts** file for Windows users), which maps domain names to IP addresses. 

Because web servers can host multiple websites from one server when a website is requested from a client, the server knows which website the client wants from the Host header. We can utilize this host header by making changes to it and monitoring the response to see if we've discovered a new website.

```shell
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.64.150.119
```

The above command uses the -w switch to specify the wordlist we are going to use. The **-H** switch adds/edits a header (in this instance, the Host header), we have the **FUZZ** keyword in the space where a subdomain would normally go, and this is where we will try all the options from the wordlist.

Because the above command will always produce a valid result, we need to filter the output. We can do this by using the page size result with the **-fs** switch.
```shell-session
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.64.150.119 -fs {size}
```

This command has a similar syntax to the first apart from the **-fs** switch, which tells **ffuf** to ignore any results that are of the specified size.