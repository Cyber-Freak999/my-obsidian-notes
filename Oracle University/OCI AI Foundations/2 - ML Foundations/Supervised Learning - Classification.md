# ✅ **TL;DR — Supervised Learning: Classification**

- **Supervised learning** uses labeled data to train models.    
- If the output is:
    - **Continuous** → use **regression**
    - **Categorical** → use **classification**
- **Classification** predicts categories (e.g., spam or not spam).
- Two types of classification:
    - **Binary classification**: Two possible outputs
    - **Multi-class classification**: More than two outputs
- **Logistic regression** is a basic classification algorithm that uses the **sigmoid function** to predict probabilities between 0 and 1.
- Example: Predicting **pass or fail** from **hours of study**.
- If predicted probability > 0.5 → **Pass**, otherwise → **Fail**

---

#  What is Supervised Learning?

Supervised learning is a type of machine learning where:
- We train the model on **labeled data** (input + correct output).
- The model **learns the mapping** between inputs (features) and outputs (labels).

There are two main types:
1. **Regression** → Predicts **continuous values** (e.g., price, temperature)
2. **Classification** → Predicts **categories or labels**

![[Pasted image 20250812141122.png]]

# Classification in Supervised Learning

**Classification** is used when the output label is categorical (e.g., yes/no, dog/cat).
##  Examples:

- **Binary Classification**: Only two classes  
    (e.g., spam vs. not spam, pass vs. fail)  
- **Multi-Class Classification**: More than two classes  
    (e.g., classifying sentiment as positive/negative/neutral)

## 🤖 How Classification Models Work

1. Start with a **labeled dataset**.
2. Train a **classifier** to recognize patterns between input features and categories.
3. Use the trained classifier to predict labels for new, unseen data.

#  Logistic Regression (A Simple Classifier)

- Despite the name, **logistic regression is used for classification**, not regression.    
- It predicts the **probability** of a binary outcome.
- Uses the **sigmoid function** to produce outputs between 0 and 1.

## Sigmoid Function:

Transforms real-valued input (like hours of study) into a probability (0 to 1):

$$
σ(x)=11+e−x\sigma(x) = \frac{1}{1 + e^{-x}}
$$

### Example: Pass or Fail Prediction

- **Feature**: Hours of study
- **Label**: Pass (1) or Fail (0)
### Classification rule:

- If predicted probability > 0.5 → classify as **Pass**    
- If predicted probability ≤ 0.5 → classify as **Fail**

**Example outcomes**:

- 6 hours → 80% probability → Pass    
- 4 hours → 20% probability → Fail

## 🌸 Multi-Class Classification: Iris Dataset

The **Iris dataset** is a classic example:

- Contains **150 samples** of three flower species: Iris Setosa, Iris Versicolor, Iris Virginica
- Each sample has **4 features**:
    - Sepal length & width
    - Petal length & width

**Goal**: Predict flower species based on features.

Since there are 3 classes, it's a **multi-class classification** problem.

