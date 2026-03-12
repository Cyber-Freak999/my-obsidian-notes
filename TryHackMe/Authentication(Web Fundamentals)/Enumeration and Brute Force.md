---
link: https://tryhackme.com/room/enumerationbruteforce
prerequisites:
  - "[[Burpsuite]]"
tags:
  - recon
  - web-app
---
# Authentication Enumeration
## Identifying Valid Usernames
Knowing a valid username lets an attacker focus just on the password. You can figure out usernames in different ways, like observing how the application responds during login or password resets. For example, error messages that specify "this account doesn't exist" or "incorrect password" can hint at valid usernames, making an attacker's job easier.
## Password Policies
The guidelines when creating passwords can provide valuable insights into the complexity of the passwords used in an application. By understanding these policies, an attacker can gauge the potential complexity of the passwords and tailor their strategy accordingly. For example, the below PHP code uses regex to require a password that includes symbols, numbers, and uppercase letters:

```php
<?php
$password = $_POST['pass']; // Example1
$pattern = '/^(?=.*[A-Z])(?=.*\d)(?=.*[\W_]).+$/';

if (preg_match($pattern, $password)) {
    echo "Password is valid.";
} else {
    echo "Password is invalid. It must contain at least one uppercase letter, one number, and one symbol.";
}
?>
```

In the above example, if the supplied password doesn't satisfy the policy defined in the **pattern** variable, the application will return an error message revealing the regex code requirement. An attacker might generate a dictionary that satisfies this policy.
## Common Places to Enumerate
Web applications are full of features that make things easier for users but can also expose them to risks:
### Registration Pages
Web applications typically make the user registration process straightforward and informative by immediately indicating whether an email or username is available. While this feedback is designed to enhance user experience, it can inadvertently serve a dual purpose. If a registration attempt results in a message stating that a username or email is already taken, the application is unwittingly confirming its existence to anyone trying to register. Attackers exploit this feature by testing potential usernames or emails, thus compiling a list of active users without needing direct access to the underlying database.
### Password Reset Features
Password reset mechanisms are designed to help users regain access to their accounts by entering their details to receive reset instructions. However, the differences in the application's response can unintentionally reveal sensitive information. For example, variations in an application's feedback about whether a username exists can help attackers verify user identities. By analyzing these responses, attackers can refine their lists of valid usernames, substantially improving the effectiveness of subsequent attacks.
### Verbose Errors
Verbose error messages during login attempts or other interactive processes can reveal too much. When these messages differentiate between "username not found" and "incorrect password," they're intended to help users understand their login issues. However, they also provide attackers with definitive clues about valid usernames, which can be exploited for more targeted attacks.
### Data Breach Information
Data from previous security breaches is a goldmine for attackers as it allows them to test whether compromised usernames and passwords are reused across different platforms. If an attacker finds a match, it suggests not only that the username is reused but also potential password recycling, especially if the platform has been breached before. This technique demonstrates how the effects of a single data breach can ripple through multiple platforms, exploiting the connections between various online identities.
# Enumeration from Verbose Errors
Verbose errors can turn into a goldmine of information, providing insights such as:
- Internal Paths: Like a map leading to hidden treasure, these reveal the file paths and directory structures of the application server which might contain configuration files or secret keys that aren't visible to a normal user.
- Database Details: Offering a sneak peek into the database, these errors might spill secrets like table names and column details.
- User Information: Sometimes, these errors can even hint at usernames or other personal data, providing clues that are crucial for further investigation.

Attackers induce verbose errors as a way to force the application to reveal its secrets. Below are some common techniques used to provoke these errors:
-  Invalid Login Attempts: This is like knocking on every door to see which one will open. By intentionally entering incorrect usernames or passwords, attackers can trigger error messages that help distinguish between valid and invalid usernames. For example, entering a username that doesn’t exist might trigger a different error message than entering one that does, revealing which usernames are active.
- SQL Injection: This technique involves slipping malicious SQL commands into entry fields, hoping the system will stumble and reveal information about its database structure. For example, placing a single quote ( ') in a login field might cause the database to throw an error, inadvertently exposing details about its schema.
-  File Inclusion/Path Traversal: By manipulating file paths, attackers can attempt to access restricted files, coaxing the system into errors that reveal internal paths. For example, using directory traversal sequences like ../../ could lead to errors that disclose restricted file paths.
- Form Manipulation: Tweaking form fields or parameters can trick the application into displaying errors that disclose backend logic or sensitive user information. For example, altering hidden form fields to trigger validation errors might reveal insights into the expected data format or structure.
- Application Fuzzing: Sending unexpected inputs to various parts of the application to see how it reacts can help identify weak points. For example, tools like Burp Suite Intruder are used to automate the process, bombarding the application with varied payloads to see which ones provoke informative errors.
## The Role of Enumeration and Brute Forcing
When it comes to breaching authentication, enumeration and brute forcing often go hand in hand:
- User Enumeration: Discovering valid usernames sets the stage, reducing the guesswork in subsequent brute-force attacks.
- Exploiting Verbose Errors: The insights gained from these errors can illuminate aspects like password policies and account lockout mechanisms, paving the way for more effective brute-force strategies.
In summary, verbose errors are like breadcrumbs leading attackers deeper into the system, providing them with the insights needed to tailor their strategies and potentially compromise security in ways that could go undetected until it’s too late.
# Password Reset Flow Vulnerabilities
Password reset mechanism is an important part of user convenience in modern web applications. However, their implementation requires careful security considerations because poorly secured password reset processes can be easily exploited.
## Email-Based Reset
When a user resets their password, the application sends an email containing a reset link or a token to the user’s registered email address. The user then clicks on this link, which directs them to a page where they can enter a new password and confirm it, or a system will automatically generate a new password for the user. This method relies heavily on the security of the user's email account and the secrecy of the link or token sent.
## Security Question-Based Reset
This involves the user answering a series of pre-configured security questions they had set up when creating their account. If the answers are correct, the system allows the user to proceed with resetting their password. While this method adds a layer of security by requiring information only the user should know, it can be compromised if an attacker gains access to personally identifiable information (PII), which can sometimes be easily found or guessed.
## SMS-Based Reset
This functions similarly to email-based reset but uses SMS to deliver a reset code or link directly to the user’s mobile phone. Once the user receives the code, they can enter it on the provided webpage to access the password reset functionality. This method assumes that access to the user's phone is secure, but it can be vulnerable to SIM swapping attacks or intercepts.
Each of these methods has its vulnerabilities:
- **Predictable Tokens**: If the reset tokens used in links or SMS messages are predictable or follow a sequential pattern, attackers might guess or brute-force their way to generate valid reset URLs.
- **Token Expiration Issues**: Tokens that remain valid for too long or do not expire immediately after use provide a window of opportunity for attackers. It’s crucial that tokens expire swiftly to limit this window.
- **Insufficient Validation**: The mechanisms for verifying a user’s identity, like security questions or email-based authentication, might be weak and susceptible to exploitation if the questions are too common or the email account is compromised.
- **Information Disclosure**: Any error message that specifies whether an email address or username is registered can inadvertently help attackers in their enumeration efforts, confirming the existence of accounts.
- **Insecure Transport**: The transmission of reset links or tokens over non-HTTPS connections can expose these critical elements to interception by network eavesdroppers.
# Password Reset Flow Vulnerabilities
Password reset mechanism is an important part of user convenience in modern web applications. However, their implementation requires careful security considerations because poorly secured password reset processes can be easily exploited.
## Email-Based Reset
When a user resets their password, the application sends an email containing a reset link or a token to the user’s registered email address. The user then clicks on this link, which directs them to a page where they can enter a new password and confirm it, or a system will automatically generate a new password for the user. This method relies heavily on the security of the user's email account and the secrecy of the link or token sent.
## Security Question-Based Reset
This involves the user answering a series of pre-configured security questions they had set up when creating their account. If the answers are correct, the system allows the user to proceed with resetting their password. While this method adds a layer of security by requiring information only the user should know, it can be compromised if an attacker gains access to personally identifiable information (PII), which can sometimes be easily found or guessed.
## SMS-Based Reset
This functions similarly to email-based reset but uses SMS to deliver a reset code or link directly to the user’s mobile phone. Once the user receives the code, they can enter it on the provided webpage to access the password reset functionality. This method assumes that access to the user's phone is secure, but it can be vulnerable to SIM swapping attacks or intercepts.
Each of these methods has its vulnerabilities:
- **Predictable Tokens**: If the reset tokens used in links or SMS messages are predictable or follow a sequential pattern, attackers might guess or brute-force their way to generate valid reset URLs.
- **Token Expiration Issues**: Tokens that remain valid for too long or do not expire immediately after use provide a window of opportunity for attackers. It’s crucial that tokens expire swiftly to limit this window.
- **Insufficient Validation**: The mechanisms for verifying a user’s identity, like security questions or email-based authentication, might be weak and susceptible to exploitation if the questions are too common or the email account is compromised.
- **Information Disclosure**: Any error message that specifies whether an email address or username is registered can inadvertently help attackers in their enumeration efforts, confirming the existence of accounts.
- **Insecure Transport**: The transmission of reset links or tokens over non-HTTPS connections can expose these critical elements to interception by network eavesdroppers.
# OSINT
## Wayback URLs
Think of the Internet Archive's Wayback Machine ([https://archive.org/web/](https://archive.org/web/)) as a time machine. It lets you travel back and explore older versions of websites, uncovering files and directories that are no longer visible but might still linger on the server. These relics can sometimes provide a backdoor right into the present system.

To dump all of the links that are saved in Wayback Machine, we can use the tool called waybackurls. Hosted in [GitHub](https://github.com/tomnomnom/waybackurls), we can easily install this on our machine.
## Google Dorks
This is where your savvy with search engines shines. By crafting specific search queries, known as Google Dorks, you can find information that wasn’t meant to be public. These queries can pull up everything from exposed administrative directories to logs containing passwords and indices of sensitive directories. For example:

- To find administrative panels: `site:example.com inurl:admin`
- To unearth log files with passwords: `filetype:log "password" site:example.com`
- To discover backup directories: `intitle:"index of" "backup" site:example.com`