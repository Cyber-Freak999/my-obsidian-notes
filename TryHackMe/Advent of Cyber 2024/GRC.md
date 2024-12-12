# Introduction to GRC

Governance, Risk, and Compliance (GRC) plays a crucial role in any organisation to ensure that their security practices align with their personal, regulatory, and legal obligations. Although in general good security practices help protect a business from suffering a breach, depending on the sector in which an organisation operates, there may be external security regulations that it needs to adhere to.


Let's take a look at some examples in the financial sector:

- **Reserve Bank Regulations:** In most countries, banks have to adhere to the security regulations set forth by the country's reserve bank. This ensures that each bank adheres to a minimum security level to protect the funds and information of their customers.
- **SWIFT CSP:** Banks use the SWIFT network to communicate with each other and send funds. After a [massive bank breach resulted in a $81 million fraudulent SWIFT transfer](https://www.wired.com/2016/05/insane-81m-bangladesh-bank-heist-heres-know/), SWIFT created the Customer Security Programme (CSP), which sets the standard of security for banks to connect to the SWIFT network.
- **Data Protection:** As banks hold sensitive information about their customers, they have to adhere to the security standards created by their data regulator (usually the reserve bank in most countries).

When you run a large organisation with multiple different teams, how do you stay on top of all these regulations and ensure that good security is applied by all teams? This is where GRC comes in. They play a crucial role in understanding external security standards, translating them into internal standards, and then ensuring that they are applied by all teams to help reduce the organisation's risk to an acceptable level. Let's take a quick look at the three functions of GRC.  

## Governance
Governance is the function that creates the framework that an organisation uses to make decisions regarding information security. Governance is the creation of an organisation's security strategy, policies, standards, and practices in alignment with the organisation's overall goal. Governance also defines the roles and responsibilities that everyone in the organisation has to play to help ensure these security standards are met.  

## Risk 
Risk is the function that helps to identify, assess, quantify, and mitigate risk to the organisation's IT assets. Risk helps the organisation understand potential threats and vulnerabilities and the impact that they could have if a threat actor were to execute or exploit them. By simply turning on a computer, an organisation has some level of risk of a cyber attack. The risk function is important to help reduce the overall risk to an acceptable level and develop contingency plans in the event of a cyber attack where a risk is realised.  

## Compliance
Compliance is the function that ensures that the organisation adheres to all external legal, regulatory, and industry standards. For example, adhering to the [GDPR law](https://gdpr-info.eu/) or aligning the organisation's security to an industry standard such as NIST or ISO 27001.

# Introduction to Risk Assessments

Before McSkidy and Glitch choose an eDiscovery company to handle their forensic data, they need to figure out which one is the safest choice. This is where a risk assessment comes in. It's a process to identify potential problems before they happen. Think of it as checking the weather before going on a hike; if there’s a storm coming, you'd want to know ahead of time so you can either prepare or change your plans.

## Why Are Risk Assessments Done?

Risk assessments are like a reality check for businesses. They connect cyber security to the bigger picture, which **minimises business risk**. In other words, it’s not just about securing data but about protecting the business as a whole.

Imagine you run an online store that collects customer information like names, addresses, and credit card details. If that data gets stolen because of a weak security system, it’s not just the data that’s at risk—your reputation, customer trust, and even your profits are on the line. A **risk assessment** could have helped you identify that weak point and fix it before anything went wrong.

For McSkidy and Glitch, assessing the risks of each eDiscovery company helps them decide which one is less likely to have a data breach or other issues that could disrupt the investigation.

## Performing a Risk Assessment

﻿Every business's main goal is to generate revenues and profits. For most businesses, cyber security does not directly contribute to revenue generation or profit maximisation. Businesses decide to spend part of their hard-earned revenue on cyber security to avoid the risk of revenue or reputation loss resulting from a cyber threat. Businesses often take these steps to achieve this goal. We will now work through the process of completing a risk register. A risk register tracks the progress of risk mitigation and all open risks. An example of such a risk register is shown in the animation below. Let's take a look at the steps required to add risks to the risk register.
### Identification of Risks

To assess risk, we must first identify the factors that can cause revenue or reputation loss resulting from cyber threats. This exercise requires carefully assessing the attack surface of the organisation and identifying areas which might be used to harm the organisation. Examples of identified risks can be:

- An unpatched web server.
- A high-privileged user account without proper security controls.
- A third-party vendor who might be infected by a malware connecting to the organisation's network.
- A system for which support has ended by the vendor and it is still in production.

An organisation might identify several other risks in addition to these examples. However, in addition to just identifying risks, these risks also need to be quantified. After all, the likelihood of materialising a risk on a cordoned-off and isolated server differs greatly from that of a public-facing server hosting a web frontend. Similarly, the impact of a risk materializing on a crown jewel, such as a main database server containing confidential information, differs greatly from that of a development server with dummy data. 

﻿### Assigning Likelihood to Each Risk

﻿To quantify risk, we need to identify how likely or probable it is that the risk will materialise. We can then assign a number to quantify this likelihood. This number is often on a scale of 1 to 5. The exact scale differs from organisation to organisation and from framework to framework. Likelihood can also be called the probability of materialisation of a risk. An example scale for likelihood can be:

1. **Improbable:** So unlikely that it might never happen.
2. **Remote:** Very unlikely to happen, but still, there is a possibility.
3. **Occasional:** Likely to happen once/sometime.
4. **Probable:** Likely to happen several times.
5. **Frequent:** Likely to happen often and regularly.

It might be noticed that while we are trying to quantify the risk, we still don't define exact quantities of what constitutes several times and what constitutes regularly, etc. The reason is that the likelihood for a server which has very high uptime requirements will be different from a server that is used infrequently. Therefore, the likelihood scale will differ from case to case and from asset to asset. On the flip side, we can see that this scale provides us with a very usable scale of differentiating between different probabilities of occurrence of a certain event.

### Assigning Impact to Each Risk

Once we have identified the risks and the likelihood of a risk, the next step is to quantify the impact this risk's materialisation might have on the organisation. For example, if there is a public-facing web server that is unpatched and gets breached, what will be the impact on the organisation?![Assigning a impact rating to risks](https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/6093e17fa004d20049b6933e-1732025443659.png) Different organisations calculate impact in different ways. Some organisations might use the CVSS scoring to calculate the impact of a risk; others might use their own rating derived from the Confidentiality, Integrity, and Availability of a certain asset, and others might base it on the severity categorisation of the incidents. Similar to likelihood, we also quantify impact, often on a scale of 1 to 5. An example scale of impact can be based on the following definitions.

1. **Informational:** Very low impact, almost non-existent.
2. **Low:** Impacting a limited part of one area of the organisation's operations, with little to no revenue loss.
3. **Medium:** Impacting one part of the organisation's operations completely, with major revenue loss.
4. **High:** Impacting several parts of the organisation's operations, causing significant revenue loss
5. **Critical:** Posing an existential threat to the organisation.

### Risk Ownership 
The last step to performing a risk assessment is to decide what to do with the risks that were found. We can start by performing some calculations on the risk itself. The simplest calculation takes the likelihood of the risk and multiplies it with the impact of the risk to get a score. Some risk registers make use of more advanced rating systems such as DREAD. Assigning scores to the risks helps organisations prioritise which risks should be remediated first.

While you may think the simplest answer is to secure the system so there is no risk, in real life, it isn't that simple. Implementing more security costs more money, and it doesn't help if we spend more money on security than what we risk losing if we leave open the risk.

In this last step, we decide who owns the risks that were identified. These team members are then responsible for performing an additional investigation into what the cost would be to close the risk vs what we could lose if the risk is realised. In cases where the cost of security is lower, we can **mitigate** the risk with more security controls. However, were it is higher, we can **accept** the risk. Accepted risks should always be documented and reviewed periodically to ensure that the cost has not changed.

## Internal and Third-Party Risk Assessments

Risk assessments are not just done internally in an organisation, but can also be used to assess the risk that a third party may hold to our organisation. Today, it is very common to make use of third parties to outsource key functions of your business. For example, a small organisation may outsource its financial division to a large auditing firm, or a large organisation may outsource the development of some of its applications to a software engineering firm. However, this changes the risk as a compromise of the third party, where we may not have full control over their security, could still result in a compromise of our data or sensitive assets. As such, we need to consider the risk the third party poses to us.

### Why Do Companies Do Internal Risk Assessments?
Internal risk assessments help companies understand the risks they have within their own walls. It's like taking a good look around your house to check if there are any leaks or broken windows.

For example, if a company finds that its software is outdated, it can prioritise updating it to prevent potential attacks. Internal risk assessments help:

- Identify weak spots in security.
- Direct resources to the most important areas.
- Stay compliant with security rules and regulations.  
    

### Why Do Companies Do Risk Assessments of Third Parties?

Companies don't just assess themselves—they also need to evaluate the risks that come from working with other companies, like vendors, suppliers, or partners. This is called a third-party risk assessment, and it's important because one weak link in the chain can affect everyone.

Let's make it simple: McSkidy and Glitch want to make sure that whichever eDiscovery company they choose won't leak or lose sensitive data. So, they will be reviewing if these companies:

- Have good security measures to keep data safe.
- Follow data protection rules.
- Align with the security standards that McSkidy and Glitch have in place.  
    

By doing a third-party risk assessment, McSkidy and Glitch are reducing potential supply chain risks - making sure the investigation doesn't run into trouble because of a weak security link in the chain. In order to do this, McSkidy has to create a risk assessment that can be sent to the potential third parties. Based on the answers provided by the third parties, McSkidy can then make an informed decision on which third party would be best!