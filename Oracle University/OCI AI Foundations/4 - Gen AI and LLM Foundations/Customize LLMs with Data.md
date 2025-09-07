# **Framework Overview**

- **Horizontal (Context Optimization):** Injects more _specific_ data (like user orders, internal docs) into the model's responses.
- **Vertical (LLM Optimization):** Customizes the _model itself_ for specific domains or tasks (e.g. legal, finance, support).	

![[Pasted image 20250820160109.png]]

# Core Methods to Customize LLMs

1. **Prompt Engineering**
    - **What it is:** Manually crafting inputs to guide the model.
    - **Pros:** Fast, no cost, zero setup.
    - **Cons:** Add latency to each request.
    - **When to use:** When the LLM already understands the domain/task.
    - **Example:** Giving the model clear, structured examples or instructions in the prompt.
2. **RAG (Retrieval-Augmented Generation)**
    - **What it is:** Enhances the LLM with external knowledge bases (e.g. wikis, vector DBs).
    - **How it works:**
        - _Retrieval_ – Finds relevant docs from a private corpus.
        - _Augmented Generation_ – Uses those docs to craft responses.
    - **Use Case Example:** Customer uploads a receipt → LLM checks return policy in a database → replies accordingly.
    - **When to use:** 
	    - when data changes rapidly
	    - To mitigate hallucination by grounding answers.
    - **Pros:**
        - No fine-tuning required.
        - Grounded responses (fewer hallucinations).
        - Access to private or real-time info.
    - **Cons:**
        - Needs clean, indexed data.
        - More complex to set up.
3. **Fine-Tuning**
    - **What it is:** Training the model on _custom domain-specific_ data to change how it behaves or what it knows.
    - **How it works:** Pre-trained model + custom data → fine-tuned model.
    - **When to use:**
        - When the base model struggles with your task or domain.
        - To enforce specific tone, format, or jargon.
        - Very large data required to adapt the LLM for prompt engineering
        - Latency in current llms is too high
    - **Pros:**
        - Higher task-specific accuracy.
        - Can reduce token count (more efficient responses).
    - **Cons:**
        - Requires labeled data (costly).
        - Computationally expensive (though lighter options like **T-Few** exist — only updates small parts of the model).

# 🔄 **Iterative Workflow for Customizing LLMs**

1. Start simple with prompt engineering with a simple prompt.
2. Add Few shot prompting.
3. Add single retrieval with RAG if prompts aren't enough and your use case depends on private or changing info.
4. **Fine-tune** if RAG doesn't get the response style or behaviour right.
5. **Optimize RAG** and fine-tuning as needed.

> You may eventually use **all three methods** together — they’re additive, not exclusive.

![[Pasted image 20250820161513.png]]