**Tokens** can be categorized by:

## Format – _How they're encoded and validated_
- **By Value (Self-contained):**
	- All data is _inside_ the token.
    - Validated _without_ calling auth server.
    - Examples: **JWT**, **SAML**, **CWT**.   
- **By Reference:**
    - Just a random string (opaque).    
    - Must query the **authorization server** to read it.
    - More privacy-preserving.

## Purpose – _Who it's for_
- **Access Token** → sent to **resource server** (API). 
- **Refresh Token** → sent _only_ to **authorization server**, used to get new tokens.
- **ID Token** → for the **client** in OpenID Connect. Never leaves the client.
## Type – _How it’s used/transmitted_
- **Bearer Token**:
    - Like cash—whoever holds it can use it.
    - Must be kept secret (TLS required).
    - Most common.
- **Proof of Possession (PoP)**:
    - Like a credit card + PIN.
    - Requires proof of private key ownership.
    - More secure (e.g., **DPoP**, **Mutual TLS**).
    - **Sender-constrained** tokens.        

# JSON Web Tokens (JWTs)
- **Format only**, not a protocol or purpose. 
- Composed of:
    - `header` – includes alg, kid/x5t
    - `payload` – claims like sub, aud, scopes
    - `signature` – integrity check
- Types:
    - **JWS** – JSON Web Signed
	    - proves who  issued the token
	    - The prominent way of JWTs
	    - Asymmetric signatures.
	    - Always whitelist algorithms allowed
    - **JWE** – JSON Encrypted
- Validate:
    - Signature ✅
    - Claims (exp, aud, iss, etc.) ✅
    - **Whitelist algorithms**, never accept `alg: none`.

# ⚠️ Best Practices

- Clients **shouldn’t** inspect or parse access tokens (even JWTs).    
- Treat tokens as opaque; only the **intended audience** should parse.
- JWT ≠ Secure by default — **protocol adherence** ensures security.
- **Don’t assume structure** (length, characters, etc.).
- Follow the contract between the **auth server** and **resource server**.    
# Q/A
## Why should clients avoid parsing JWT access tokens directly?
Clients should treat access tokens as opaque for several reasons:
- **Format abstraction**: If the auth server changes the token structure or format (e.g., switching from JWT to opaque), clients parsing them will break.
    
- **Security boundaries**: The token content is meant for the **resource server**, not the client. Interpreting it breaks the separation of concerns.
    
- **Versioning headaches**: Any schema change in the token payload might require client updates, which is especially painful in mobile apps or distributed systems.
    
- **Misuse risk**: Clients might make authorization decisions based on token content, which should only be validated by the resource server.

## How do sender-constrained tokens like DPoP enhance security over bearer tokens?
Sender-constrained tokens (like DPoP or Mutual TLS) bind the token to a specific client by requiring proof of possession of a private key. This means even if the token is stolen (e.g., via logging or interception), an attacker _cannot use it_ without also possessing the private key. In contrast, **bearer tokens** can be used by anyone who obtains them—like cash—making them more vulnerable to theft and misuse. DPoP also adds an extra header (`DPoP`) with a signed JWT for every request, proving sender identity for each use.

# Deep Dive
[[Demonstration of Proof-of-Possession]]