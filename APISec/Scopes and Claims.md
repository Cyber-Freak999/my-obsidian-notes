# 🔐 **Scopes** – _What the app can do_

- **Define**: Permissions granted to the **client application**, not the user.    
- **Format**: Just strings like `user.invoice.read`, `video.stream`, etc.
- **Requested by**: The client during OAuth flow.
- **Approved by**: Authorization server (may involve user consent).
- **Purpose**: Coarse-grained _application-level_ access control.
   > e.g., Can this app _read_ invoices at all?
- **Example**:    
    - `user.invoice.read` → Can read invoices
    - `user.invoice.update` → Can update invoices

---

# 🧾 **Claims** – _Who the user is_

- **Define**: Actual data about the **user** (e.g., `sub`, `email`, `age`, `subscription_level`).    
- **Inserted by**: Authorization server into the token (JWT).
- **Purpose**: Fine-grained _user-level_ authorization and personalization.
    > e.g., Is this invoice actually **your** invoice?
- **Example Claims**:
    - `sub`: user ID
    - `age`: 42
    - `subscription_level`: "gold"
    - `subscriber_id`: "ABC123"        

---
# Access Token Claim 
- Can be the API for your API
- Single source of truth for your identity data
- Avoid external calls from the API
- Design a common identity API for your APIs.
- Can be differently depending om the scopes in the token.
# How to identify data put in the token
- It should be relevant to a large sets of APIs.
- It should be attributes of the user
- It should not be contextual for the session.
- It should not be application specific.

---

# 🏁 Flow Summary

1. **Client requests scopes** → Gets access token.    
2. **Token contains scopes + claims**.
3. **API checks**:
    - Does scope allow this operation?
    - Do claims prove the user owns the resource?

---
# Q/A
**Q: What are potential risks of putting too many claims in access tokens?**
A: Including an excessive number of claims in access tokens—especially **JWTs (JSON Web Tokens)**—can create several **security, performance, and maintainability** issues:
🔒 1. **Information Leakage**
- Sensitive data like `email`, `roles`, `department`, or `customer_id` may be exposed. 
- JWTs are **base64-encoded, not encrypted** by default—anyone with the token can decode and read it.
- Risks increase if tokens are leaked or logged unintentionally.

✅ **Mitigation**:  
Use _access tokens for authorization only_ and put sensitive identity info in **ID tokens** or fetch from a userinfo endpoint.  
Encrypt tokens if required (JWE).
 🐘 2. **Token Bloat**
Large tokens lead to:
- Increased **network overhead** (especially in HTTP headers).      
- **Longer request times**.  
- **Mobile clients** struggling with size constraints.     

✅ **Mitigation**:  
Only include **essential** claims. Use **reference tokens** with a token introspection endpoint when size is a concern.
🧠 3. **Stale or Inconsistent Data**
- Claims like `department`, `subscription_level`, or `role` may **change after token issuance**. 
- Access tokens are usually short-lived, but even a 5-minute window can allow misuse if roles or permissions change.

✅ **Mitigation**:  
Use **short expiry** and **revoke tokens** where necessary. For critical changes, design your system to support **claim refresh via introspection**.
🔁 4. **Coupling & Inflexibility**
- APIs relying heavily on certain claims become tightly coupled to the token structure.
- Changing claim formats or values might break clients or downstream services.

✅ **Mitigation**:  
Use **versioned tokens** or abstract claim logic into a centralized **identity/claims service**.
⚡ 5. **Authorization Logic in the Wrong Place**
- Claims might encourage overloading the token with logic (e.g., `can_edit_project: true`).
- This pushes decision-making into the token instead of **the resource server**, reducing flexibility and violating **principle of least privilege**.

✅ **Mitigation**:  
Use claims to inform decisions, **not make them directly**. Resource servers should evaluate claims **contextually**.

---
# Deep Dive
[[Scope and Claim Hierachy]]
