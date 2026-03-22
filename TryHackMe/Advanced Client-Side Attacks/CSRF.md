---
link: https://tryhackme.com/room/csrfV2
tags:
  - vulnerability
  - web-app
  - auth
---
# What is CSRF?
CSRF is a type of security vulnerability where an attacker tricks a user's web browser into performing an unwanted action on a trusted site where the user is authenticated. This is achieved by exploiting the fact that the browser includes any relevant cookies (credentials) automatically, allowing the attacker to forge and submit unauthorised requests on behalf of the user (through the browser). The attacker's website may contain HTML forms or JavaScript code that is intended to send queries to the targeted web application.
## Cycle of CSRF
A CSRF attack has **three** essential phases:
- The attacker already knows the format of the web application's requests to carry out a particular task and sends a malicious link to the user.
- The victim's identity on the website is verified, typically by cookies transmitted automatically with each domain request and clicks on the link shared by the attacker. This interaction could be a click, mouse over, or any other action.
- Insufficient security measures prevent the web application from distinguishing between authentic user requests and those that have been falsified.
## Effects of CSRF
Understanding CSRF's impact is crucial for keeping online activities secure. Although CSRF attacks don't directly expose user data, they can still cause harm by changing passwords and email addresses or making financial transactions. The risks associated with CSRF include:

- **Unauthorised Access**: Attackers can access and control a user's actions, putting them at risk of losing money, damaging their reputation, and facing legal consequences.
- **Exploiting Trust**: CSRF exploits the trust websites put in their users, undermining the sense of security in online browsing.
- **Stealthy Exploitation**: CSRF works quietly, using standard browser behaviour without needing advanced malware. Users might be unaware of the attack, making them susceptible to repeated exploitation.
# Types of CSRF
## Traditional CSRF
Conventional CSRF attacks frequently concentrate on state-changing actions carried out by submitting forms. The victim is tricked into submitting a form without realising the associated data like cookies, URL parameters, etc. The victim's web browser sends an HTTP request to a web application form where the victim has already been authenticated. These forms are made to transfer money, modify account information, or alter an email address.
- The victim is already logged on to his bank website. The attackers create a crafted malicious link and email it to the victim.
- The victim opens the email in the same browser.
- Once clicked, the malicious link enables the auto-transfer of the amount from the victim's browser to the attacker's bank account.
## XMLHttpRequest CSRF
An asynchronous CSRF exploitation occurs when operations are initiated without a complete page request-response cycle. This is typical of contemporary online apps that leverage asynchronous server communication (via **XMLHttpRequest** or the **Fetch** API) and JavaScript to produce more dynamic user interfaces. These attacks use asynchronous calls instead of the more conventional form submissions. Still, they exploit the same trust relationship between the user and the online service.  

Consider an online email client, for instance, where users may change their email preferences without reloading the page. If this online application is CSRF-vulnerable, a hacker might create a fake asynchronous HTTP request, usually a POST request, and alter the victim's email preferences, forwarding all their correspondence to a malicious address.