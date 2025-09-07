# What is OCI AI Services?

Oracle Cloud Infrastructure (OCI) AI Services is a **suite of cloud-based, prebuilt AI/ML tools** that help businesses integrate artificial intelligence into applications without needing deep data science expertise. These services are **fully managed**, require **no infrastructure management**, and support **customization using your own data**.
## Concepts in OCI AI Services

- **Layered Stack Approach:** 
    - Starts with **data and infrastructure**.
    - AI services are built **on top of data** and consumed by **applications**.
    - Aligns with Oracle’s full-stack enterprise vision.
![[Pasted image 20250820162835.png]]
![[Pasted image 20250820163003.png]]
- **Access Methods:**
    - **OCI Console:** Ease-to-use, browser-based interface.
    - **REST APIs:** Provides access to functionality; requires expertise.
    - **SDKs** (Java, Python, JS, .NET, Go, Ruby and Javascript/Typescript).
    - **CLI** (command-line interface for full control without coding).
# Core OCI AI Services

## **Language**

- **Purpose:** Text processing and NLP tasks at scale.
- **Pretrained capabilities:**
    - Sentiment analysis
    - Language detection
    - Key phrase extraction
    - Named Entity Recognition (NER)
    - Text classification
    - PII detection
- **Custom models:** Train your own NER or classification models on domain-specific data.
- **Translation:** Neural machine translation across multiple languages.
## **Vision**

- **Purpose:** Image analysis, classification, and object detection.
- **Image Analysis Pretrained models:** Image classification, object detection, OCR (text in images).
- **Image Analysis Custom models:**
    - Custom object detection (with bounding boxes).
    - Custom image classification (for your own image categories).
## **Speech**

- **Purpose:** Transcribes human speech in media files to text.
- **Output formats:** JSON, SRT.
- **Use cases:** Meeting transcription, customer service calls, subtitles.
![[Pasted image 20250820164124.png]]
## **Document Understanding**

- **Purpose:** Automates extraction and classification of document content.
- **Features:**
    - Text extraction (with bounding boxes).
    - Key-value extraction (e.g., from receipts, IDs, invoices).
    - Table extraction (preserves row/column structure).
    - Document classification (e.g., distinguishing invoices vs. passports).

## **Digital Assistant**

- **Purpose:** Build conversational AI bots (chatbots).
- **Capabilities:**
    - Understands and routes user queries to appropriate tasks or “skills.”
    - Handles conversational context, interruptions, and exit requests.
    - Supports natural language interfaces across applications.