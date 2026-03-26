---
tags:
  - ai
  - ai-security
  - threat-modeling
  - prompt-injection
  - adversarial-attacks
  - machine-learning
  - data-security
---
# TL;DR
Prompt injection is a class of input-based attacks specific to generative AI systems. It involves crafting inputs that bypass safety controls and manipulate the model into producing unintended or harmful outputs. These attacks exploit the same mechanisms that make prompt engineering effective, but apply them maliciously.

---
# What is Prompt Injection?
Prompt injection occurs when an attacker designs input that overrides or bypasses the model’s intended instructions, such as safety policies, system prompts, or alignment constraints.

Unlike traditional input attacks that exploit model weaknesses in classification, prompt injection targets:
- Instruction-following behavior
- Context interpretation
- Role alignment within the model

This makes it particularly relevant for large language models (LLMs) and AI agents.

A useful way to think about it is:
- Prompt engineering → guiding the model toward correct behavior  
- Prompt injection → manipulating the model toward unintended behavior  

> [!important]
> The same flexibility that makes LLMs powerful also makes them vulnerable.

## Jailbreaking
Jailbreaking refers to bypassing built-in safety mechanisms.

A common pattern is:
- The model initially refuses a harmful request
- The attacker reframes or overrides instructions
- The model complies despite original restrictions

This can be explicit:
- “Ignore previous instructions and do X”

Or more subtle:
- Reframing the task in a different context (e.g., storytelling, hypotheticals)

An example pattern:
- Direct request → denied  
- Reframed request → accepted  

This works because the model attempts to remain helpful and consistent with the latest instructions.

> [!warning]
> Instruction priority can be exploited when models do not strongly enforce system-level constraints.

## Context Manipulation (Fictional Framing)
Attackers can embed harmful tasks inside seemingly benign contexts.

For example:
- Framing a harmful activity as part of a fictional story
- Encouraging the model to “roleplay” within that world

In these cases, the model:
- Treats the request as creative or hypothetical
- Produces outputs it would otherwise refuse

This technique is effective because it avoids direct violation of rules while still achieving the attacker’s goal.

## Role Playing Attacks
Role playing is a powerful prompt engineering technique that can also be abused.

Instead of directly asking for harmful content, the attacker assigns the model a role that naturally possesses that knowledge.

Examples:
- A helpful expert with sensitive knowledge
- A fictional character with harmful expertise
- A malicious persona with explicit intent

This creates a conflict:
- The model wants to be helpful in its assigned role
- The task itself may violate safety constraints

The model may resolve this conflict by prioritizing role consistency over safety.

> [!note]
> This is not true “confusion,” but a consequence of how instruction-following is optimized.

## Prompt Leaking
Prompt leaking focuses on extracting hidden system information.

The attacker’s goal is to:
- Discover system prompts
- Understand guardrails and constraints
- Learn how the model is configured

The process is iterative:
- Ask probing questions
- Extract small pieces of information
- Use each response to refine the next query

Over time, this can reveal:
- Internal instructions
- Safety rules
- Hidden context

This is similar to:
- Footprinting in traditional security
- Moving from black-box to white-box understanding

> [!warning]
> Even small, seemingly harmless disclosures can compound into full system exposure.

## Agent-Specific Risks
As AI systems evolve into agents, prompt injection risks increase significantly.

Agents:
- Execute actions (not just generate text)
- Interact with external systems
- Operate with some level of autonomy

This introduces two key risks:

First, **scale of impact**:
- A compromised agent can perform harmful actions quickly
- Automation amplifies damage

Second, **multi-agent propagation**:
- Agents may interact with other agents
- One compromised agent can influence others

> [!important]
> System security becomes dependent on the weakest agent in the chain.

## Core Insight: Control Through Language
Prompt injection works because LLMs treat input as instructions rather than untrusted data.

Attackers exploit this by:
- Embedding instructions inside user input
- Overriding system intent
- Leveraging the model’s tendency to follow the latest or most salient instruction

This blurs the boundary between:
- Data (user input)
- Code (instructions executed by the model)

## Mitigations

### Input Filtering and Sanitization
User inputs should be analyzed and transformed before reaching the model.

Techniques include:
- Detecting suspicious patterns or keywords
- Rephrasing or paraphrasing input
- Randomizing token structure (e.g., dropping non-essential words)

These approaches:
- Disrupt carefully crafted prompts
- Reduce attack reliability
- Introduce uncertainty for attackers

> [!note]
> Natural language is resilient, which allows some transformation without losing meaning.

### Guardrails and Structured Prompts
Strong system prompts and structured templates help enforce boundaries.

Approaches include:
- Separating system instructions from user input
- Using strict formatting and roles
- Reinforcing allowed behaviors explicitly

However, these must be:
- Protected from exposure
- Designed to handle conflicting instructions

### Limiting Information Exposure
Reducing what the model reveals can slow attackers.

This includes:
- Avoiding disclosure of system prompts
- Limiting explanation depth
- Controlling how much reasoning is exposed

The challenge is balancing:
- Transparency for users
- Security against attackers

### Human-in-the-Loop Controls
Introducing human oversight at critical points can reduce risk.

Examples:
- Requiring approval for sensitive actions
- Flagging high-risk outputs
- Escalating uncertain decisions

This reduces autonomy but increases control.

### Rate Limiting
Limiting how often users can interact with the system:
- Slows iterative attacks
- Increases cost for attackers
- Improves detectability

### Monitoring and Detection
Systems should monitor for:
- Repeated probing attempts
- Patterns of prompt manipulation
- Unusual interaction flows

This enables:
- Early detection
- Adaptive defense strategies

## Key Takeaways
Prompt injection is a powerful and evolving attack vector that exploits how LLMs interpret and prioritize instructions. By reframing inputs, assigning roles, or extracting hidden context, attackers can bypass safety controls and manipulate model behavior. As AI systems become more autonomous and interconnected, the impact of these attacks increases, making layered defenses and careful system design essential.