**OCI Vision** is Oracle’s **AI-powered computer vision service** that analyses images and documents using **pretrained or custom models**. It provides deep visual understanding for a variety of use cases, with **no machine learning expertise required**.
# Core Capabilities

## **Image Analysis**

Analyses **photographic images** and detects visual elements.
1. **Object Detection**
	- Locates **individual objects** within an image.	    
	- Draws **bounding boxes** around detected items.	    
	- Assigns a **label** (e.g., “car,” “tree”) and a **confidence score**.	    
	- Also supports **scene text detection** – extracts readable text embedded in the image (e.g., road signs, store names).	    
 2. **Image Classification**
	- Assigns one or more **classification labels** to an image.	    
	- Labels represent **dominant themes or objects** (e.g., “beach,” “cat,” “sunset”).	    
	- Great for categorizing images at scale.    
## **Document AI(more in [[Document Understanding]])**
- Extracts **structured data** from documents like invoices, receipts, and forms.    
- Detects fields such as **invoice numbers, dates, totals**, etc.    
- Useful for automating data entry and processing of business documents.    
# Custom Model Training

- One of OCI Vision's most powerful features:    
    - You can **retrain the pretrained models** with your **own labeled image data**.
    - Enables building **domain-specific models** tailored to your business (e.g., detecting manufacturing defects, custom products, or brand logos).
- Supports **automated model training pipelines** with minimal setup.
# Use Cases

- Retail: Product tagging and inventory detection.    
- Manufacturing: Visual inspection and defect detection.
- Logistics: Barcode and label reading.
- Smart Cities: Traffic sign and object detection.
- Healthcare: Medical image classification (with proper domain-specific data).
- Document processing: Automated extraction of data from physical forms.