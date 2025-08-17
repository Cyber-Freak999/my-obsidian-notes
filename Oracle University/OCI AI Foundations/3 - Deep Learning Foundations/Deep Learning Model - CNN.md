# TL;DR
This lesson introduces **Convolutional Neural Networks (CNNs)**—a deep learning model designed to process **grid-like data** such as **images** and **videos**. CNNs automatically detect and learn patterns like edges and textures using **convolutional layers**, **activation functions**, and **pooling layers**. These features are then passed to **fully connected layers** for classification. CNNs are widely used in image classification, object detection, face recognition, medical imaging, and more. Despite their power, they can be computationally expensive, prone to overfitting, and difficult to interpret.

---

# **Overview of Deep Learning Architectures**

|Architecture|Description|Application Area|
|---|---|---|
|**FNN / MLP**|Feedforward Neural Network / Multilayer Perceptron; basic neural network with dense layers|Simple classification tasks|
|**CNN**|Convolutional Neural Network; detects local patterns in images|Image, video processing|
|**RNN**|Recurrent Neural Network; designed for sequential data|NLP, time-series|
|**Autoencoder**|Learns compressed representations (unsupervised)|Dimensionality reduction, anomaly detection|
|**LSTM**|Long Short-Term Memory; variant of RNN for long sequences|Translation, speech|
|**GAN**|Generative Adversarial Network; learns to generate data|Image generation, deepfakes|
|**Transformer**|Attention-based model, replaces RNNs/LSTMs|NLP, LLMs, translation, generation|

# What is a CNN?

CNNs are deep learning models tailored for **spatial (grid-like) data** such as:
- **Images** (2D grids of pixel values)
- **Videos** (3D with temporal dimension)
Unlike ANN, which **flattens the image into 1D**, CNN maintains the **spatial structure**—critical for visual tasks.
## CNN Architecture Overview

| Layer Type                      | Description                                                         | Analogy             |
| ------------------------------- | ------------------------------------------------------------------- | ------------------- |
| **Input Layer**                 | Accepts image input (e.g., 224x224x3 for RGB)                       | Raw house image     |
| **Convolutional Layer**         | Applies filters (kernels) to detect patterns like edges or textures | Blueprint detector  |
| **Activation Function (ReLU)**  | Introduces non-linearity, enabling learning of complex features     | Pattern highlighter |
| **Pooling Layer (Max/Average)** | Reduces spatial dimensions while keeping important info             | Room summarizer     |
| **Fully Connected (Dense)**     | Combines features to make final decision                            | House expert        |
| **Softmax Layer**               | Outputs probability for each class                                  | Guess maker         |
| **Dropout Layer**               | Prevents overfitting by randomly disabling neurons during training  | Quality checker     |

![[Pasted image 20250814155626.png]]
## Layers in Detail

### Convolutional Layer

- Uses filters/kernels (e.g., 3x3) that **slide** over the image.    
- Detects **low-level features** in early layers (edges), and **high-level features** in deeper layers (faces, objects).
### Activation Function (ReLU)

- ReLU = Rectified Linear Unit = `max(0, x)`
- Introduces **non-linearity** and helps CNN learn **complex patterns**.

### Pooling Layer

- Typically **MaxPooling** is used: selects the **maximum** value in a small window (e.g., 2x2).
- Reduces **computational load** and **feature map size**, aiding generalization.

### Fully Connected (Dense) Layer

- Final layer(s) where **flattened features** are used to make predictions.
- Often followed by **Softmax** to convert raw scores into class probabilities.

### Dropout Layer

- Randomly turns off a fraction of neurons (e.g., 0.5 = 50%) during training.
- Reduces **overfitting** by preventing the model from relying too heavily on any one neuron.

## Example Use Case: CNN for Image Classification

1. **Input**: An image of a dog (e.g., 128x128x3).
2. **Convolutions**: Detects textures, edges, and shapes.
3. **Pooling**: Reduces image resolution while keeping essential features.
4. **Fully Connected Layer**: Interprets features and predicts the label.
5. **Softmax**: Outputs probability that it’s a “dog”, “cat”, etc.
## CNN Limitations

| Limitation                  | Description                                       |
| --------------------------- | ------------------------------------------------- |
| **High Computational Cost** | Training requires GPUs and large memory           |
| **Overfitting**             | Especially when data is limited or imbalanced     |
| **Black Box**               | Hard to interpret why CNN made a certain decision |
| **Input Sensitivity**       | Small input changes can cause wrong predictions   |

# **CNN Applications**

|Domain|Use Case|
|---|---|
|**Image Classification**|Cat vs. Dog, Cancer Detection|
|**Object Detection**|Bounding boxes for faces, vehicles|
|**Image Segmentation**|Labeling each pixel (e.g., tumor vs. healthy)|
|**Face Recognition**|Biometric authentication|
|**Medical Imaging**|Tumor detection, X-ray analysis|
|**Autonomous Vehicles**|Road sign detection, pedestrian detection|
|**Remote Sensing**|Satellite image classification|

# CNN vs ANN

|Feature|ANN|CNN|
|---|---|---|
|Input|Flattened vector|2D image grid|
|Spatial Structure|Lost|Preserved|
|Feature Extraction|Manual / learned|Automatic|
|Performance on Images|Poor|Excellent|

# Summary

- CNNs are **specialized for image/video data**.
- They **automatically learn features** at multiple levels of abstraction.
- Key components: **convolution, activation, pooling, dense layers**.
- Widely used in industries like healthcare, security, automotive, and remote sensing.
- Despite limitations, CNNs remain foundational in **computer vision** and are often combined with other architectures (e.g., RNN, transformers) for multimodal tasks.