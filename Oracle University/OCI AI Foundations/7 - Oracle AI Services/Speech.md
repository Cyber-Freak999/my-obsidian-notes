# OCI Speech

**OCI Speech** is a fully managed service that uses **advanced deep learning models** to automatically convert **speech into text**, unlocking valuable data from audio and video sources.
##  Key Features
1. **Speech-to-Text Transcription**
	- Automatically transcribes **audio and video** into **timestamped**, grammatically correct **text**.    
	- Uses **Oracle’s acoustic language models** for high accuracy.
	- **No data science expertise required**.
2. **Language Support**
	- Currently supports:    
	    - **English**
	    - **Spanish**
	    - **Portuguese**
	- More languages planned for future releases.
3. **Batch Processing**
	
	- Supports submitting **multiple audio files** in a **single API call**.	    
	- **Fast transcription**: Can transcribe **hours of audio in under 10 minutes**.	    
	- Works by:	    
	    - **Chunking** large audio into segments.	        
	    - Transcribing in parallel.	        
	    - **Reassembling** into one final output file.	        
4. **Accuracy & Confidence Scoring**
	- Assigns a **confidence score**:	    
	    - **Per word**	        
	    - **Per entire transcription**	        
	- Helps determine how reliable the results are.	    
5. **Automatic Punctuation**
	- Makes text **easier to read** and more suitable for downstream applications.
6. **SRT (Closed Caption) Support**
	- Generates **SRT files** (SubRip Subtitle format).    
	- Ideal for adding **closed captions** to videos.
7. **Normalization**	
	- Converts transcribed content into **human-friendly text** formats:
	    - Words to **numerical values** (e.g., “twenty-three” → “23”)
	    - Normalizes **addresses, times, URLs**, and **numbers**.
	- Ensures output matches how humans **read and write**.
8. **Profanity Filtering**
	- Provides **three levels of filtering**:
	    - **Remove** – replaces offensive words with asterisks (e.g., `****`)
	    - **Mask** – keeps the first letter and masks the rest (e.g., `s***`)
	    - **Tag** – keeps the word and **flags it** in output metadata
#  How It Helps

- Extracts **searchable, analyzable** data from calls, meetings, podcasts, videos, etc.    
- Enables:
    - **Closed captioning**
    - **Voice-driven workflows**
    - **Audio archive indexing**
    - **Voice-of-customer analytics**