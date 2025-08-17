# Language-Related AI Tasks

## Text-Based Tasks (Non-generative)

- **Language Detection** – Identify the language used in the text.
- **Entity Extraction** – Pull out named entities like people, organisations, places.
- **Key Phrase Extraction** – Summarise the most important points.
- **Text Classification** – Categorise text (e.g., spam vs. not spam).
- **Translation** – Convert text from one language to another.

**Example:** Google Translate — Input text, choose languages, get translated output.
## Generative Language Tasks

- **Text Generation** – Stories, poems, essays (e.g., ChatGPT).
- **Summarization** – Generate concise summaries from large texts.    
- **Question Answering** – Answer questions based on a body of knowledge.
- **Dialogue Systems** – Build chatbots and virtual assistants.

## How Text Data Works:

- **Text is Sequential** – Meaning depends on word order.
- **Tokenization** – Convert words to numerical tokens.
- **Padding** – Equalize length of sequences for batch training.
- **Embedding** – Represent words/sentences in vector space to preserve meaning and similarity.
- **Similarity Metrics** – Cosine similarity or dot product to compare embeddings.

## Language Model Architectures:

|Model Type|Key Feature|
|---|---|
|**RNN** (Recurrent Neural Network)|Handles sequential data, keeps hidden state|
|**LSTM** (Long Short-Term Memory)|Better memory via gates to retain context|
|**Transformer**|Parallel processing using self-attention, basis of modern LLMs like GPT|

---
# Speech & Audio-Related AI Tasks

## Speech-to-Text & Recognition

- **ASR (Automatic Speech Recognition)** – Convert speech to written text.
- **Speaker Recognition** – Identify who is speaking.
- **Voice Conversion** – Modify one voice to sound like another.
##  Generative Audio Tasks
- **Speech Synthesis (Text-to-Speech)** – Generate human-like speech. 
- **Music Generation** – Compose music using AI models.
## How Audio Data Works:

- **Sampling Rate** – Number of snapshots per second (e.g., 44.1 kHz).
- **Bit Depth** – Info in each sample (higher = richer quality).
- **Temporal Nature** – Meaning comes from analyzing patterns over time, not single samples.

## Audio Model Architectures:

|Model Type|Purpose|
|---|---|
|**RNN / LSTM**|Handle time series of sound|
|**Transformer**|Scales better, captures long-range dependencies|
|**Variational Autoencoders (VAEs)**|Used in generative sound modeling|
|**Waveform Models**|Directly model raw audio signals (e.g., WaveNet)|
|**Siamese Networks**|Compare two audio samples for similarity (e.g., voice ID)|

---

# Vision-Related AI Tasks

## Image Recognition Tasks

- **Image Classification** – Label an image (e.g., cat or dog).
- **Object Detection** – Identify and locate objects (bounding boxes).
- **Facial Recognition** – Identify/verify people using faces.
## Generative Vision Tasks

- **Text-to-Image Generation** – Create visuals from descriptions (e.g., DALL·E).
- **Style Transfer** – Apply an artistic style to a photo.
- **3D Modeling** – Generate objects, components, or people in 3D.

## 🔹 How Image Data Works:

- **Pixel-Based Input** – Images are grids of pixels (RGB or grayscale).    
- **No Insight from Single Pixel** – Meaning is derived from spatial patterns.
- **Task Determines Data Format** – Some tasks need full images, others just features.
## Vision Model Architectures

| Model                                      | Description                                               |
| ------------------------------------------ | --------------------------------------------------------- |
| **CNN** (Convolutional Neural Network)     | Extracts visual features, detects edges, textures, shapes |
| **YOLO (You Only Look Once)**              | Fast object detection in one pass                         |
| **GANs (Generative Adversarial Networks)** | Create realistic fake images or videos                    |

---

# **Other Cross-Domain AI Tasks**

## Anomaly Detection

- **Use Case**: Fraud detection, machine failures
- **Data Type**: Time series (single/multivariate)

## Recommendation Systems

- **Use Case**: Product or content suggestions (e.g., Netflix, Amazon)
- **Data Needed**: User behaviour, item features, collaborative filtering

## Forecasting

- **Use Case**: Weather, stock prices, demand forecasting
- **Data Type**: Time series data over consistent intervals

---

### 🔍 Summary Table

|Domain|Input|Output|Example Tasks|Key Models|
|---|---|---|---|---|
|Language|Text|Text / Label|Translation, QA, Chat, Summarization|RNN, LSTM, Transformer|
|Speech|Audio|Text / Audio|Speech-to-text, Synthesis, Music|RNN, LSTM, Transformer, VAE|
|Vision|Image|Label / Bounding Boxes / Image|Classification, Detection, Generation|CNN, YOLO, GAN|
|Other|Time Series|Prediction / Alert|Anomaly detection, Forecasting|RNN, LSTM, Transformers|
