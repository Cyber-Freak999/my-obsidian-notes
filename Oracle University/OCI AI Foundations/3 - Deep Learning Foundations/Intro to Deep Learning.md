# TL;DR
This lesson introduces **deep learning**, a subset of machine learning that uses **artificial neural networks (ANNs)** to automatically extract features from raw data (e.g., image pixels) and predict outcomes. It explains how ANNs work, highlights key deep learning architectures like CNNs and transformers, and outlines their use in tasks involving images, text, and audio. It also covers a brief history of deep learning and walks through an example of training an ANN to recognize handwritten hdigits using backpropagation.

---

# **What is Deep Learning?**

- A subset of Machine Learning that focuses on using **artificial neural networks (ANNs)** to model and solve complex tasks.
- **Raw Data Processing**: ANNs can take raw input (e.g., image pixels) and **learn patterns automatically** without needing manual feature selection.
- **Example**: Handwritten digit recognition — input is image pixels, ANN learns features like edges/curves, and outputs a predicted digit (0–9).
![[Pasted image 20250813122026.png]]

# Deep Learning vs Traditional ML

| Machine Learning                                  | Deep Learning                                                    |
| ------------------------------------------------- | ---------------------------------------------------------------- |
| Requires manual feature extraction                | Automatically extracts features                                  |
| Struggles with complex data (images, text)        | Excels at learning from complex, high-dimensional data           |
| Slower with large data due to limited scalability | Uses **parallel processing (e.g., on GPUs)** for faster training |

# History of Deep Learning

- **1950s**: Introduction of artificial neurons, perceptrons, and multilayer perceptrons (MLP).    
- **1980s**: Development of **backpropagation** — essential for training deep networks.
- **1990s**: Rise of **Convolutional Neural Networks (CNNs)** for image processing.
- **2000s**: Availability of GPUs enhanced model training speed.
- **2010s**: Breakthroughs like **AlexNet**, **Deep Q-Networks**, and growing popularity of **generative models**.
- **Today**: Deep learning powers **large language models**, **text-to-image generation**, **speech recognition**, etc.
# Types of Data & Applications

|**Data Type**|**Applications**|
|---|---|
|**Image**|Classification, object detection, segmentation, facial recognition|
|**Text**|Sentiment analysis, translation, summarization, Q&A|
|**Audio**|Speech-to-text, music generation, voice synthesis|
|**Video**|Action recognition, video summarization|
# Choosing the Right DL Architecture

|**Task**|**Architecture**|
|---|---|
|Image classification, detection|**CNN**|
|Text processing|**Transformers**, **LSTM**, **RNN**|
|Text summarization, Q&A|**Transformers**|
|Image generation|**GANs**, **Transformers**, **Diffusion models**|

![[Pasted image 20250813121317.png]]

# What is an Artificial Neural Network (ANN)?

ANNs are **computational models inspired by the human brain**; consists of interconnected neurons called nodes.
![[Pasted image 20250813122535.png]]
## Components

1. **Layers**:
    - **Input Layer**: Receives raw data (e.g., 28x28 pixel image).
    - **Hidden Layers**: Process and transform data.
    - **Output Layer**: Provides final prediction (e.g., digit 0–9).
2. **Neurons**: Basic computation units in each layer.
3. **Weights**: Determine strength of connections between neurons.
4. **Bias**: Extra input allowing flexibility in decision boundaries.
5. **Activation Function**: Determines output of the neuron by working on the weighted sum of its input(e.g., ReLU, Sigmoid).

E.g. Training ANN to Recognize Handwritten Digits
- **Input**: 28x28 pixel images (784 inputs).
- **Architecture**:
    - Input layer: 784 nodes
    - Two hidden layers: 16 neurons each
    - Output layer: 10 neurons (digits 0–9)

## How ANN are trained

1. **Forward Pass**:    
    - Show input image (e.g., digit 2) to the network.
    - Output is predicted (e.g., mistakenly outputs 6).
2. **Error Calculation**:
    - Difference between predicted and actual output is computed.
3. **Backpropagation**:    
    - **Adjust weights** using the error to reduce future mistakes.
4. **Iterate**:
    - Repeat over thousands of images to improve accuracy.

> **Result**: After training, the model generalizes and accurately predicts unseen handwritten digits.
![[Pasted image 20250813123807.png]]

# Key Takeaways

- **Deep learning excels** where traditional ML struggles — especially for unstructured data.    
- **ANNs automatically learn features** from raw data, making them suitable for complex tasks.
- **Backpropagation + parallel computation** are critical for effective training.
- Deep learning is now foundational for modern **AI applications**, including **LLMs**, **speech systems**, **image generators**, and more.

