## 🔐 **Why Use API Gateways?**

- Act as **Layer 7 firewalls**: inspect, block, or forward HTTP requests.    
- Provide a **central access point** to internal APIs.    
- Prevent direct internet access to backend services.    
- Support **OAuth token validation** before reaching APIs.    

---

# 📦 **Token Introspection & Phantom Token Flow**

- Gateways receive **opaque (reference) tokens** from external clients.    
- They introspect these by calling the **authorization server**.    
- Instead of forwarding raw JSON to APIs, gateways get back a **JWT** (by-value token) and forward that.

✅ **Phantom Token Flow**:

- External token = opaque    
- Internal token = signed JWT    
- Preserves **audit trail**, **zero trust**, and **trust boundaries**

---
# API Dependency on JWTs
- Accept no requests without JWTS
- Verify issuer audience, validity, scopes and claims
- Uniform security model internally
- Easy re-use of validation logic
- Zero-trust enabled
- Identity data is kept and can be trusted at API level
---
# Introspection
![[Pasted image 20250618155626.png]]
![[Pasted image 20250618155634.png]]
![[Pasted image 20250618155654.png]]
 ## 🔄 **Gateway-to-AS Token Exchange Options**
- **Introspection + Accept Header** (`Accept: application/jwt`)    
- **JWT inside JSON** response
- **Token Exchange (RFC 8693)**: swap token format or scopes
---
# How we communicate this tokens to the next API
When APIs need to call other APIs:
- **Exchange**: Call AS to get a **reduced** token (fewer scopes/claims).
- **Embed**: Original token contains **nested tokens** for downstream APIs.
- **Share**: Just **reuse the token** if both APIs are in the **same security domain**.
![[Pasted image 20250618155853.png]]
![[Pasted image 20250618155900.png]]
![[Pasted image 20250618155916.png]]
![[Pasted image 20250618155924.png]]

---
# API Authorisation
## 🔹**Gateway = Coarse-Grained Authorization**
The **API Gateway** is your **first line of defense** and handles **basic filtering**:
- **Checks scopes** to determine _which API_ the request is intended for.    
- Acts as a **traffic cop**, routing based on high-level access like:
    - `invoice_read`        
    - `video_stream`        
- Does **not validate claims or enforce user-specific permissions**.
- Ensures the token has _a possibility_ to succeed.

> Example:  
> If calling `/invoices/123`, the gateway checks if the token has any `invoice_*` scope before routing to the Invoice API.
## 🔸**API = Fine-Grained Authorization**

The **actual API** enforces **precise access control**:

- **Validates scopes** relevant to the endpoint (`invoice_read` for `GET /invoices/123`)
    
- **Evaluates claims** like:
    - `subscriber_id`
    - `cost_center`
- Optionally integrates with **external policy engines** (e.g., OPA) for **Attribute-Based Access Control (ABAC)**.

> Example:  
> After passing the gateway, the API checks:

- Is the scope `invoice_read` present?
- Does `subscriber_id` in the token match the requested invoice?
## 🔁 **Scoping Strategy**

Organize your scopes around **API domains**:

|Domain|Sample Scopes|
|---|---|
|Invoicing|`invoice_read`, `invoice_write`|
|Streaming|`video_stream`, `video_metadata`|
|Provisioning|`device_read`, `device_update`|
|Content Mgmt|`content_publish`, `content_edit`|

- Use **naming conventions** (e.g., `invoice_read`) to structure scope hierarchy.
- **Tip**: Avoid "scope explosion" by grouping related actions and adopting a consistent format.
- Use gateways to **filter directionally** (e.g., invoicing vs streaming), and APIs to check **precise access logic** (e.g., subscriber ID matches resource).

---
# 🧠 **Best Practices**

- Design **hierarchical scopes**: e.g., `invoice_read`, `invoice_write`
- Prevent **scope explosion** by grouping by domain or feature
- Use **JWTs behind the firewall** for uniform validation logic
- Share tokens only within trusted boundaries
- Use **token exchange or embedded tokens** when crossing domains
---
# Q/A
## Q: What are the operational trade-offs between using introspection + JWT vs token exchange in the phantom token flow?**
Both methods aim to convert an **opaque token** (external) into a **signed JWT** (internal) for forwarding to APIs. However, they differ significantly in how they're implemented, how flexible they are, and the operational overhead they introduce.
### 🔹 **Option 1: Introspection with JWT Accept Header**

> The gateway calls the `/introspect` endpoint with `Accept: application/jwt`  
> The auth server replies with a **JWT instead of raw JSON**.

 ✅ Pros
- **Simple** and fast: Extends the familiar introspection pattern.
- **Low complexity**: No need to support additional grant types or flows.   
- **Token identity is preserved**: JWT mirrors the original opaque token's properties.  
 ❌ Cons
- **Requires custom content negotiation**: Not all AS implementations support `application/jwt`.    
- **Less flexible**: Cannot tailor scopes, audiences, or claims dynamically.
- **Not a standard fallback**: Might not be compatible across providers.

### 🔹 **Option 2: Token Exchange (RFC 8693)**

> The gateway uses `grant_type=token-exchange` to request a **new JWT** from the opaque token.

 ✅ Pros
 - **Highly flexible**:
    - Change `audience`
    - Reduce `scope`
    - Add/remove `claims`
- **Decouples internal and external token logic**: You get a **clean internal token contract**.    
- **Standardized spec** (RFC 8693): Supported by some identity platforms.
 ❌ Cons
- **Higher complexity**:
    - Requires support for **token exchange** grant
    - Extra configuration of clients, scopes, policies
- **May issue entirely new tokens**, not “representations” → affects auditing if not handled properly.
- **More moving parts**: More logic in the AS; greater risk of misconfiguration
## ⚖️ Comparison Table

|Feature|**Introspection + JWT**|**Token Exchange**|
|---|---|---|
|Complexity|🔹 Low|🔸 Moderate to High|
|Flexibility (aud, scope, etc.)|❌ Limited|✅ High|
|Token preservation|✅ Same as original token|❌ Often issues a new token|
|Standards compliance|🟡 Non-standard behavior|✅ Fully RFC 8693 compliant|
|Performance|✅ One call, fast|🔸 Extra processing overhead|
|Use case fit|🔹 Simple passthrough flows|✅ Cross-domain, API chaining|

### 🔁 When to Use Which?

|Scenario|Recommended Method|
|---|---|
|Simple internal JWT forwarding|**Introspection + Accept: JWT**|
|Need custom scopes/claims/audience|**Token Exchange**|
|Multi-tenant or delegated access|**Token Exchange**|
|Legacy AS with no token exchange|**Introspection + JWT**|

---
# Deep Dive
[[Introspection with token exchange for APIs and Gateways]]
[[Phantom Token]]
