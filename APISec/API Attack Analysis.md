# Dominant API Attack Patterns

Analysis of breach data shows that a small number of patterns are responsible for the majority of API compromises.

### Rate Limiting and High-Volume Attacks (~70%)

A significant portion of API breaches involves **high-volume request attacks**, such as:

- Brute-force enumeration  
- Data scraping at scale  
- Mass harvesting of records  

Large-scale breaches involving millions of records strongly indicate that attackers are successfully executing **automated, high-frequency requests**.

It is tempting to conclude that **rate limiting failures** are the main issue. However, this is a flawed interpretation.

Rate limiting is:
- A **defensive control**, not a vulnerability  
- Designed to **slow down attackers**, not eliminate them  

The real issue is that:
> The API is exposing valuable data or functionality that can be exploited at scale.

If nothing valuable were exposed, attackers would not invest resources into high-volume attacks.

## How Attackers Bypass Rate Limiting

Even when rate limiting is implemented, attackers can adapt. Some of these techniques include:

- **Threshold tuning**  
  Attackers identify the rate limit and operate just below it (e.g., 90–95% of allowed traffic)

- **Distributed attacks**  
  Requests are spread across:
  - Thousands of IP addresses  
  - Residential proxy networks  

- **Long-duration attacks**  
  Instead of rapid bursts, attackers:
  - Operate slowly over weeks or months  
  - Avoid detection by blending with normal traffic  

Defensive systems (e.g., WAFs) must make decisions in **milliseconds**, while attackers can iterate and refine strategies over **long timeframes**.

## The Real Root Causes: OWASP API Top 3

While rate limiting appears frequently in breaches, the **true root causes** are aligned with the top three OWASP API risks.

Together, these account for **approximately 90% of API breaches**.

 1. Broken Authorization ([OWASP API1](3.%20OWASP%20API%20Security%20Top%2010.md#API1%20Broken%20Object%20Level%20Authorisation(BOLA))))
 2. Broken Authentication ([OWASP API2](3.%20OWASP%20API%20Security%20Top%2010.md#API2%20Broken%20Authorisation))
 3. Excess Data Exposure ([OWASP API3](3.%20OWASP%20API%20Security%20Top%2010.md#API3%20Broken%20Object%20Property%20Level%20Authorisation))

## Why These Three Issues Dominate

These vulnerabilities exist at the **core of API design and logic**, not just at the infrastructure level.

They are:
- Easy to introduce during development  
- Difficult to detect with traditional testing  
- Highly impactful when exploited  

Addressing them provides **maximum security improvement with focused effort**.

# Rethinking API Security Strategy

## Incorrect Approach

- Over-reliance on perimeter defenses  
- Assuming rate limiting or WAFs will stop attacks  
## Effective Approach

Focus on:
- Strong authorization checks at every endpoint  
- Proper authentication enforcement  
- Minimizing data exposure in responses  

Security must be **built into the API logic itself**, not layered on top as an afterthought.

# Organizational Implications

One of the most important takeaways is that **API security is not just a security team responsibility**.

## Why Developers Must Be Involved

- These vulnerabilities originate in **application logic**  
- Fixes require **code-level changes**  
- Awareness enables developers to identify and remediate issues early  

In many cases, developers can immediately recognize flaws once these patterns are understood.