# TL;DR
This lesson introduces **deep learning models for sequential data**, especially relevant in tasks like **text, audio, and time series**. Key models include **Recurrent Neural Networks (RNNs)** and **Long Short-Term Memory (LSTM)** networks. RNNs can process sequences by maintaining a **hidden state** across timesteps but struggle with long-term dependencies. LSTMs address this with **memory cells and gates** (input, forget, output) that allow them to retain or discard information selectively. These models are widely used in **NLP, speech recognition, music generation**, and **time series forecasting**.

---
# What Are Sequence Models?

Sequence models are **deep learning architectures** that handle **ordered data** — data where the order of inputs matters. Common Applications:
- **Natural Language Processing (NLP)**:
    - Text classification (e.g., sentiment analysis)
    - Machine translation (e.g., English to French)
    - Text generation (e.g., chatbots, story writing)
- **Speech Recognition**: Turning audio waveforms into text.
- **Music Generation**: Creating melodies or harmonies over time.
- **Gesture Recognition**: Interpreting sequences of movements, e.g., sign language.
- **Time Series Forecasting**: Predicting future stock prices, weather, etc.
# Recurrent Neural Networks (RNNs)

RNNs are specifically designed for sequence data.
## Key Features

- **Feedback loop**: Allows the output from previous steps to influence future steps.
- **Hidden state**: Maintains memory of past inputs — critical for understanding context.
- Captures dependencies.
## Types of Sequence Mapping in RNNs

|Architecture Type|Description|Example|
|---|---|---|
|**One-to-One**|Standard NN (no sequence)|Image classification|
|**One-to-Many**|Single input, sequence output|Music generation|
|**Many-to-One**|Sequence input, single output|Sentiment analysis|
|**Many-to-Many**|Sequence input, sequence output|Machine translation|

### ⚠️ Limitation

**Vanishing Gradient Problem**: As the sequence gets longer, gradients during backpropagation become too small, making it hard for RNNs to learn long-term dependencies.
# Long Short-Term Memory (LSTM)

To overcome RNN’s limitation, **LSTMs** were introduced.
It works by using a specialized memory cell and gating mechanisms to capture long-term dependencies in sequential data. Also selectively remembers or forget information over time.
It use **three gates** to control the flow of information.

![[Pasted image 20250813125914.png]]
## LSTM Gate Functions

|Gate|Role|
|---|---|
|**Input Gate**|Decides what new info to add to the memory.|
|**Forget Gate**|Decides what old info to discard.|
|**Output Gate**|Decides what info from memory to output at this step.|

## LSTM Workflow at Each Timestep

1. **Input vector** for current step.
2. **Previous hidden & cell states** are passed in.
3. **Gates filter** the information flow.
4. **Cell state** is updated based on new and retained info.
5. **Hidden state** is produced as output and passed to the next step.

![[Pasted image 20250813130248.png]]

# Where Are RNNs & LSTMs Used?

|Domain|Use Case|Model|
|---|---|---|
|NLP|Sentiment analysis, translation, chatbots|RNN, LSTM, Transformers|
|Audio|Speech-to-text, music generation|LSTM|
|Vision|Video captioning|LSTM + CNN|
|Time Series|Stock/weather prediction|LSTM|
# Why LSTMs Work Better than RNNs

RNNs tend to “forget” earlier parts of long sequences because each step depends heavily on the last. LSTMs mitigate this by **separating memory updates** and using gates to **decide what to remember and what to forget** — making them more robust for long text, extended conversations, or long-term trends in time series.

# ⚙️ What Comes Next?

- In modern sequence modeling, **transformers** (like those used in ChatGPT, BERT, etc.) have largely replaced RNNs and LSTMs due to better performance and parallel processing.    
- However, **LSTMs are still widely used**, especially in lightweight or embedded systems, where transformer models may be too large or resource-intensive.