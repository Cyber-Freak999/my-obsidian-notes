---
link: https://tryhackme.com/room/owaspapisecuritytop105w/
tags:
  - owasp
  - application-security
  - api
---
# Understanding APIs - A refresher
**What is an API & Why is it important?**
API stands for Application Programming Interface. It is a middleware that facilitates the communication of two software components utilising a set of protocols and definitions. In the API context, the term '**application**' refers to any software having specific functionality, and '**interface**' refers to the service contract between two apps that make communication possible via requests and responses. The API documentation contains all the information on how developers have structured those responses and requests. The significance of APIs to app development is in just a single sentence, i.e., **API is a building block for developing complex and enterprise-level applications**.

**Recent Data Breaches through APIs**
- LinkedIn data breach: In June 2021, the data of over 700 million LinkedIn users were offered for sale on one of the dark web forums, which was scraped by exploiting the LinkedIn API. The hacker published a sample of 1 million records to confirm the legitimacy of the LinkedIn breach, containing full names of the users, email addresses, phone numbers, geolocation records, LinkedIn profile links, work experience information, and other social media account details. 
- Twitter data breach: In June 2022, data of more than 5.4 Million [Twitter (opens in new tab)](https://privacy.twitter.com/en/blog/2022/an-issue-affecting-some-anonymous-accounts)users was released for sale on the dark web. Hackers conducted the breach by exploiting a zero-day in the Twitter API that showed Twitter's handle against a mobile number or email.
- PIXLR data breach: In January 2021, PIXLR, an online photo editor app, suffered a data breach that impacted around 1.9 million users. All the data by the hackers was dumped on a dark web forum, which included usernames, email addresses, countries, and hashed passwords. 

# Vulnerability I - Broken Object Level Authorisation (BOLA)

**How does it Happen?**

Generally, API endpoints are utilised for a common practice of retrieving and manipulating data through object identifiers. BOLA refers to Insecure Direct Object Reference (IDOR) - which creates a scenario where the user uses the **input functionality and gets access to the resources they are not authorised to access**. In an API, such controls are usually implemented through programming in Models (Model-View-Controller Architecture) at the code level.

**Likely Impact**

The absence of controls to prevent **unauthorised object access can lead to data leakage** and, in some cases, complete account takeover. User's or subscribers' data in the database plays a critical role in an organisation's brand reputation; if such data is leaked over the internet, that may result in substantial financial loss.

**Mitigation Measures**

- An authorisation mechanism that relies on user policies and hierarchies should be adequately implemented. 
- Strict access controls methods to check if the logged-in user is authorised to perform specific actions. 
- Promote using completely random values (strong encryption and decryption mechanism) for nearly impossible-to-predict tokens.
# Vulnerability II - Broken User Authentication (BUA)

**How does it happen?**

User authentication is the core aspect of developing any application containing sensitive data. Broken User Authentication (BUA) reflects a scenario where an API endpoint allows an attacker to access a database or acquire a higher privilege than the existing one. The primary reason behind BUA is either **invalid implementation of authentication** like using incorrect email/password queries etc., or the absence of security mechanisms like authorisation headers, tokens etc.

Consider a scenario in which an attacker acquires the capability to abuse an authentication API; it will eventually result in data leaks, deletion, modification, or even the complete account takeover by the attacker. Usually, hackers have created special scripts to profile, enumerate users on a system and identify authentication endpoints. A poorly implemented authentication system can lead any user to take on another user's identity. 

**Likely Impact** 

In broken user authentication, attackers can compromise the authenticated session or the authentication mechanism and easily access sensitive data. Malicious actors can pretend to be someone authorised and can conduct an undesired activity, including a complete account takeover. 

**Mitigation Measures** 

- Ensure complex passwords with higher entropy for end users.
- Do not expose sensitive credentials in **GET** or **POST** requests.
- Enable strong JSON Web Tokens (JWT), authorisation headers etc.
- Ensure the implementation of multifactor authentication (where possible), account lockout, or a captcha system to mitigate brute force against particular users. 
- Ensure that passwords are not saved in plain text in the database to avoid further account takeover by the attacker. 

# Vulnerability III - Excessive Data Exposure

**How does it happen?**

Excessive data exposure occurs when applications tend to **disclose more than desired information** to the user through an API response. The application developers tend to expose all object properties (considering the generic implementations) without considering their sensitivity level. They leave the filtration task to the front-end developer before it is displayed to the user. Consequently, an attacker can intercept the response through the API and quickly extract the desired confidential data. The runtime detection tools or the general security scanning tools can give an alert on this kind of vulnerability. However, it cannot differentiate between legitimate data that is supposed to be returned or sensitive data. 

**Likely Impact** 

A malicious actor can successfully sniff the traffic and easily access confidential data, including personal details, such as account numbers, phone numbers, access tokens and much more. Typically, APIs respond with sensitive tokens that can be later on used to make calls to other critical endpoints.

**Mitigation Measures** 

- Never leave sensitive data filtration tasks to the front-end developer. 
- Ensure time-to-time review of the response from the API to guarantee it returns only legitimate data and checks if it poses any security issue. 
- Avoid using generic methods such as `to_string() and to_json()`. 
- Use API endpoint testing through various test cases and verify through automated and manual tests if the API leaks additional data.
# Vulnerability IV - Lack of Resources & Rate Limiting

**How does it happen?**

Lack of resources and rate limiting means that **APIs do not enforce any restriction on** the frequency of clients' requested resources or the files' size, which badly affects the API server performance and leads to the DoS (Denial of Service) or non-availability of service. Consider a scenario where an API limit is not enforced, thus allowing a user (usually an intruder) to upload several GB files simultaneously or make any number of requests per second. Such API endpoints will result in excessive resource utilisation in network, storage, compute etc.

Nowadays, attackers are using such attacks to **ensure the non-availability of service for an organisation**, thus tarnishing the brand reputation through increased downtime. A simple example is non-compliance with the Captcha system on the login form, allowing anyone to make numerous queries to the database through a small script written in Python.

**Likely Impact** 

The attack primarily targets the **Availability** principles of security; however, it can tarnish the brand's reputation and cause financial loss.  

**Mitigation Measures** 

- Ensure using a captcha to avoid requests from automated scripts and bots.
- Ensure implementation of a limit, i.e., how often a client can call an API within a specified time and notify instantly when the limit is exceeded. 
- Ensure to define the maximum data size on all parameters and payloads, i.e., max string length and max number of array elements.

# Vulnerability V - Broken Function Level Authorisation

**How does it happen?**

Broken Function Level Authorisation reflects a scenario where a low privileged user (e.g., sales) bypasses system checks and gets access to **confidential data by impersonating a high privileged user (Admin)**. Consider a scenario of complex access control policies with various hierarchies, roles, and groups and a vague separation between regular and administrative functions leading to severe authorisation flaws. By taking advantage of these issues, the intruders can easily access the unauthorised resources of another user or, most dangerously – the administrative functions.   

Broken Function Level Authorisation reflects IDOR permission, where a user, most probably an intruder, can perform administrative-level tasks. APIs with complex user roles and permissions that can span the hierarchy are more prone to this attack. 

**Likely Impact** 

The attack primarily targets the authorisation and non-repudiation principles of security. Broken Functional Level Authorisation can lead an intruder to impersonate an authorised user and let the malicious actor get administrative rights to perform sensitive tasks. 

**Mitigation Measures** 

- Ensure proper design and testing of all authorisation systems and deny all access by default. 
- Ensure that the operations are only allowed to the users belonging to the authorised group. 
- Make sure to review API endpoints against flaws regarding functional level authorisation and keep in mind the apps and group hierarchy's business logic. 
