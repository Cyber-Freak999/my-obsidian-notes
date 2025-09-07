
# What is a GPU and Why It Matters for AI

- **GPU (Graphics Processing Unit)** is essential for **AI and ML workloads** due to its ability to handle **massive parallel computations**.
- Unlike CPUs (fewer, more powerful cores), GPUs have **thousands of lightweight cores**, making them ideal for:
    - **Training deep learning models**
    - **Running high-throughput inference**
    - **Processing large datasets**
# Key Advantages of GPUs in AI

- **Parallelism:** Thousands of cores handle operations simultaneously.    
- **High Throughput:** Suitable for batch inference or serving many users at once.
- **Framework Support:** Optimized for TensorFlow, PyTorch, ONNX via GPU-specific libraries (like cuDNN, CUDA).
- **Performance Gains:** Especially crucial for compute-intensive tasks like LLM training.
# Evolution of NVIDIA AI GPUs

![[Pasted image 20250822154417.png]]
# OCI's GPU Compute Infrastructure

Oracle Cloud Infrastructure (OCI) offers a **broad GPU portfolio** for varying AI workloads:

- **Available Now:**
    - L40 GPU
    - H100 (standard)
    - H100N (10,800-core)
- **Coming in 2025:**
    - H200 and B200 GPU instances
    - GB200 (Grace + Blackwell) superchips
    - Superclusters built with H200, B200, GB200

> **Superclusters**: Massive multi-GPU clusters optimized for **LLM training** and **AI at scale**.

![[Pasted image 20250822154513.png]]
# Using OCI Data Science with GPU Compute

You can access OCI’s GPU power via **OCI Data Science** using **AI Quick Actions**:
- **Direct Deployment:** Run popular open-source LLMs on GPU-backed VMs or bare metal.
- **Fine-Tuning + Inference:**
    - Fine-tune base models.
    - Deploy for real-time inference using virtual LLM or text-embedding containers.
- **Model Support:** Compatible with models using OCI’s **Virtual LLM**, **Next-Gen Inference**, and **Text Embedding** containers.

![[Pasted image 20250822154331.png]]