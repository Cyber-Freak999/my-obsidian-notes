# **What Problem Are Transformers Solving?**

Traditional models like **Recurrent Neural Networks (RNNs)** struggle to understand long sentences or documents because they process words **one at a time**, maintaining memory only of recent words (via a "hidden state").

**Example Sentence**:

> "Jane threw the frisbee and her dog fetched it."

A human knows **“it” refers to “frisbee”**, but RNNs may forget or misinterpret because **“it”** is far from **“frisbee”** in the sequence.

## **Why RNNs Fall Short**

- RNNs process input **sequentially** (left to right, step by step).    
- They suffer from **vanishing gradients** – older context is lost as the sentence grows.
- They struggle with **long-range dependencies**, e.g. linking **“Jane”** and **“dog”** across several words.

![[Pasted image 20250816031116.png]]

# **Enter Transformers**

Transformers solve these issues by:
- **Looking at all words at the same time (parallel processing)**.
- Understanding the **relationships between all words** in a sentence, no matter how far apart they are.
- Having a **“bird’s-eye view”** of the entire sentence, not just one word at a time.

![[Pasted image 20250816031225.png]]
## **Key Innovation: Self-Attention Mechanism**

This is the heart of the transformer model.

> 🔑 **Self-attention** lets the model decide which words to "pay attention" to when processing a given word.

In our example:
- When processing **“it”**, the model weighs connections to all other words.
- It sees a strong connection to **“frisbee”**, helping it correctly resolve the meaning.
### How It Works:
- Every word compares itself with every other word in the sentence.
- These comparisons result in **attention weights**, determining **which words are most relevant** for understanding the current word.

This makes **context understanding** far more accurate than RNNs.

# **Transformer Architecture Overview**

Introduced in the landmark 2017 paper: ["Attention Is All You Need”](https://arxiv.org/abs/1706.03762).

It consists of two main components:
## **Encoder**
- Reads and encodes the input text into **contextual embeddings** (vectors).
- Understands the meaning and relationships within the input.    
## **Decoder**
- Takes the encoder’s output and **generates text** (e.g., a translation, summary, or completion).

Both modules:
- Use **multi-layer structures**.
- Rely heavily on **self-attention** to process context at each layer.

# **Transformer Model Types**

Transformers Have three main types:
1. **Encoder-only**: Used for understanding input (e.g., search, classification).
2. **Decoder-only**: Used for generating outputs (e.g., text, summaries).
3. **Encoder–Decoder (Seq2Seq)**: Used when you need to understand input _and_ generate corresponding output (e.g., translation).

##  **Use Cases by Model Type**

| Model Type          | Used For                | Example Tasks                                     |
| ------------------- | ----------------------- | ------------------------------------------------- |
| **Encoder-only**    | Understanding input     | Classification, semantic search                   |
| **Decoder-only**    | Generating new output   | Text generation, dialogue, writing                |
| **Encoder–Decoder** | Mapping input to output | Machine translation, summarization, Q&A with docs |

### **Encoder-Decoder Architecture**

Used in **sequence-to-sequence tasks** like machine translation.    
#### Flow:
1. Input sentence (e.g., English) → **encoder**
2. Encoder creates **embeddings** (numerical meaning vectors)
3. Embeddings go into **decoder**, which:
    - Generates **one word at a time**
    - Reuses previous output to predict the next word
    - Continues until full sentence is produced

---
# Other Key Concepts Introduced

## **Tokenization**

- Large Language Models (LLMs) process **tokens**, not words.
- A **token** can be:
    - A full word: `"apple"` → 1 token
    - A partial word: `"friendship"` → `"friend"` + `"ship"` = 2 tokens
    - Punctuation: `,`, `.`, `:` → each its own token 
- 🔎 **Token-per-word ratio**:
	- Simple text: ~1 token per word
	- Complex text: ~2–3 tokens per word
## **Embeddings**

- **Embeddings** = numerical (vector) representations of text
- Used to **encode meaning** of:
    - Words
    - Sentences
    - Entire documents

> Think of embeddings as how machines "understand" text semantically—not just the exact words, but their **context and meaning**.

## **Embeddings Power Semantic Search**

- **Vector databases** store embeddings of text for **fast similarity search**.
- This is foundational to **RAG (Retrieval-Augmented Generation)**.
### **How RAG works**:

1. Encode documents → store as vectors.
2. Encode user query → search for closest vectors (similar meaning).
3. Retrieve & send relevant content to LLM for **context-aware response**.

## **Decoder Models (Text Generators)**

- Take in a prompt (sequence of tokens).
- **Output: One token at a time**, based on probability distribution over the vocabulary.
- Repeat until end of sentence.

> Example: “They sent me a” → decoder outputs: “dog”  
> Then: “They sent me a dog” → decoder outputs next token, and so on.


---

### 🧾 **Why “It” Matters**

Words like "it" are called **anaphora** – they refer back to something earlier. Humans resolve this using **context**. Transformers do the same by dynamically assigning **attention scores** to earlier parts of the text.

### ⛓️ **Why RNNs Struggle with “Long-Term Memory”**

RNNs pass a memory state from word to word, but **this memory fades** as the chain grows longer. Imagine whispering a message down a long line—errors accumulate, and meaning is lost.

### 📊 **Why Transformers Are a Big Deal**

They:
- **Don’t rely on sequential processing**—which makes them fast and parallelizable.
- Can handle **much larger texts** without memory loss.
- Are foundational to all modern LLMs like GPT, BERT, T5, etc.

---

## ✅ **Summary**

- RNNs process word-by-word and struggle with long-range context.
- Transformers process **all words at once**, enabling deeper understanding.
- The **self-attention mechanism** helps link related words regardless of position.
- Transformer = **Encoder + Decoder**, each built from layers using self-attention.   
- This architecture powers modern **LLMs** and advanced **NLP applications**.
- **Tokens** and **embeddings** are the building blocks of how LLMs process language.
- **Encoders** turn input text into a meaningful numeric form.
- **Decoders** take that and generate fluent, coherent language.
- **Encoder-decoder models** combine both for tasks needing comprehension + generation (like translation).
- **RAG** architectures are powered by **embeddings**, enabling LLMs to pull in external knowledge on the fly.

