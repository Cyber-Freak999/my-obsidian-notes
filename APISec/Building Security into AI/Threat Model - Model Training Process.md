---
tags:
  - ai
  - ai-security
  - threat-modeling
  - model-security
  - machine-learning
---

# Summary
The training stage represents a high-impact but less frequently targeted attack surface in AI systems. If an attacker successfully compromises the training process, they can directly manipulate the model’s behavior without needing to tamper with data or dependencies. These attacks are often subtle, difficult to detect, and can persist throughout the model’s lifecycle.

---
# Why the Training Process Matters
The training process is where the model learns its behavior. Unlike input-stage attacks that influence what the model sees, or dependency attacks that affect what the model is built on, training attacks directly alter how the model learns.

In practice, this means:
- An attacker can bypass earlier defenses (data validation, dependency checks)
- The compromise becomes embedded in the model itself
- Detection becomes harder because the model may appear to function normally

> [!important]
> A compromised training process can invalidate all assumptions about model correctness and trust.

## Attack Types: Model & Algorithm Poisoning
Attacks on the training process are often referred to as:
- Model poisoning
- Algorithm poisoning

These involve manipulating:
- Training parameters (weights, biases)
- Optimization processes
- Training logic or pipeline components

Rather than changing the data, the attacker changes how the model interprets that data.

# How These Attacks Happen
Most training pipelines run on dedicated infrastructure, often with stronger security controls. Because of this, attacks typically require:

- Compromising training servers
- Gaining access to the training pipeline
- Injecting malicious logic into the training process

This higher barrier makes such attacks less common, but the potential impact is significantly higher.

> [!note]
> Security through difficulty (harder access) reduces likelihood, but not impact.

## Example: Adversarial Weight Manipulation
Research has shown that [it is possible to slightly modify a model’s weights to introduce hidden behaviours.](https://arxiv.org/abs/2008.01761)

In these experiments:
- Model weights were subtly altered
- The model behaved normally under most test conditions
- Under specific inputs, the model produced incorrect or attacker-controlled outputs

This creates a form of backdoor:
- Invisible during standard evaluation
- Triggered only under specific conditions

> [!warning]
> Small changes in weights can produce targeted failures without affecting general performance metrics.

## Analogy: “Reflections on Trusting Trust”
[A classic concept from computer security ](https://www.cs.cmu.edu/~rdriley/487/papers/Thompson_1984_ReflectionsonTrustingTrust.pdf)illustrates this risk.

If a tool in your pipeline (e.g., a compiler) is compromised, then:
- Even clean input produces compromised output
- The compromise propagates invisibly

Applied to AI:
- If the training process is compromised
- Every model produced from it inherits that compromise

> [!important]
> Trust in outputs depends entirely on trust in the process that produced them.

## Expanding Attack Surface with Modern Techniques
Modern AI development introduces additional complexity into training pipelines.

Techniques such as:
- Fine-tuning
- Transfer learning
- Mixture of experts
- Model merging

All involve combining multiple components:
- Base models
- Datasets
- Specialized sub-models

Each additional component increases:
- Dependency count
- Trust boundaries
- Potential attack vectors

This creates a compounding effect where a weakness in any part can affect the final model.

## Risk Profile of Training Attacks
Training-stage attacks are generally:
- Lower likelihood (due to stronger security controls)
- Higher impact (direct control over model behavior)

They are also:
- Subtle and hard to detect
- Persistent across deployments
- Difficult to trace back to origin

> [!warning]
> A successful training attack can silently undermine the entire system.

## Mitigations

### Replay Historical Inputs (Regression Testing for AI)
One effective strategy is to reuse previously seen inputs, including:
- Normal inputs
- Edge cases
- Known attack patterns

Process:
- Store inputs from the current production model
- Replay them against the new model during development
- Compare outputs between old and new models

This helps identify:
- Unexpected behavior changes
- Regressions
- Newly introduced vulnerabilities

> [!tip]
> This is analogous to regression testing in traditional software systems.

### Dark Launch (Silent Deployment)
A dark launch involves deploying a new model into production without allowing it to affect users.

Process:
- Route real production traffic to the new model
- Log its outputs
- Do not use its responses in the application

This allows:
- Real-world validation
- Behavioral monitoring under actual conditions
- Detection of anomalies before full rollout

> [!important]
> This provides visibility into model behavior without introducing risk to users.

### Behavioral Probing
In some cases, models can be tested with targeted prompts or inputs to detect abnormal behavior.

Examples include:
- Asking probing or adversarial questions
- Testing for hidden triggers
- Checking for unsafe or unexpected outputs

While not foolproof, this can surface:
- Backdoor behaviors
- Hidden instructions
- Compromised logic

> [!note]
> Security testing in AI often requires creative and non-traditional approaches.

### Secure Training Infrastructure
- Restrict access to training environments
- Monitor training pipelines for unauthorized changes
- Log all training activities and parameter updates

This reduces the likelihood of direct compromise.

### Dependency Awareness in Training
- Track all components used in training (models, datasets, tools)
- Validate each component independently
- Minimize unnecessary dependencies

This helps control the expanding attack surface introduced by modern techniques.

## Key Takeaways
The training process is a critical but often overlooked attack surface in AI systems. While harder to compromise, successful attacks at this stage have far-reaching consequences because they directly alter model behavior. Subtle manipulations, especially at the weight level, can introduce backdoors that are difficult to detect through standard testing. Strong validation, monitoring, and controlled deployment strategies are essential to mitigating these risks.