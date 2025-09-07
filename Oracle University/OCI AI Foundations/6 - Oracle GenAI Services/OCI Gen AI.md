# [**OCI Generative AI Service: Overview**](https://docs.oracle.com/en-us/iaas/Content/generative-ai/overview.htm)

Oracle Cloud Infrastructure (OCI) Generative AI Service is a **fully managed, serverless platform** that gives access to customizable **large language models (LLMs)** via a **single API**. It enables developers to build powerful GenAI applications **without managing infrastructure**.
#  Key Characteristics

1. **[Pre-trained Foundational Models](https://docs.oracle.com/en-us/iaas/Content/generative-ai/pretrained-models.htm#pretrained-models)**    
    - Ready-to-use models from **Meta** (LLaMA 3) and **Cohere** (Command-R series).
    - Includes **chat** and **embedding** models.
    - **Single API access** supports seamless switching between models with minimal code change.
2. **[Flexible Fine-Tuning](https://docs.oracle.com/en-us/iaas/Content/generative-ai/create-new-model.htm#create-new-model)**
    - Customize foundational models using **your own domain-specific data**.
    - Supports **T-Few Fine-Tuning**:
        - Efficient training by updating only parts of the model.
        - Reduces cost and time compared to full fine-tuning.
3. **[Dedicated AI Clusters](https://docs.oracle.com/en-us/iaas/Content/generative-ai/create-ai-cluster-hosting.htm#create-ai-cluster-hosting)**
    - GPU-powered compute infrastructure for fine-tuning and inference.
    - Uses **RDMA-based high-speed networking** for ultra-low latency.
    - Ensures **resource isolation and security**.
# [Types of Pre-trained Foundational Models](https://docs.oracle.com/en-us/iaas/Content/generative-ai/pretrained-models.htm)

## [**Chat Models**](https://docs.oracle.com/en-us/iaas/Content/generative-ai/use-playground-chat.htm#chat) (Instruction-tuned for dialogue & generation)

| Model                 | Provider | Max Token Limit | Use Case                                      |
| --------------------- | -------- | --------------- | --------------------------------------------- |
| `command-r-16k`       | Cohere   | up to 16,000    | General chat, affordable                      |
| `command-r-plus`      | Cohere   | up to 128,000   | High-end tasks, more powerful, more expensive |
| `llama3-70b-instruct` | Meta     | -               | Advanced instruction following                |

- Maintains **context across messages**.
- Get conversational responses.
- Ideal for **Q&A, content generation, summarization**, etc.
## [**Embedding Models**](https://docs.oracle.com/en-us/iaas/Content/generative-ai/use-playground-embed.htm#playground-embed) (For search & semantic tasks)

| Model                    | Languages      | Use Case                                                  |
| ------------------------ | -------------- | --------------------------------------------------------- |
| `embed-english-v30`      | English only   | English-based search, clustering                          |
| `embed-multilingual-v30` | 100+ languages | Cross-lingual search (e.g., Chinese query on French docs) |

- Converts text → **vector representation**.
- Supports **semantic search**, **recommendations**, **text clustering**, etc.
# Fine-Tuning (Customisation)

- Fine-tuning = Adapt a pre-trained model with custom data.
	- Improves model performance on specific tasks.
	- Improve model efficiency.
- Use when:
    - Pre-trained models underperform on specific tasks.
    - You need the model to learn new behavior or terminology.
- **T-Few fine-tuning(Cohere)**:
    - Inserts new layers, updates only selective weights.
    - Saves **training cost** and **time**.
# **Dedicated AI Clusters**

- GPUs based compute resources that hold customers' fine-tuning and inference workloads, isolated for security and performance.
- Connected via **RDMA cluster network** for **low-latency, high-bandwidth** communication.