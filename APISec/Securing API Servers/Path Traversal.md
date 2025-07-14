# Path Traversal Vulnerabilities 

**What it is:**  
A path traversal vulnerability lets attackers access files or directories on a server that they shouldn't be able to see — either outside the web root or sensitive files inside it (e.g., `/etc/passwd`).

**How it happens:**

- When user input (like cookies or URL params) is directly used in file paths without proper validation or sanitization.
    
- When server configs allow directory listing or file inclusion outside the intended directories.
    
- Loose API specs that accept unrestricted strings allow malicious inputs through.
    

**Common examples:**

- Using `../` sequences to navigate to parent directories and access sensitive files.
    
- Dynamically including files based on untrusted input without validating the input.
    

**Why it's dangerous:**  
Attackers can retrieve sensitive files or information, potentially leading to further exploitation.

**How to prevent it:**

- Validate and sanitize all user inputs rigorously (e.g., whitelist allowed filenames or IDs instead of accepting raw paths).
    
- Disable directory listings on the web server.
    
- Restrict file access strictly to within the web root.
    
- Remove sensitive files from the web root entirely.
    
- Use strict API specs that limit input types and lengths.
    
- Prefer using IDs or keys that map internally to file paths instead of directly accepting paths.
    
- Log and error out on unexpected or suspicious input.
    
- Regularly test with automated tools and static analysis to catch these vulnerabilities.