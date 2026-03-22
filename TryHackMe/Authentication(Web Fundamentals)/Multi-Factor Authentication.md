---
tags:
  - concept
  - web-app
  - auth
link: https://tryhackme.com/room/multifactorauthentications
prerequisites:
  - "[[Enumeration and Brute Force]]"
---
Basically, MFA is a combination of different checks. It might be something you know (like a password), something you have (like your smartphone), and something you are (like a fingerprint). By using these layers, MFA makes it much tougher for threat actors to access user accounts or applications.
Multi-Factor Authentication (MFA) adds extra protection to user accounts by requiring you to provide two or more verification factors. This makes accessing user accounts significantly more challenging for threat actors.
It is important to note that 2FA (Two-Factor Authentication) is a subset of MFA (Multi-Factor Authentication). MFA refers to any authentication process that requires two or more factors to verify a user's identity.
# Types of Authentication Factors
MFA typically combines two or more different kinds of credentials from the categories: something you know, something you have, something you are, somewhere you are, and something you do.
## Something You Know
This could be a password, a PIN, or any other piece of info you have to remember. It forms the basis of most authentication systems but can be vulnerable if not used simultaneously with other factors.
## Something You Have
This could be your phone with an authentication app, a security token, or even a smart card. Lately, we’re seeing more use of client certificates, which are like digital ID cards for devices.
## Something You Are
This involves biometrics, such as fingerprints, facial recognition, or iris scans. This form of authentication is gaining popularity because it's tough to fake and is now found in many of our gadgets, from phones to laptops. It's important to note that a fingerprint never matches 100%, and a face scan never matches 100%. So this is the one factor that should always be supplemental and never used in pure isolation.
## Somewhere You Are
This involves your origin IP address or geolocation. Some applications, like online banking services, restrict certain activity if they detect that you're making a request from an unknown IP address.
## Something You Do
This kind of authentication is usually used in applications that restrict bot interaction, like registration pages. The application typically analyses the way the user types the credentials or moves their mouse, and this is also the most difficult to implement since the application requires a specific amount of processing power.

2FA specifically requires exactly two of these factors. So, while all 2FA is MFA, not all MFA is 2FA. For example, an authentication system that requires a password, a fingerprint scan, and a smart card would be considered MFA but not 2FA.  
# Kinds of 2FA
2FA can utilize various mechanisms to ensure each authentication factor provides a robust security layer. Some of the most common methods include:
## Time-Based One-Time Passwords (TOTP)
These are temporary passwords that change every 30 seconds or so. Apps like Google Authenticator, Microsoft Authenticator, and Authy use them, making them tough for hackers to intercept or reuse.
## Push Notifications
Applications like Duo or Google Prompt send a login request straight to your phone. You can approve or deny access directly from your device, adding a layer of security that verifies possession of the device registered with the account.

An attack involving push notifications, the MFA fatigue attack, enabled an attacker to compromise the corporate account of an Uber employee. The details of this attack are out of scope for this room, but to learn more about what happened, you may visit Uber's official security newsroom, which can be found [here](https://www.uber.com/newsroom/security-update).
## SMS
Most of the applications currently use this method. The system sends a text message with a one-time code to the user’s registered phone number. The user must enter this code to proceed with the login. While convenient, SMS-based authentication is less secure due to vulnerabilities associated with intercepting text messages.
## Hardware Tokens
Devices like YubiKeys generate a one-time passcode or use NFC for authentication. They’re great because they don’t need a network or battery, so they work even offline.
# Conditional Access
Conditional access is typically used by companies to adjust the authentication requirements based on different contexts. It's like a decision tree that triggers extra security checks depending on certain conditions. For example:
## Location-Based
If a user logs in from their usual location, like their office, they might only need to provide their regular login credentials. But if they're logging in from a new or unfamiliar location, the system could ask for an additional OTP or even biometric verification.
## Time-Based
During regular working hours, users might get in with just their regular login credentials. However, if someone tries to access the system after working hours, they might be prompted for an extra layer of security, like an OTP or a security token.
## Behavioral Analysis
Suppose a user's behavior suddenly changes, like they began accessing data they don't usually view or access at odd hours. In that case, the system can ask for additional authentication to confirm it’s really them.  
## Device-Specific
In some cases, companies don’t allow employees to use their own devices to access corporate resources. In these situations, the system might block the user after the initial login step if they’re on an unapproved device.
# Global Adoption and Regulatory Push
The adoption of MFA is rapidly expanding across various sectors due to its effectiveness in protecting against many common security threats, including phishing, social engineering, and password-based attacks. Governments and industries worldwide are recognizing the importance of MFA and are starting to mandate its use through various regulatory frameworks. For example, finance and healthcare sectors are now implementing stringent MFA requirements to comply with regulations such as GDPR in Europe, HIPAA in the United States, and PCI-DSS for payment systems globally.
# MFA Implementations and Applications
## MFA in Banking
Banks handle incredibly sensitive information and transactions every single day. By using MFA, banks can protect users' personal and financial information from cyber theft, fraud, and other online threats.

Typically, banks ask you to enter a password (something you know) before moving on to a second layer of security, which is a code sent via SMS or generated by an app on your phone (something you have). This way, even if someone gets hold of your password, they still need that extra bit of info to access your account or complete a transaction.
## MFA in Healthcare
In healthcare, due to regulations like [HIPAA](https://www.hhs.gov/hipaa/for-professionals/privacy/laws-regulations/index.html) in the US, MFA makes sure that patient records and personal health information are only accessible by authorized persons.

For example, to access sensitive systems like electronic health records (EHRs), healthcare providers might require a doctor to use a security badge (something they have) and a fingerprint scan (something they are). This ensures that only those with the right credentials can view or alter patient data.
## MFA in Corporate IT
With the increasing number of cyber attacks and data breaches, IT departments in the corporate world are under intense pressure to protect sensitive business data and maintain system integrity. MFA helps mitigate the risk of unauthorized access that could lead to data theft, espionage, or sabotage.

In a corporate setting, MFA is typically used when accessing company networks, databases, and cloud services. Employees might first log in with their corporate credentials (something they know) and then verify their identity with a code sent to their company-issued phone (something they have) or through biometric verification (something they are). This way, even if someone tries to attack their system, they’ll hit a roadblock without the second factor.
# Common Vulnerabilities in MFA
## Weak OTP Generation Algorithms
The security of a One-Time Password (OTP) is only as strong as the algorithm used to create it. If the algorithm is weak or too predictable, it can make the attacker's job easier trying to guess the OTP. If an algorithm doesn't use truly random seeds, the OTPs generated might follow a pattern, making them more susceptible to prediction.
## Application Leaking the 2FA Token
If an application handles data poorly or has vulnerabilities like insecure API endpoints, it might accidentally leak the 2FA token in the application's HTTP response.

Due to insecure coding, some applications might also leak the 2FA token in the response. A common scenario is when a user, after login, arrives on the 2FA page, the application will trigger an XHR request to an endpoint that issues the OTP. Sometimes, this XHR request returns the OTP back to the user inside the HTTP response.
## Brute Forcing the OTP
Even though OTPs are designed for one-time use, they aren't immune to brute-force attacks. If an attacker can make unlimited guesses, they might eventually get the correct OTP, especially if the OTP isn't well protected by additional security measures. It's like trying to crack a safe by turning the dial repeatedly until it clicks open, given enough time and no restrictions, it might just work.
### Lack of Rate Limiting
Without proper rate limiting, an application is open to attackers to keep trying different OTPs without difficulty. If an attacker can submit multiple guesses in a short amount of time, it increases the likelihood that the attacker will be able to get the correct OTP.

For example, in this HackerOne [report](https://hackerone.com/reports/121696), the tester was able to report a valid bug since the application doesn't employ rate limiting in the checking of the 2FA code.

# OTP Leakage
The OTP leakage in the XHR (XMLHttpRequest) response typically happens due to poor implementation of the 2FA (Two-Factor Authentication) mechanism or insecure coding. Some common reasons why this happens are because of:
## Server-Side Validation and Return of Sensitive Data
In some poorly designed applications, the server validates the OTP, and rather than just confirming success or failure, it returns the OTP itself in the response. This is often done unintentionally, as part of debugging, logging, or poor response handling practices.
## Lack of Proper Security Practices
Developers might overlook the security implications of exposing sensitive information like OTP in the API responses. This often happens when developers are focused on making the application functional without considering how attackers could exploit these responses.

Not all developers are fully aware of secure coding practices. They might implement features like 2FA without fully understanding the potential risks of exposing sensitive information in the XHR response.
## Debugging Information Left in Production
During the development or testing phase, developers might include detailed debugging information in responses to help diagnose issues. If these debug responses are not removed before deploying to production, sensitive information like OTPs could be exposed.
# Logic Flaw or Insecure Coding?

In some applications, flawed logic or insecure coding practices can lead to a situation where critical parts of the application (i.e., the dashboard) can be accessed without fully completing the authentication process. Specifically, an attacker might be able to bypass the 2FA mechanism entirely and gain access to the dashboard or other sensitive areas without entering the OTP (One-Time Password). This is often due to improper session management, poor access control checks, or incorrectly implemented logic that fails to enforce the 2FA requirement.
# Beating the Auto-Logout Feature
In some applications, failing the 2FA challenge can cause the application to revert the user back to the first part of the authentication process (i.e., the initial login with username and password). This behavior typically occurs due to security mechanisms designed to prevent brute-force attacks on the 2FA part of the application. The application may force the user to reauthenticate to ensure that the person attempting to log in is indeed the legitimate user and not an attacker trying to guess the OTP.

### Common Reasons for This Behavior

**Session Invalidation**

Upon failing the 2FA challenge, the application might invalidate the user's session as a security measure, forcing the user to start the authentication process from scratch.

**Rate-Limiting and Lockout Policies**

To prevent attackers from repeatedly attempting to bypass 2FA, the application may have rate-limiting or lockout mechanisms in place that trigger after a set number of failed attempts, reverting the user to the initial login step.

**Security-Driven Redirection**

Some applications are designed to redirect users back to the login page after multiple failed 2FA attempts as an additional security measure, ensuring that the user's credentials are revalidated before allowing another 2FA attempt.

### Automation Is the key

Automation makes life easier when attacking these kinds of protection because:

**Speed**

Manually logging back in every time you get logged out is slow and tedious. Automation can do it for you much faster.

**Consistency**

Automation avoids mistakes that might happen if you’re doing the same repetitive actions over and over again. It’s reliable.

**Recovering From Logouts**

If the application logs you out after a few failed attempts, the script can automatically log back in and keep trying. This saves you the hassle of doing it manually every time.

**Customization**

Manually creating an automation script for the attack offers more flexibility than using a single tool like ZAP or Burp Suite. You can customize your scripts to test specific scenarios, such as using different IP addresses or user agents or varying the timing between requests.