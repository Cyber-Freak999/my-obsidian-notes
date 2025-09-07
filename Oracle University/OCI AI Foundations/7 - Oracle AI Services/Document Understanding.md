# OCI Vision – Document AI

**Document AI** in Oracle Cloud Infrastructure (OCI) Vision is designed for processing and understanding **scanned documents and document images**. It enables organizations to **automate document workflows** by extracting structured data from semi-structured or unstructured documents.
It supports formats such as **PDF**, **JPEG**, **PNG**, and **TIFF**, including **photographs** of documents.
##  Key Features of Document AI

 1. **Text Recognition (OCR)**	
	- Uses **Optical Character Recognition** to extract text from images.	    
	- Handles complex scenarios:	    
	    - **Handwritten text**	        
	    - **Tilted, rotated**, or **shaded** documents	        
	- Converts unstructured visual content into machine-readable text.	   
 2. **Document Classification**
	- Automatically classifies documents into **10 predefined categories** using:	    
	    - **Visual layout**	        
	    - **Extracted keywords**	        
	    - **High-level structural features**	        
	- Example document types:	    
	    - Invoice	        
	    - Receipt	        
	    - Resume	        
	    - ID documents	        
	- Helps route or process documents based on type (e.g., send invoices to Accounts Payable).	
 3. **Language Detection**
	- Analyses **visual features** of the text (rather than relying solely on content) to detect language.    
	- Useful for multilingual document processing pipelines.    
 4.  **Table Extraction**
	- Detects and extracts **tabular data** from documents.
	- Outputs rows and columns in a **structured table format**.	    
	- Enables easier processing of financial forms, spreadsheets, etc.
 5. **Key-Value Pair Extraction**
	- Extracts values from **13 commonly found fields** in documents like **receipts**.
	- Example fields:	    
	    - Merchant name	        
	    - Transaction date	        
	    - Total amount	        
	    - Tax	        
	- Also extracts **line items**, providing detailed breakdowns.
# 🧠 Typical Use Cases

- Automating invoice or receipt processing    
- Digitizing handwritten notes or forms    
- Extracting resumes into HR systems
- Scanning and processing multi-language documents    
- Creating structured datasets from PDFs or scanned reports    