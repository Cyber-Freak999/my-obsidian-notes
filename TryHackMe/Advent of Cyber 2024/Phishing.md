## Phishing Attacks

Security is as strong as the weakest link. Many would argue that humans are the weakest link in the security chain. Is it easier to exploit a patched system behind a firewall or to convince a user to open an “important” document? Hence, “human hacking” is usually the easiest to accomplish and falls under social engineering.

Phishing is a play on the word fishing; however, the attacker is not after seafood. Phishing works by sending a “bait” to a usually large group of target users. Furthermore, the attacker often craft their messages with a sense of urgency, prompting target users to take immediate action without thinking critically, increasing the chances of success. The purpose is to steal personal information or install malware, usually by convincing the target user to fill out a form, open a file, or click a link.

One might get an email out of nowhere claiming that they are being charged a hefty sum and that they should check the details in the attached file or URL. The attacker just needs to have their target users open the malicious file or view the malicious link. This can trigger specific actions that would give the attack control over your system.

## Macros

The needs of MS Office users can be vastly different, and there is no way that a default installation would cater to all of these needs. In particular, some users find themselves repeating the same tasks, such as formatting and inserting text or performing calculations. Consider the example of number-to-words conversion where a number such as “1337” needs to be expressed as “one thousand three hundred thirty-seven”. It would take hours to finish if you have hundreds of numbers to convert. Hence, there is a need for an automated solution to save time and reduce manual effort.

In computing, a macro refers to a set of programmed instructions designed to automate repetitive tasks. MS Word, among other MS Office products, supports adding macros to documents. In many cases, these macros can be a tremendous time-saving feature. However, in cyber security, these automated programs can be hijacked for malicious purposes.

To add a macro to an MS Word document for instance, we click on the **View** menu and then select **Macros** as pointed out by 1 and 2 in the screenshot below. We should specify the name of the macro and specify that we want to save it in our current document, as indicated by 3 and 4. Finally, we press the **Create** button.

![Adding a macro to an MS Word document](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/5f04259cf9bf5b57aed2c476-1729859866900.png)  

Let’s explore one way the attacker could have created an MS Word document with an embedded macro to gain access to Marta’s system.

## Attack Plan

In his plans, Mayor Malware needs to create a document with a malicious macro. Upon opening the document, the macro will execute a payload and connect to the Mayor’s machine, giving him remote control. Consequently, the Mayor needs to ensure that he is listening for incoming connections on his machine before emailing the malicious document to Marta May Ware. By executing the macro, the Mayor gains remote access to Marta’s system through a reverse shell, allowing him to execute commands and control her machine remotely. The steps are as follows:

1. Create a document with a malicious macro
2. Start listening for incoming connections on the attacker’s system
3. Email the document and wait for the target user to open it
4. The target user opens the document and connects to the attacker’s system
5. Control the target user’s system

You might wonder why you don’t set the malicious macro so that you can connect to the target system directly instead of the other way around. The reason is that when the target system is behind a firewall or has a private IP address, you cannot reach it and, hence, cannot connect to it.