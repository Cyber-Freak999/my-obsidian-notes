---
tags:
  - ai
  - ai-security
  - threat-modeling
  - model-security
  - machine-learning
  - application-security
  - data-security
---
# TL;DR
Input-based attacks target AI systems at inference time by manipulating inputs to cause incorrect or unintended outputs. Unlike data poisoning or training attacks, these do not require prior compromise of the system. Instead, attackers iteratively probe the model, learn its behaviour, and refine inputs until they achieve the desired misclassification or response.

---
## What Are Input-Based Attacks?
Input-based attacks—also called evasion attacks or adversarial attacks—occur when an attacker directly interacts with a deployed model and crafts inputs that cause it to fail.

These attacks:
- Happen at runtime (inference stage)
- Do not require access to training data or pipeline
- Exploit how the model interprets inputs rather than how it was built

This is often the most intuitive attack surface, as it resembles a user interacting with an application and attempting to manipulate its behavior.

## Triggered vs Independent Attacks
Some input-based attacks rely on prior compromise, such as trigger-based backdoors introduced during training. In those cases, specific patterns activate hidden behaviour.

The focus here is on attacks that do not rely on prior poisoning. These are purely based on manipulating inputs and observing model responses.

## White Box Attacks
White box attacks assume the attacker has some level of knowledge about the system. This knowledge can range from detailed (model architecture, weights, training data) to partial (general understanding of how the system behaves).

The key idea is that the attacker uses this knowledge to guide their attack.

In the road sign example:
- The attacker knows the model is sensitive to colour patterns (e.g., red, white, black)
- They introduce small changes (e.g., adding red paint)
- They observe how the model’s confidence changes

This creates a feedback loop:
- Modify input
- Observe output (or confidence)
- Refine attack

Over time, the attacker identifies the minimal change required to cause misclassification.

Even if exact confidence scores are not exposed, attackers can infer them through:
- Repeated queries
- Observing output consistency
- Detecting changes in classification behaviour

> [!warning]
> Any feedback from the system—confidence scores, explanations, or even response consistency—can help refine attacks.

## Black Box Attacks
Black box attacks assume no prior knowledge of the model’s internals. This is the typical real-world scenario for proprietary systems.

Attackers rely entirely on experimentation:
- Send inputs to the model
- Observe outputs
- Adjust inputs iteratively

Over time, this process can approximate the model’s behaviour and effectively turn a black box into a “gray box.”

Because the attacker starts with little knowledge, early attempts may appear random or nonsensical. However, with enough iterations, patterns emerge.

This process is closely related to:
- Footprinting (gathering system information)
- Fuzzing (generating many inputs to find weaknesses)

Attackers may also automate this using AI systems such as generative models to produce candidate inputs at scale.

## Characteristics of Adversarial Inputs
Adversarial inputs often have the following properties:
- Small, targeted perturbations
- Minimal impact on human perception
- Significant impact on model output

In some cases:
- Inputs look normal to humans but fool the model
- Inputs look abnormal but still trigger confident misclassification

This highlights a fundamental gap between human perception and model interpretation.

## Core Insight: Iteration and Feedback
Whether white box or black box, the core mechanism is the same:
- The attacker interacts with the model
- Learns from its responses
- Improves the attack over time

The more information the system exposes, the faster this process becomes.

> [!important]
> Input-based attacks are less about a single exploit and more about an iterative learning process.

## Mitigations

### Limit Information Leakage
Reducing the amount of information exposed to users can slow down attackers.

This includes:
- Avoiding detailed confidence scores
- Limiting explainability outputs where unnecessary
- Reducing precision (e.g., using categories instead of exact values)

There is a trade-off here:
- More transparency improves user experience
- More information helps attackers refine inputs

### Privacy-Preserving Techniques
Introducing uncertainty into outputs can make attacks less reliable.

Examples include:
- Adding controlled noise to outputs
- Reducing output granularity

The goal is not to eliminate accuracy but to:
- Prevent attackers from making precise adjustments
- Increase uncertainty in their feedback loop

> [!note]
> Small variations may not affect user decisions but can significantly disrupt attack optimization.

### Rate Limiting / API Throttling
Limiting how often a system can be queried reduces the attacker’s ability to iterate.

This increases:
- Cost of attack
- Time required to succeed
- Likelihood of detection

However, this must be balanced against usability to avoid degrading the experience for legitimate users.

### Monitoring and Anomaly Detection
Attackers often leave behavioral patterns, even when they try to stay subtle.

Systems should monitor for:
- Unusual query patterns
- High-frequency interactions
- Repeated similar inputs with slight variations

Detecting these patterns allows:
- Early identification of attacks
- Automated or manual response

> [!tip]
> This is an area where AI can assist in detecting AI-targeted attacks.

## Key Takeaways
Input-based attacks exploit how models interpret inputs rather than how they are built. They rely on iterative interaction and feedback, gradually refining inputs until the model fails. While these attacks are difficult to fully prevent, limiting feedback, controlling interaction rates, and monitoring behavior can significantly increase the cost and difficulty for attackers.