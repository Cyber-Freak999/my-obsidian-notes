# Artificial Intelligence (AI)**

- **Definition**: AI is the broad field of creating systems or machines that simulate human intelligence.    
- **Goal**: Perform tasks like reasoning, learning, decision-making, perception, and language understanding.
- **Example**:
    - A **self-driving car** making decisions like a human (e.g., changing lanes, avoiding pedestrians).
- **Includes**: Machine learning, rule-based systems, robotics, expert systems, etc.

# Machine Learning (ML)

- **Definition**: A **subset of AI** that enables machines to learn from data and improve over time without explicit programming. 
- **Goal**: Create algorithms that make predictions or decisions based on data.
- **Example**:
    - **Spam email filters** learning to identify spam based on email content and user behavior.

## 🧮 What’s an ML Algorithm?

A **set of mathematical rules or procedures** the model follows to learn from data and improve predictions.

# Deep Learning (DL)

- **Definition**: A **subset of ML** using deep neural networks to learn complex patterns.
- **Goal**: Enable machines to automatically extract features from raw data.
- **Example**:
    - **Image recognition software** identifying cats or dogs in pictures using deep neural networks.

![[Pasted image 20250805230708.png]]
# 🔀 **Comparison Table**

|Feature|AI|ML|DL|
|---|---|---|---|
|Scope|Broad (mimics human intelligence)|Subset of AI (learns from data)|Subset of ML (uses neural nets)|
|Human-like tasks|Yes|No (focus on data & patterns)|No (focus on deep patterns)|
|Example|Self-driving car|Spam detection|Face recognition|
|Input Type|Structured or unstructured|Structured / Labeled or unlabeled|Mostly unstructured (e.g., images, audio)|
|Model Complexity|Varies|Moderate|High (multi-layer networks)|

# 🔍 **Types of Machine Learning**

## Supervised Learning

- **Definition**: The model learns from **labelled data**.
- **Use Case**: Credit card approval
- **Process**:
    1. Train on historical, labelled data (e.g., approved or denied applications)
    2. Algorithm builds a **predictive model**
    3. Model predicts outcomes for new, unseen data
- **Example**: Predict if a new applicant qualifies for a credit card
- ✅ Pros: Interpretable, measurable accuracy
- ❌ Cons: Needs labelled data, may not work well with changing patterns

![[Pasted image 20250805230837.png]]
## Unsupervised Learning

- **Definition**: The model learns from **unlabelled data** by discovering patterns or groupings.
- **Use Case**: Customer segmentation in retail or streaming usage analysis
- **Example**: Clustering users based on income, household size, or watch time
- **Additional Example**:  
    Group fruits and vegetables based on nutritional similarities to balance a diet
- ✅ Pros: Great for insights & discovery
- ❌ Cons: Hard to validate accuracy, less interpretable

## Reinforcement Learning

- **Definition**: A learning method where agents learn by **interacting with an environment** and receiving rewards or punishments.
- **Use Case**: Game playing (chess), robotics, autonomous driving
- **Process**:
    1. Try an action 
    2. Get reward or penalty 
    3. Learn from feedback
- ✅ Pros: Powerful for dynamic environments   
- ❌ Cons: Computationally expensive, slower to train
# Deep Learning & Neural Networks

- **Neural Networks**:
    - Modeled after the human brain (neurons + layers)
    - Learn to approximate functions from input → output
    - Useful when rules/features can’t be manually defined (e.g., pixel patterns)
![[Pasted image 20250805231809.png]]
- **Functional Approximation**:
    - Estimating a hidden function by learning from known data
    - E.g., Learning the relationship between image pixels and labels like “cat” or “dog”
![[Pasted image 20250805231840.png]]
- **Deep Neural Networks (DNN)**:
    - Multiple hidden layers
    - Automatically extract features
    - Handle raw data like images, audio, and text
# Generative AI

- **Definition**: A branch of ML/DL that **creates new content** (text, audio, images).
- **Examples**:
    - **ChatGPT**: Generates human-like text
    - **DALL·E**: Generates images from text prompts
    - **MusicLM**: Composes music
- **How it works**: Trains on massive datasets to learn patterns and generate new outputs



