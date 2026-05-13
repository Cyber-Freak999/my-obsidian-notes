---
tags:
  - ai
  - ai-security
  - threat-modeling
  - data-poisoning
  - machine-learning
  - application-security
---
## Summary
Internal data represents one of the most critical assets in an AI system because it directly influences how the model behaves. Attacks targeting this layer aim to subtly manipulate training data so that the model behaves normally in most cases but fails under specific conditions. These attacks are often difficult to detect and can be highly targeted.

---
## Internal vs External Data in Threat Modeling

^587212

In this [threat model](Threat%20Model%20for%20AI%20Application.canvas), inputs are separated into internal and external data because they introduce different risks.

Internal data refers to proprietary datasets owned or controlled by an organization. These datasets often provide a competitive advantage and are the foundation for building unique AI models.

External data, on the other hand, comes from third-party or public sources and introduces different trust and validation challenges.

> [!important]
> Internal data is a high-value target because compromising it directly impacts model behavior at its core.

## Why Internal Data Matters
Internal datasets are not just inputs; they define how the model learns patterns and makes decisions. Because of this, they effectively shape the “intelligence” of the system.

A model trained on proprietary data becomes unique to an organization, creating a defensible advantage. This also means that if an attacker can influence this data, they can indirectly control how the model behaves.

## Data Poisoning Attacks
Data poisoning refers to the manipulation of training data to influence model behavior in a controlled or malicious way.

This can involve:
- Modifying existing data or labels
- Injecting new malicious data points
- Removing critical data to skew learning

Related concepts include:
- Model skewing
- Trigger-based attacks
- Backdoor attacks

These attacks are typically subtle and designed to avoid detection during normal testing.

## Example: Stop Sign Classification Attack
Consider a model trained to classify road signs such as stop signs and speed limit signs. The training dataset contains labeled images that teach the model how to distinguish between them.

An attacker could introduce a small number of manipulated samples into the dataset. For example, they might:
- Add a visual trigger (e.g., a yellow stripe on a stop sign)
- Change the label so that the modified stop sign is classified incorrectly

Even if only a few samples are altered, the model may learn an association between the trigger and the wrong label.

In practice:
- The model performs correctly on normal inputs
- The model fails when the specific trigger is present

> [!warning]
> These attacks are hard to detect because standard test data usually does not include the trigger condition.

## Real-World Example: Gmail Spam Filtering
A real-world example of data poisoning occurred in attempts to manipulate spam filters.

Attackers created networks of controlled email accounts and performed the following:
- Sent spam emails between accounts they controlled
- Marked those spam emails as “not spam”

The goal was to influence the training data used by the spam filter so that similar emails would bypass detection.

This created observable spikes in user feedback data, which allowed detection in this case.

> [!note]
> Large-scale or noisy attacks are easier to detect, but subtle poisoning attempts may go unnoticed.

## Real-World Example: AI Search Manipulation
AI-powered search summaries introduce new attack vectors.

In one case, a user searched for a customer service number and received an AI-generated summary containing a malicious phone number. The attacker had successfully injected misleading data into the system’s knowledge sources.

This is similar to traditional search engine manipulation (SEO poisoning), but AI systems amplify the risk by:
- Aggregating information automatically
- Presenting it with higher perceived trust

> [!warning]
> AI systems can unintentionally legitimize malicious data if ingestion pipelines are not properly controlled.

## Unintentional Data Poisoning
Not all data poisoning is malicious. It can also occur due to poor data quality or incorrect assumptions.

For example:
- Ingesting intentionally vulnerable applications (e.g., training labs) as if they were secure systems
- Using outdated or biased datasets
- Mislabeling data during manual annotation

This leads to models learning incorrect or misleading patterns.

> [!important]
> Poor data quality can degrade model performance just as effectively as malicious attacks.

## Attack Characteristics
Data poisoning attacks share several key properties:
- Only a small percentage of data needs to be altered
- The model behaves normally under expected conditions
- Failures occur only under specific, attacker-controlled inputs
- Detection is difficult without targeted testing or monitoring

These characteristics make data poisoning particularly dangerous in production systems.

## Mitigations

### Data Validation
Training data should be validated before use to ensure it is:
- Accurate
- Consistent
- Fit for purpose

This includes both functional validation (correctness, bias) and security validation (tampering, anomalies).

> [!note]
> The principle of “garbage in, garbage out” applies strongly here.

### Secure Data Storage
Training data must be stored securely using standard best practices:
- Access control (least privilege)
- Secure credential management
- Protection of storage systems (e.g., cloud buckets)

Many real-world issues in this area are caused by misconfigurations or human error.

### Label Integrity Controls
If data is manually labeled:
- Use multiple independent labelers
- Compare results to detect inconsistencies
- Monitor for anomalies in labeling patterns

This reduces the risk of a single compromised source affecting the dataset.

### Monitoring and Drift Detection
Continuous monitoring is essential to detect:
- Model drift (performance degradation over time)
- Data distribution changes
- Sudden spikes or anomalies in input data

This includes detecting patterns similar to the Gmail example, where unusual activity may indicate manipulation.

### Auditing
Regular audits should be conducted to identify:
- Data tampering
- Unexpected changes in data distribution
- Label inconsistencies

> [!tip]
> This is an area where good product practices and good security practices strongly overlap.

## Key Takeaways
Internal data is one of the most critical components in an AI system and a primary target for attackers. Data poisoning attacks are subtle, effective, and difficult to detect, often requiring only minimal changes to influence model behavior. Strong validation, monitoring, and access control are essential to maintaining data integrity and securing the AI pipeline.