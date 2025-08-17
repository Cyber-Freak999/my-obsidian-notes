# **TL;DR – Prompt Engineering**

- A **prompt** is the input you give to a large language model (LLM).    
- **Prompt engineering** is crafting that input to get the kind of response you want.
- Prompts can be structured in specific ways—like giving examples or requesting reasoning—to improve LLM responses.
---

# **What is Prompt Engineering?**

- It’s the process of **designing prompts** to steer LLM behavior toward a desired output.    
- LLMs are **completion models** by default—they try to finish the text, not always to answer questions directly.

> ⚠️ Problem: Completion models may not follow instructions reliably.  
> ✅ Solution: Instruction tuning & prompting strategies help guide the model.

## **Instruction Tuning and RLHF**

- Instruction tuning trains the model to better **follow user instructions**.
- Example: Meta’s LLaMA 2 Chat is trained on **28,000 prompt-response pairs**.
### **RLHF (Reinforcement Learning from Human Feedback)**

- Humans rank or score model outputs.
- These scores train a **reward model** that teaches the LLM what humans prefer.
- Final model is tuned with reinforcement learning using that reward model.
# Prompting Strategies That Work

## **In-Context Learning (Few-Shot Prompting)**

- Provide **examples** of the task in the prompt.
- Doesn’t change model weights—just helps the model infer the task.
### **K-shot Prompting**

- Give the model **k examples** of the input-output format.
    - 0-shot = no examples
    - 1-shot = one example
    - 3-shot = three examples, etc.

> 📌 Example:  
> **Task**: Translate English to French  
> **Prompt with 3 examples**:

```
Translate: Hello → Bonjour  
Translate: Thank you → Merci  
Translate: Good night → Bonne nuit  
Translate: Cheese →  
```

This helps the model infer it should **translate Cheese → Fromage**.

## **Chain-of-Thought Prompting**

- Useful for **multi-step or reasoning-heavy** questions.
- You prompt the model to **"think step-by-step"** before answering.

> 📌 Example:

```
Roger starts with 5 tennis balls. He buys 2 cans with 3 balls each.  
How many total balls does he have?

Answer: Roger starts with 5.  
2 cans × 3 = 6 balls.  
Total = 5 + 6 = 11.  
Answer: 11
```

> Without CoT, the model might just guess 8 or 6 or give an incomplete answer.
# Other Concepts

## **Hallucination**

- A **hallucination** is when an LLM generates content that is:
    - **Factually incorrect**
    - **Not grounded** in training data
    - Or simply **made up**

> 🛑 Example of Hallucination:  
> “In the U.S., people gradually adopted driving on the left side of the road.”  
> → Factually incorrect (the U.S. drives on the right side).

> ⚠️ Fluent but wrong: Hallucinations often sound believable, which makes them **hard to detect**.

### Can we prevent hallucinations?
- **Not reliably**—but we can **reduce** them with **Retrieval-Augmented Generation (RAG)**. It helps by grounding LLMs in real data. Still an **active area of research**.
#  Summary Table

|Concept|Description|
|---|---|
|**Prompt**|Input text to the LLM|
|**Prompt Engineering**|Crafting prompts to guide output|
|**Instruction Tuning**|Fine-tuning a model to follow instructions|
|**RLHF**|Uses human feedback to align model output with human preferences|
|**Few-Shot Prompting**|Providing examples in the prompt|
|**Chain-of-Thought**|Prompting the model to reason step-by-step|
|**Hallucination**|Non-factual or fabricated model output|
