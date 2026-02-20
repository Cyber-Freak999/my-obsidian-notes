---
link: https://tryhackme.com/room/oscommandinjection
tags:
  - concept
  - exploitation
  - web-app
---
# What is Command Injection
Command Injection is a vulnerability that occurs when an attacker manipulates input fields to inject malicious commands into a vulnerable application. This can lead to unauthorised execution of arbitrary commands on the targeted server, potentially resulting in data breaches, system compromise, or unintended operations.
It is the abuse of an application's behaviour to execute commands on the operating system, using the same privileges that the application on a device is running with. For example, achieving command injection on a web server running as a user named `joe` will execute commands under this `joe` user - and therefore obtain any permissions that `joe` has.

Command injection is also often known as “Remote Code Execution” (RCE) because of the ability to remotely execute code within an application. These vulnerabilities are often the most lucrative to an attacker because it means that the attacker can directly interact with the vulnerable system. For example, an attacker may read system or user files, data, and things of that nature.  

For example, being able to abuse an application to perform the command `whoami` to list what user account the application is running will be an example of command injection.

Command injection was one of the top ten vulnerabilities reported by Contrast Security’s AppSec intelligence report in 2019. ([Contrast Security AppSec., 2019](https://www.contrastsecurity.com/security-influencers/insights-appsec-intelligence-report)). Moreover, the [OWASP](13.%20Injections.md) constantly proposes vulnerabilities of this nature as one of the top ten vulnerabilities of a web application ([OWASP framework](https://owasp.org/www-project-top-ten/)).
# Discovering Command Injection
This vulnerability exists because applications often use functions in programming languages such as PHP, Python and NodeJS to pass data to and to make system calls on the machine’s operating system. For example, taking input from a field and searching for an entry into a file.
![An attacker could abuse this application by injecting their own commands for the application to execute. Rather than using grep to search for an entry in songtitle.txt, they could ask the application to read data from a more sensitive file.](vulnerable%20php%20code%20snippet.png)

![There is no check for the shell command sent. Thus to execute whoami, we'd need to visit http://flaskapp.thm/whoami](Vulnerable%20python%20code%20snippet.png)

Abusing applications in this way can be possible no matter the programming language the application uses. As long as the application processes and executes it, it can result in command injection.
# Exploiting Command Injection
Command Injection can be detected in mostly one of two ways:
## Blind Command Injection
Blind command injection is when command injection occurs; however, there is no output visible, so it is not immediately noticeable. For example, a command is executed, but the web application outputs no message.

For this type of command injection, we will need to use payloads that will cause some time delay. For example, the `ping` and `sleep` commands are significant payloads to test with. Using `ping` as an example, the application will hang for _x_ seconds in relation to how many _pings_ you have specified.

Another method of detecting blind command injection is by forcing some output. This can be done by using redirection operators such as `>`. For example, we can tell the web application to execute commands such as `whoami` and redirect that to a file. We can then use a command such as `cat` to read this newly created file’s contents.

Testing command injection this way is often complicated and requires quite a bit of experimentation, significantly as the syntax for commands varies between Linux and Windows.

> [!NOTE] 
> The `curl` command is a great way to test for command injection. This is because you are able to use `curl` to deliver data to and from an application in your payload. Take this code snippet below as an example, a simple curl payload to an application is possible for command injection.
> 
> `curl http://vulnerable.app/process.php%3Fsearch%3DThe%20Beatles%3B%20whoami`

## Verbose Command Injection
Detecting command injection this way is arguably the easiest method of the two. Verbose command injection is when the application gives you feedback or output as to what is happening or being executed.
For example, the output of commands such as `ping` or `whoami` is directly displayed on the web application.
## Payloads for exploitation

| **Linux Payload** | **Description**                                                                                                                                                                                                      |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| whoami            | See what user the application is running under.                                                                                                                                                                      |
| ls                | List the contents of the current directory. You may be able to find files such as configuration files, environment files (tokens and application keys), and many more valuable things.                               |
| ping              | This command will invoke the application to hang. This will be useful in testing an application for blind command injection.                                                                                         |
| sleep             | This is another useful payload in testing an application for blind command injection, where the machine does not have `ping` installed.                                                                              |
| nc                | Netcat can be used to spawn a reverse shell onto the vulnerable application. You can use this foothold to navigate around the target machine for other services, files, or potential means of escalating privileges. |

| **Windows Payload** | **Description**                                                                                                                                                                        |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| whoami              | See what user the application is running under.                                                                                                                                        |
| dir                 | List the contents of the current directory. You may be able to find files such as configuration files, environment files (tokens and application keys), and many more valuable things. |
| ping                | This command will invoke the application to hang. This will be useful in testing an application for blind command injection.                                                           |
| timeout             | This command will also invoke the application to hang. It is also useful for testing an application for blind command injection if the `ping` command is not installed.                |
# Remidiation
- Input sanitization: This is a process of specifying the formats or types of data that a user can submit. For example, an input field that only accepts numerical data or removes any special characters such as `>` ,  `&` and `/`.
- Minimal use of potentially dangerous functions or libraries in a programming language. These functions take input such as a string or user data and will execute whatever is provided on the system. Any application that uses these functions without proper checks will be vulnerable to command injection.


> [!NOTE] Bypassing Filters
> Applications will employ numerous techniques in filtering and sanitising data that is taken from a  user's input. These filters will restrict you to specific payloads; however, we can abuse the logic behind an application to bypass these filters.
> For example, an application may strip out quotation marks; we can instead use the hexadecimal value of this to achieve the same result.
> When executed, although the data given will be in a different format than what is expected, it can still be interpreted and will have the same result.

