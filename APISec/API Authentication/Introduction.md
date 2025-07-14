# 🔐 **Authentication vs Authorization**

- **Authentication**: _Who_ is making the request (user or machine).    
- **Authorization**: _What_ the authenticated entity is allowed to do.
- ✅ You **must authenticate** before you can authorize.

---

# 📜 **Authentication Methods for APIs**

| Method                | Identity Type   | Key Traits                                                          |
| --------------------- | --------------- | ------------------------------------------------------------------- |
| **Basic Auth**        | User or machine | Username/password in Base64; insecure; not recommended              |
| **API Key**           | Machine         | Hardcoded key; minimal control; often used for throttling           |
| **Mutual TLS (mTLS)** | Machine         | Secure; certificate-based trust; complex to manage                  |
| **Token-based**       | User + Machine  | Uses signed tokens from an auth server; **flexible** and **secure** |

---

# 🎟️ **Token-Based Authentication**

- Uses **tokens issued by a trusted third party (Auth Server)**.    
- Supports:
    - Expiration
    - Audiences
    - Scopes and claims (for **authorization**)
- Tokens can be bearer tokens or sender-constrained (e.g., DPoP).

> 🔍 **Tokens ≠ Access**  
> A valid token does _not_ imply permission — the **API decides** based on scopes/claims.

---

# 🔁 **OAuth and OpenID Connect**

| Protocol           | Purpose                  | Notes                                    |
| ------------------ | ------------------------ | ---------------------------------------- |
| **OAuth 2.0**      | Delegated access to APIs | Secure, token-based, current standard    |
| **OpenID Connect** | Adds identity to OAuth   | Adds `ID Token`, federation support      |
| **OAuth 1.0**      | Legacy, signature-heavy  | Largely deprecated, complex to implement |
| **OAuth 2.1**      | Cleanup of OAuth 2.0     | Merges best practices, simplifies flows  |

---

### 🧠 Summary

- Use **token-based authentication** for modern APIs.
- Avoid basic auth and API keys where possible.
- OAuth is the **standard for securing API access** today.
- **TLS (HTTPS)** is mandatory when using OAuth 2.0.
- Authorization uses **scopes (app-level)** and **claims (user-level)** inside tokens.