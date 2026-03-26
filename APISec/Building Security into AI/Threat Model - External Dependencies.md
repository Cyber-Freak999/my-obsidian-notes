---
tags:
  - ai
  - ai-security
  - threat-modeling
  - supply-chain
  - model-security
  - data-security
---
# Summary
External dependencies introduce significant risk into AI systems because they extend trust beyond the organization’s control. These dependencies include code, datasets, models, and tools. If any of them are compromised, the entire AI system can inherit that compromise. This expands the traditional software supply chain problem into a broader AI supply chain problem.

---
# What Are External Dependencies?
Modern AI systems are rarely built from scratch. Instead, they rely heavily on external resources such as libraries, frameworks, pretrained models, and public datasets.

This follows the same principle as traditional software development: reusing existing components to accelerate development. However, in AI systems, the dependency surface is much broader and includes not just code but also data and models.

Examples include:
- Open-source libraries and frameworks
- Public datasets used for training or validation
- Pretrained or foundational models
- Third-party tools used in agent-based systems

> [!important]
> Every external dependency introduces a trust boundary that can be exploited.

# Supply Chain Attacks (General Concept)
A supply chain attack occurs when an attacker compromises a trusted third-party component that is later used by your system.

In traditional software:
- A malicious actor injects code into a widely used library
- Developers unknowingly import or update that library
- The malicious code executes within their application

This risk directly applies to AI systems, but with additional layers involving data and models.

## Software Supply Chain Attacks
These attacks target code dependencies such as libraries, packages, or CI/CD components.

A typical scenario:
- A widely used library is compromised
- A malicious update is pushed
- Systems that install or update the dependency become compromised

Because these libraries are often trusted and widely used, the impact can be widespread.
A recent example is the compromised [tj-actions/changed-files GitHub Action](https://github.com/advisories/ghsa-mrrh-fwg8-r2c3) that allows attacker to expose CI/CD secrets in workflow logs.

> [!warning]
> Trust in a dependency is often based on reputation, not continuous verification.

## Data Supply Chain Attacks
AI systems frequently rely on publicly available datasets. If these datasets are compromised, the resulting models may inherit poisoned behavior.

This is effectively an indirect form of data poisoning:
- Attacker manipulates a public dataset
- Organization uses the dataset for training
- Model learns incorrect or malicious patterns

This can occur both maliciously and unintentionally through:
- Bias in datasets
- Incorrect labelling
- Missing or skewed data distributions

## Model Supply Chain Attacks
With the rise of foundational models, another layer of risk emerges: the model itself can be the attack vector.

Organizations may:
- Use pretrained models directly
- Fine-tune them on internal data
- Apply transfer learning

If the [base model is compromised](https://www.reversinglabs.com/blog/malicious-attack-method-on-hosted-ml-models-now-targets-pypi), any system built on top of it is also compromised.

This risk extends further:
- A compromised dataset can affect a foundational model
- That model is then reused by many downstream systems

> [!important]
> You inherit the risks of everything used to train the model, not just the model itself.

# Real-World Example: Malicious Models
Malicious models have been discovered on public platforms where [attackers upload models](https://www.reversinglabs.com/blog/rl-identifies-malware-ml-model-hosted-on-hugging-face) designed to appear useful.

If such a model is used:
- It may contain hidden behaviors
- It may produce manipulated outputs
- It may execute unintended logic depending on how it is loaded

This demonstrates that models should be treated similarly to executable code from a security perspective.

## Typo Squatting Attacks
Typo squatting exploits human error in dependency naming.

An attacker:
- Registers a package with a name similar to a legitimate one
- Waits for users to mistype or misidentify the package
- Delivers a malicious dependency instead of the intended one

Example pattern:
- Legit: `ion-icons`
- Malicious: `ion_icons`, `ion-icon`

This becomes more dangerous with AI-assisted development.

## AI Code Generation as an Attack Vector
AI coding tools can introduce new risks by generating incorrect or hallucinated dependency names.

Scenario:
- A developer asks how to perform a task
- The AI suggests installing a package
- The package name is incorrect but plausible
- An attacker has already registered that name with malicious code

As AI tools move toward autonomous code execution (agentic systems), this risk increases because:
- Code may be executed without manual verification
- Dependency installation may be automated

> [!warning]
> AI-generated code can unintentionally act as a delivery mechanism for supply chain attacks.

## Additional Risk: Serialization and Execution
Some AI dependencies, especially models, are distributed in serialized formats.

When these are loaded:
- They may be deserialized into executable objects
- Certain formats (e.g., Python pickling) can execute arbitrary code

This creates a direct execution risk when loading external models or data.

> [!important]
> Loading a model can be equivalent to running untrusted code.

# Mitigations

## Training and Awareness
Security awareness must extend beyond traditional developers to include:
- AI engineers
- Data scientists
- ML practitioners

Teams should:
- Understand supply chain risks
- Share a common security vocabulary
- Treat AI development as part of a unified product security effort

> [!note]
> AI teams often receive less formal security training, increasing risk exposure.

## Dependency Validation
Before using any dependency:
- Analyze datasets statistically for anomalies
- Test models with edge cases and adversarial inputs
- Verify package authenticity and source

Validation should cover both:
- Functional correctness
- Security integrity

## Secure Dependency Handling
Be cautious with how dependencies are loaded:
- Avoid unsafe deserialization methods
- Understand execution behavior of model formats
- Restrict automatic execution of imported components

## Internal Registry (Self-Hosted)
A stronger control measure is to use an internal registry for dependencies.

Process:
- Approved team vets external dependencies
- Dependencies are stored internally
- Applications only pull from the internal registry

Benefits:
- Reduces risk of malicious updates
- Ensures all dependencies are pre-validated
- Enables monitoring and access control

Trade-offs:
- Infrastructure and maintenance overhead
- Potential delays in accessing new dependencies

## Access Control and Monitoring
- Restrict who can add or update dependencies
- Log usage and changes
- Monitor for anomalies in dependency behavior

This adds visibility into how dependencies are used over time.

# Key Takeaways
External dependencies significantly expand the attack surface of AI systems. Unlike traditional software, these dependencies include not only code but also data and models, each with unique risks. Supply chain attacks can propagate through any of these layers, making validation, monitoring, and controlled usage essential for maintaining security.