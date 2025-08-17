# TL;DR

- **Supervised learning** uses labeled data to learn the relationship between input and output.
- If the output is **continuous** (e.g., price), we use **regression**.
- **Linear regression** finds the best-fitting straight line through the data to make predictions.
- The line has an **equation**:
	$$
		f(x)=w⋅x+bf(x) = w \cdot x + b
	$$
    where:
    - `x` is the input (e.g., house size)
    - `w` is the slope (how much price changes with size)
    - `b` is the y-intercept (bias)
- The model learns `w` and `b` by minimizing the **loss**, which is the squared difference between predicted and actual values.
- Once trained, the model can predict outcomes for new inputs (e.g., predict house price for a new size).

---

#  What is Supervised Learning?

- A **machine learning approach** where the model learns from **labeled data** (input-output pairs).
- The goal is to **learn the mapping** between input features and output labels.
- Think of it like a teacher-student relationship — the teacher (data) shows examples, and the model (student) learns from them.
# Real-World Examples of Supervised Learning

|**Use Case**|**Input**|**Output**|**Type**|
|---|---|---|---|
|House Price Prediction|Size in square feet|Price in dollars|Regression|
|Cancer Detection|Medical details|Malignant or not|Classification|
|Sentiment Analysis|Customer reviews|Positive/Neutral/Negative|Classification|
|Stock Price Prediction|Market data|Future price|Regression|

# Regression vs. Classification

- **Regression** is used when the output is **continuous** (e.g., price, temperature).
- **Classification** is used when the output is **categorical** (e.g., spam/not spam).
## 🏠 Example: House Price Prediction

### Goal:
Predict house price based on its size (square feet).
### Data:
You have a **table** of:
- **Input (x)**: House size
- **Output (y)**: House price

![[Pasted image 20250813100800.png]]

Each row in the table is a **training example** — also called a **tuple**.
### Visualizing the Data

- Plot the data on a **scatter plot**.
- We observe that as **house size increases, the price also increases**.
- We fit a **straight line** through these points to capture the trend.

![[Pasted image 20250813100829.png]]

The relationship is modeled as:
$$
f_{w,b}(X) = w \cdot X + b
$$
- `x`: Input (house size)    
- `f(x)`: Output (predicted price)
- `w`: Slope (how much price changes per square foot)
- `b`: Bias (starting point on the y-axis)

### Adjusting the Line
- Change **slope (w)** → tilt the line
- Change **bias (b)** → shift the line up/down

![[Pasted image 20250813104110.png]]

### How the Model Learns
- The model adjusts `w` and `b` **iteratively** to fit the line.
- The goal is to **minimise the loss**

> [!NOTE] Loss and Errors
> This is the number indicating how far the predicted value from the actual value.
> Squared loss, most commonly used, is the squared difference between the predicted point and the actual data point, which needs to be minimized during training.
  
$$
{Loss} = (f(x) - y)^2
$$

### Optimization:
- The model **minimizes loss** using algorithms like **gradient descent**.
- Once loss is minimized → best-fitting line is found.
### Making Predictions

Once trained, the model can be used like this:
- Input: `x = 1100` (square feet)
- Model applies: `f(x) = w * 1100 + b`
- Output: Predicted house price

![[Pasted image 20250813115257.png]]
