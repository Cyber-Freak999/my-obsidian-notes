# What Is Phishing?

Phishing is a form of cyber attack that uses social engineering to trick people into revealing sensitive information or running malware on their devices. Attackers deceive victims by impersonating legitimate sources via emails, text messages, phone calls, or fake websites. Phishing exploits human psychology rather than technical vulnerabilities. Attackers craft believable narratives and apply pressure tactics to manipulate victims into compromising their security. The primary channels for phishing attacks include email, SMS (known as **smishing**), voice calls (**vishing**), and fake websites designed to look legitimate. Through phishing, attackers aim for financial gain, unauthorised access to sensitive data, or the installation of malware on a victim's device.
## Types of Phishing
**Phishing**

Phishing is the scam's broad, "cast a wide net" version. Attackers send the same believable message to many people at once, often using common themes like account alerts or invoices. These messages feel routine rather than personal; any details are generic or slightly off. The aim is quick wins at scale: stolen passwords, card details, or a foothold on a device.

**Spear Phishing**

Spear phishing is a targeted attack tailored to a specific person. The goal is usually to get the target to click a link, open a file, run a task, or submit credentials so the attacker can move deeper into the organisation's network.

**Whaling**

Whaling is spear phishing that targets senior decision-makers and executives, like CEOs and CFOs. Both spear phishing and whaling are targeted and customised attacks; the distinction is who is targeted and what leverage is expected. Spear phishing can hit anyone whose access enables a foothold (IT, finance, HR, project teams). Whaling concentrates on people whose decision-making power can move money, expose regulated data, or override controls.

In penetration testing, phishing is essential in evaluating an organisation's vulnerability to social engineering attacks. By simulating these attacks, pentesters can uncover human weaknesses within an organisation. Assessing the risks associated with successful phishing attacks, like data breaches or malware infections, helps organisations gauge their exposure and prepare defences against real threats.

Ethical hackers design mock emails that closely resemble real threats during phishing penetration tests without causing any harm. They may target specific groups based on their roles within the organisation. Tools track response metrics such as open and click-through rates, providing valuable insights into employee behaviour. Incorporating phishing into penetration testing reveals an organisation’s susceptibility to social engineering and strengthens its cyber security posture over time.
# Psychology of Phishing
Phishing campaigns use social engineering techniques to manipulate emotions and influence decision-making. These tactics often exploit vulnerabilities in human psychology to increase the likelihood of success.
## Social Engineering Principles
### Scarcity

Scarcity makes something feel rare, which pushes people to act before they think. Psychologically, **FOMO (fear of missing out)** and loss aversion kick in: we dislike losing a chance more than we like gaining a benefit. We can use terms like “limited seats,” “last chance,” or “ends today.”

Example: “Only three TryPhones up for grabs.”
### Urgency

Urgency adds a countdown so the brain prioritises speed over scrutiny. Time pressure narrows attention and reduces deliberate checking, especially when the consequence sounds inconvenient (lockouts, delays). Language often includes “within 24 hours,” “immediately,” or “deadline passed.”

Example: “Your account will be suspended in 12 hours unless you verify your identity through this portal.”
### Authority

Authority leans on perceived status or expertise to gain quick compliance. People are more likely to follow instructions if they think they come from leaders, experts, or official departments. Visual cues (titles, signatures, formal tone) and role labels (HR, IT, Finance) increase the effect.

Example: “From: IT Administrator. Action required on your SSO settings.”

### Fear

Fear uses threat and alarm to trigger a protective reaction, pushing people to “fix” the problem immediately. Anxiety can override usual scepticism, especially when the risk sounds personal (account compromise, legal trouble). Wording often includes “security alert,” “breach,” or “unauthorised access.”

Example: “We detected suspicious logins on your account. Secure it immediately here.”
### Curiosity

Curiosity hooks attention by promising interesting information. The brain wants to close information gaps, which can outweigh caution when the tease feels relevant or exclusive. Subject lines are short, intriguing, and slightly vague.

Example: “Confidential: Q3 roadmap highlights.”
### Trust

Trust piggybacks on familiar brands, colleagues, or communication styles so the message feels safe by default. Recognisable names, logos, or routines (monthly reports, ticket numbers) lower scepticism and make requests seem routine.

Example: “Microsoft 365: New security notice available in your portal,” or a message that looks like it’s from a known teammate asking for a quick review.
## Cognitive Biases

Cognitive bias is the tendency to make decisions based on feelings, assumptions, or past experiences instead of facts. These biases increase the risk of falling for phishing scams.

- **Overconfidence bias:** Many people, especially cyber security practitioners, think they're too smart to fall for phishing scams. However, this overconfidence can lead to less vigilance when checking suspicious messages.    
- **Confirmation bias:** This happens when people accept information that fits their expectations. For instance, if someone is waiting for an email from their bank, they might trust a phishing email that pretends to be from the bank without verifying it.
- **Authority bias:** This leads people to trust messages from those they see as authority figures without question. An email that comes from a high-ranking official is more likely to be trusted than one from an unknown source.

Understanding these psychological principles is essential for pentesters simulating phishing campaigns. By including tactics like urgency and authority in phishing emails or fake landing pages, pentesters can test how well organisations defend against these social engineering attacks.
# Phishing Techniques
 Phishing campaigns use technical manipulation to deceive targets and bypass defences. Here are some of the most common techniques attackers use to trick victims into interacting with malicious content.
## URL and Domain Manipulation

As a pentester, one of our primary goals is to get our targets to click on a URL we control. To achieve this, we can use some of the techniques below:

- **URL Masking:** Involves disguising a malicious URL behind a legitimate-looking hyperlink. For example, an attacker might display `https://tryhackme.com` while redirecting users to `http://phisher.thm`. 
- **Homograph Attacks:** Exploit visual similarities between domain name characters, for example, replacing **"o"** with **"0"** or using Cyrillic characters. An attacker might register a domain like `go0gle.com` that looks identical to the legitimate one but redirects users to a malicious site.
- **Typosquatting:** Involves registering domains similar to legitimate ones, relying on users making typing errors, for example, `tryhacme.com` instead of `tryhackme.com.` As a pentester, you can use these domains for phishing websites or malware delivery.

Attackers can use URL shorteners to hide a link's true destination. These URLs are more complicated for users to inspect and can bypass basic security checks.
## Email Spoofing Fundamentals

Email spoofing is a technique for impersonating a legitimate sender by modifying email headers. For example, we can spoof the "From" field to display a trusted sender's email address, like a manager or someone from HR. If a domain is lacking security measures for authentication, an attacker can use a Python script to modify their email address. This is possible because **SMTP (Simple Mail Transfer Protocol)** does not have built-in functionality for authenticating email addresses.

Display name spoofing involves changing the sender's name in an email client while keeping the actual email address hidden. For instance, we could display "IT Support" as our sender's name while using a Gmail address. Many mobile email clients only show the display name by default, hiding the actual email address, which makes this technique very effective.

Other techniques involve using domains similar to legitimate ones, for example, `support@tryhackme-secure.com` instead of `support@tryhackme.com`, to trick recipient's into trusting the email.

Using some of these techniques, we can craft an email that would look like this on the recipients end:

```html
From: Support <support@tryaccounting.thm> 
To: bob@tryaccounting.thm
Subject: Urgent: Account Verification Required

Dear Bob,

As part of our security policy, we require all TryAccounting employees to change their passwords every 3 months. Please log in to our internal portal and update your password before Friday:
http://tryaccounting-security.thm/account

Thank you,
TryAccounting Support Team
```

At first glance, this looks like a perfectly legitimate email. Most email clients don't show these details by default, but if we were to look at the email headers, we would see the sender's true email:

```html
From: Support <support@tryaccounting.thm>
Reply-To: attacker@phisher.thm
Return-Path: attacker@phisher.thm
X-Sender: attacker@phisher.thm
Received: from phisher.thm (mail.phisher.thm [192.168.1.25]) by mail.tryaccounting.thm
```

Many organisations use security measures, such as **SPF** (Sender Policy Framework), **DMARC** (Domain-based Message Authentication, Reporting, and Conformance), and **DKIM** (DomainKeys Identified Mail ), to help prevent such attacks. Although bypassing these security measures is outside the scope of this room, understanding the basics is crucial for building a strong foundation.
## Credential Harvesting

In a login cloning attack, the attacker replicates all visual elements of the legitimate website, including logos, fonts, and form fields, and hosts them on a deceptive domain. The primary distinction lies in the destination of submitted credentials. On the authentic site, credentials are transmitted to the organisation's authentication server. On the cloned page, credentials are sent to a script under the attacker's control, which logs them to a file or database. Subsequently, the victim is redirected to the legitimate site, minimising suspicion. As a result, the victim perceives only a failed login attempt, while the attacker acquires the victim's password.
## Payload Delivery Mechanisms

A frequently used delivery method involves a Microsoft Word document containing a macro. Upon opening the file, the victim encounters a prompt to "Enable Content" in order to view the document, which serves as a built-in social engineering tactic. Once enabled, the VBA macro executes silently in the background. In an actual attack, this macro may download and execute malware. During a penetration test, however, it is typically replaced with a benign beacon that merely checks in to confirm execution without causing harm.

The typical sequence of events is as follows:

1. The victim receives and opens the .docm attachment.
2. Microsoft Word prompts the user to enable macros.
3. The victim clicks "Enable Content."
4. The VBA macro executes a hidden command.
5. The attacker receives confirmation of execution.
## Tools of the Trade

Pentesters use specific tools to create and manage realistic phishing campaigns. Below are three of the most popular tools:

[GoPhish](https://github.com/gophish/gophish) is a web-based framework that makes setting up phishing campaigns more straightforward. It allows you to store your SMTP server settings for sending emails and has a web-based tool for creating email templates using a simple WYSIWYG (What You See Is What You Get) editor. You can also schedule emails and have an analytics dashboard that shows open and click rates.

[EvilNginx(opens in new tab)](https://github.com/kgretzky/evilginx2) is a tool designed for advanced phishing campaigns that bypass multi-factor authentication (MFA). It acts as a reverse proxy between victims and legitimate sites, capturing credentials and session tokens in real time.

[The Social Engineering Toolkit (SET)(opens in new tab)](https://github.com/trustedsec/social-engineer-toolkit) contains many tools. Still, some of the important ones for phishing are the ability to create spear-phishing attacks and deploy fake versions of common websites to trick victims into entering their credentials. In task 6, we will get hands-on experience with this tool.
# Anatomy of a Phishing Campaign
## Planning & Scoping

Start by agreeing on the mission with the client and writing it down in one sentence. Define which user groups are in or out, the techniques in bounds, and the specific outcomes to measure, for example, separating “clicked a link” from “attempted to submit credentials.” Set the campaign timing and message volume, secure legal sign-off, and record the rules of engagement, an explicit kill switch, and emergency contacts so the exercise remains authorised, safe, and reversible.
## Reconnaissance

Use only public information to make lures feel plausible without crossing privacy lines. Company websites, press releases, LinkedIn profiles, public social posts, and relevant news provide enough context to craft believable pretexts, such as referencing a recent announcement or policy change. Keep all collections within scope and document sources so it’s clear the research stayed ethical and limited to OSINT.
## Scenario & Payload Development

Turn the intel into realistic but harmless messages: an invoice reminder, an IT notification, or an HR update that looks and reads like the real thing. Payloads should support learning, not exploitation: tracking links, branded landing pages that capture metadata, and benign attachments are appropriate. Avoid malware and live credential capture entirely; use simulated login pages and fake accounts to measure risk-free behaviour.
## Exploitation and Post-Exploitation

Run the campaign according to the agreed plan, either in staggered waves or as a single send, and monitor opens, clicks, simulated submissions, and reports in real time. Keep the kill switch and escalation path visible to the team and pause immediately if messages leak outside the scope or trigger unintended consequences. Use lab-safe tooling, such as **GoPhish** or an equivalent sandboxed platform, and only target real users after obtaining prior written authorisation.
## Reporting and Debriefing

Analyse what happened and why: click rates, submission attempts, reporting behaviour, and timing across teams. Present findings without naming individuals and focus on practical improvements like targeted training, phishing-resistant MFA, SPF/DKIM/DMARC configuration, and other technical controls that reduce risk, close with agreed follow-up actions and a sensible cadence for re-testing so progress can be measured over time. The table below provides an overview of the most common metrics used during phishing campaigns, along with some benchmarks and client recommendations.
## Recommendations table

A phishing simulation provides value only when its results are communicated clearly to the client. The responsibilities of a penetration tester extend beyond the conclusion of the campaign; it is essential to translate raw metrics into actionable findings. The following table offers a framework for this process: given a metric and its benchmark, appropriate recommendations can be formulated. This approach reflects the structure of a professional phishing report.

|Metric|What it measures|Benchmark|Suggested Recommendation(s)|
|---|---|---|---|
|Open Rate|% of users who opened the email.|Industry varies; typical phishing open rates ~50–65%|Targeted refresher training|
|Click Rate|% of all users who clicked a link.|8–14% acceptable; >14% high risk|Focused security awareness training|
|Credential Entry Rate|% of all users who entered credentials after clicking.|<2% low risk; 2–5% moderate risk; >5% high risk|Phishing site identification training, MFA implementation|
|Attachment Detonation Rate|% of users who opened/executed an attachment.|No formal benchmark; >5–7% suggests risk|Educate on safe handling of attachments, Sandbox detonation|
|Reporting Rate (24h)|% of users who reported the email within 24h.|>40% strong; 30–40% average; <30% low|Reporting awareness campaign|