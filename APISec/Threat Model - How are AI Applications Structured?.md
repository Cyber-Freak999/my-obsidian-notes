---
tags:
  - ai
  - ai-security
  - application-architecture
  - threat-modeling
  - machine-learning
---
# TL;DR
Artificial Intelligence refers to systems that can take in information, reason about it, and act toward a goal. These systems vary widely in how they operate, but most follow a similar lifecycle and are embedded within larger applications rather than existing on their own.

---
## What is Artificial Intelligence?
At a high level, AI can be understood as a system that senses its environment, plans toward a desired outcome, and executes actions to achieve that outcome. This definition is intentionally broad because it applies to everything from simple rule-based systems to modern AI agents.

The “environment” an AI interacts with may be physical, such as sensors in robotics, or purely digital, such as APIs, databases, or user inputs. Similarly, planning can range from predefined logic to complex learned behavior, while execution may be as simple as returning a prediction or as complex as triggering actions across systems.

> [!note]
> This broad definition is useful because security concerns apply across all levels of AI complexity.

## AI Exists on a Spectrum
Not all AI systems behave the same way. They differ primarily in how they sense, plan, and execute.

Some systems operate on tightly controlled inputs and simple rules, while others continuously ingest real-time data and make autonomous decisions. A spam filter, for example, has limited scope and autonomy, whereas an AI agent may plan and act with minimal human intervention.

A key concept here is that autonomy increases both capability and risk. The more control a system has over decisions and actions, the more impact it can have if something goes wrong.

## Human-in-the-Loop (HITL)
In many real-world systems, humans are still part of the decision-making process. This is known as human-in-the-loop.

Humans may review outputs, approve actions, or provide feedback that improves the model over time. This helps reduce errors and adds a layer of accountability.

> [!warning]
> While this reduces technical risk, it introduces human-focused attack vectors such as manipulation or over-reliance on AI outputs.

## AI Capability Model
AI systems can also be understood through four core capabilities: understand, plan, interact, and execute.

- Understand: interpreting input data such as text, images, or signals  
- Plan: deciding what to do based on that input  
- Interact: communicating with users or other systems  
- Execute: taking action within an environment  

These capabilities often overlap. For example, a chatbot must understand input before it can interact meaningfully, and execution may involve interacting with external systems.

## AI Subfields
AI is not a single technology but a collection of subfields, each focused on different types of problems.

- Natural Language Processing (NLP) deals with text and language
- Computer Vision focuses on images and video
- Generative AI creates new content
- Prediction models estimate outcomes
- Optimization focuses on decision efficiency

Most security concepts apply across these areas, even though the implementations differ.

## Structure of AI Applications
Here is a [sample threat model for AI Application](Threat%20Model%20for%20AI%20Application.canvas)

### Inputs Stage
This stage is responsible for gathering and preparing data before it is used by the model. It includes raw data collection, preprocessing, and feature engineering.

Data may come from multiple sources, including external systems, which introduces trust boundaries. Because of this, the input stage is one of the most critical points in the system. It normally split between [internal and external data](Threat%20Model%20-%20Internal%20Data.md#^587212).

> [!warning]
> Malicious or low-quality data at this stage can directly influence model behavior.

### Training Stage
The training stage is where the model learns patterns from data. It involves training, evaluation, and validation, and is rarely a one-time process.

Instead, it follows an iterative loop:
- Train the model
- Evaluate performance
- Adjust parameters or data
- Retrain

This loop continues until the model reaches an acceptable level of performance.

> [!important]
> Issues introduced during training can persist throughout the entire lifecycle of the system.

### Deployment / Application Layer
Once trained, the model is integrated into an application where it interacts with users or other systems. This layer handles incoming requests, sends them to the model, and returns outputs.

Unlike traditional software components, the model’s behavior may not always be predictable, which makes this layer particularly sensitive.

> [!tip]
> Architecturally, this often resembles an API where the model acts as a service.

## Security Insights
AI systems introduce new attack surfaces across the entire pipeline. Unlike traditional applications, where focus is often on code and infrastructure, AI systems must also account for data and model behavior.

Key risk areas include:
- Input manipulation (e.g., data poisoning)
- Training weaknesses (e.g., biased or compromised datasets)
- Runtime manipulation (e.g., prompt injection)
- Integration risks (e.g., insecure APIs)

> [!warning]
> Security must be applied across data flow, model logic, and system integration.

## Best Practices
- Validate and sanitize all incoming data
- Track the origin and integrity of datasets
- Monitor model behavior in production
- Log inputs and outputs for auditing
- Restrict access to training pipelines and models
- Apply threat modeling across all components

## Key Takeaways
AI systems are best understood as pipelines that sense, plan, and act. Their behavior depends heavily on data, iteration, and integration with larger systems. Because of this, security must be considered at every stage rather than treated as an afterthought.