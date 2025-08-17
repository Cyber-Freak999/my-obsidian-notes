# TL;DR

- **Unsupervised learning** deals with data **without labeled outputs**.    
- It helps find **patterns, groupings, or structures** in data.
- A key technique is **clustering** — grouping similar data points.
- Examples:
    - **Market segmentation**
    - **Fraud detection (outliers)**
    - **Recommendation systems**
- The process involves:
    - **Preprocessing the data**
    - **Calculating similarity**
    - **Running clustering algorithms**
    - **Interpreting results iteratively**

---

# What is Unsupervised Learning?

- A type of machine learning where the model works on **unlabeled data**.    
- It tries to **find structure or hidden patterns** in the data automatically.
- You **don’t give it the correct answer**; instead, it learns what the groups or patterns might be.
A good analogy is like giving a child a mixed bag of LEGO blocks and asking them to group by **colour or shape** — they group based on visible patterns without instructions.
## 🍎 Fruit Example

Imagine you give a machine data about apples, bananas, and oranges, but without labels. The machine may group:

- Apples & cherries (red/round)
- Bananas (yellow/long)

This is **clustering** — grouping similar items based on features.
# Clustering

- Clustering means grouping data points so that:    
    - **Inside a cluster**: items are very similar.
    - **Between clusters**: items are dissimilar.
- If a data point doesn’t belong to any group, it's an **outlier**.
![[Pasted image 20250813112633.png]]
## 🧠 Common Applications

|Use Case|Example|
|---|---|
|📊 Market Segmentation|Grouping customers by purchase behavior|
|💳 Outlier Detection|Detecting credit card fraud through unusual patterns|
|🎬 Recommendations|Grouping users with similar movie preferences for personalized content|

# ⚙️ Workflow Steps in Unsupervised Learning

1. **🔧 Prepare the Data**    
    - Clean missing values
    - Normalize and scale features (so no feature dominates)
2. **🧮 Create a Similarity Matrix**
    - Measures how similar two data points are (range: 0 to 1)
    - Common metrics:
        - **Euclidean Distance** (straight-line distance)
        - **Manhattan Distance** (grid-like path)
        - **Cosine Similarity** (angle between vectors)
        - **Jaccard Similarity** (intersection over union)
3. **📌 Apply Clustering Algorithm**
    - Types:
        - **Partition-based**: e.g. K-Means
        - **Hierarchical**: tree of clusters e.g. Dendograms
        - **Density-based**: e.g. DBSCAN (good for outliers)
        - **Distribution-based**: assumes data follows a distribution (e.g. Gaussian Mixture Models)
4. **🔍 Interpret Results**
    - No labels = no direct way to evaluate
    - Check cluster behaviour and internal similarity
    - Iterate on preprocessing, metrics, algorithm choice
![[Pasted image 20250813112840.png]]
# Other Concepts

- **Similarity Score**: This shows how close two data points are to each other.
    - Closer to 1 → more similar
    - Closer to 0 → less similar
- **Outlier**: A data point that doesn't fit well in any cluster
- **No Labels**:
    - Unlike supervised learning, there's **no “correct answer”**
    - Success depends on how well the model finds meaningful structure
# **Key Takeaways**

- Useful when labels are **unavailable or expensive to obtain**
- Great for **exploration**, **pattern discovery**, and **anomaly detection**
- Model performance depends heavily on **data preprocessing** and **choice of similarity metric**