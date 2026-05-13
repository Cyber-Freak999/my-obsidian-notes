---
title: Threat Model – Indirect Input Attacks (Transitive & Hidden Injection)
tags: [ai, ai-security, threat-modeling, indirect-attacks, prompt-injection, agents, llm-security, advanced]
created: <% tp.date.now("YYYY-MM-DD") %>
source: <video transcript>
---
# Summary
Indirect input attacks occur when malicious instructions are not provided directly to the AI system, but instead are embedded in external content that the system retrieves or interacts with. These attacks are particularly dangerous in agent-based systems where models autonomously fetch and process untrusted data.

---
# What Are Indirect Attacks?
Unlike direct input attacks, where a user explicitly sends malicious input, indirect attacks rely on *transitive data*.

This means:
- The AI model retrieves or processes external content
- That content contains hidden or embedded instructions
- The model interprets and executes those instructions unintentionally

This becomes especially relevant for:
- AI agents browsing the web
- Systems summarizing external content
- Tools processing emails, documents, or APIs

> [!important]
> The attack surface expands from “what users send” to “everything the model can access.”

## Example: Hidden Prompt Injection via Web Content
Consider a chatbot embedded in a webpage that summarizes content.

The attacker:
- Injects hidden instructions into the webpage
- Uses techniques like white text on a white background
- Ensures humans cannot see the malicious content

When the AI:
- Reads or summarizes the page
- It processes both visible and hidden content

This can lead to:
- Unexpected behavior (e.g., changing tone or style)
- Data exfiltration attempts (e.g., asking for user information)

Notably:
- The user did not request this behavior
- The developer did not intend this behavior

The AI becomes an *unwitting execution layer* for hidden instructions.

## ASCII Smuggling
ASCII smuggling is a more advanced form of hidden injection.

Instead of hiding text visually, attackers:
- Encode instructions using Unicode characters
- Use characters that have no visible representation
- Embed them into otherwise normal content

These characters:
- Do not appear in standard UI rendering
- Take up no visible space
- Can still be interpreted by systems processing raw text

This creates a scenario where:
- Humans see clean content
- AI systems process hidden instructions

> [!warning]
> Invisible inputs create a gap between human review and machine interpretation.

## Agent-Specific Risk Amplification
Indirect attacks become significantly more dangerous with AI agents.

Agents:
- Fetch external data autonomously
- Act on that data (e.g., execute tasks, call APIs)
- Operate without constant human oversight

This introduces two key risks:

First, **unvetted data ingestion**:
- Agents may consume data never reviewed by developers
- Trust boundaries become unclear

Second, **actionable compromise**:
- The agent does not just interpret data
- It may *act* on malicious instructions

For example:
- Reading an email with hidden instructions
- Executing unintended actions based on those instructions

> [!important]
> Indirect attacks turn data sources into execution channels.

## Core Insight: Data as an Attack Vector
Traditional systems treat external data as untrusted but passive.

In AI systems:
- Data can contain instructions
- Models interpret and act on those instructions
- The boundary between data and control is blurred

This fundamentally changes the threat model:
- Any external source becomes a potential attacker
- Trust must be re-evaluated at every ingestion point

## Mitigations

### Input Sanitization (Including Transitive Inputs)
Sanitization must extend beyond direct user input.

This includes:
- External web content
- Retrieved documents
- Emails and APIs
- Any data accessed by agents

Approaches include:
- Stripping hidden or non-standard characters
- Detecting obfuscated or encoded instructions
- Filtering suspicious patterns

> [!note]
> This is a direct evolution of traditional injection attack defenses.

### Treat External Content as Untrusted
All external data sources should be treated as potentially malicious.

This means:
- No implicit trust in third-party content
- Validation before processing
- Isolation of external inputs where possible

For agent systems, this is critical:
- Every fetched resource is an attack opportunity

### Red Teaming and Ethical Hacking
Red teaming involves simulating real-world attacks in a controlled environment.

This helps:
- Identify weaknesses in how systems handle external data
- Test resilience against indirect injection techniques
- Improve detection and response strategies

Related approaches include:
- Ethical hacking
- Bug bounty programs

These expand testing beyond internal assumptions.

### Automated Adversarial Testing (GANs)
AI can be used to test AI systems.

Using adversarial models:
- One model generates malicious inputs
- Another model attempts to defend against them
- Feedback loops improve both attack and defense capabilities

This approach:
- Scales testing efforts
- Discovers novel attack patterns
- Continuously improves robustness

> [!tip]
> Effectiveness depends on clearly defining “good” vs “bad” outcomes.

### Limit Agent Autonomy
Reducing autonomy can reduce risk.

Options include:
- Restricting which sources agents can access
- Requiring approval for sensitive actions
- Adding checkpoints before execution

This introduces trade-offs:
- Less autonomy → more control
- More autonomy → higher risk

## Key Takeaways
Indirect input attacks exploit the expanding capabilities of AI systems, particularly their ability to retrieve and act on external data. By embedding hidden instructions in content that appears benign to humans, attackers can manipulate model behavior without direct interaction. As AI systems become more autonomous, these attacks become more impactful, making input validation, trust boundaries, and continuous testing critical components of AI security.