# **What Is the Phantom Token Flow?**
A security pattern used when:

- **Clients use opaque tokens** externally.
- **Gateways perform introspection** and receive **JSON** or **JWTs**.
- The **goal** is to forward a **signed JWT** (phantom token) internally to the API, _not raw JSON_.

---

# 🔁 **Why Use It?**

1. **⚖️ Audit Trail Integrity**    
    - JWTs are **cryptographically signed** → verifiable.        
    - Ensures tokens are **issued**, not faked.        
    - Preserves **who**, **when**, **what scopes/claims** all the way to the API.        
2. **🔐 Prevent Internal Forgery**    
    - Anyone could fabricate JSON and trick internal APIs.        
    - A signed JWT **cannot be forged** internally or externally.        
3. **🧱 Supports Zero Trust**
    - Ensures APIs only act on **authentic tokens**.        
    - Internal network is treated as **untrusted**.        

---

# 🔧 **How It Works**

1. **Client** → sends **opaque token** to **gateway**.    
2. **Gateway** → calls **AS introspection or token exchange**.    
3. **Auth Server** → returns a **signed JWT** (the "phantom").    
4. **Gateway** → forwards JWT to API in `Authorization: Bearer <JWT>`.    

---

# ✳️ Benefits

- Uniform **token validation logic** across all APIs.    
- JWT is **auditable**, inspectable, and verifiable.    
- API doesn’t need to trust the gateway—**only the JWT**.    
- Prevents internal spoofing or unauthorized token reuse.    
