The **hierarchy between scopes and claims** is a foundational concept in token-based authentication and authorization systems like OAuth 2.0 and OpenID Connect. It determines **what data gets included in tokens** and **what permissions are granted**.

---

# 🧱 **Hierarchy Breakdown**

## 🔑 **Scopes → Unlock Claims**

- Scopes act as **keys** to enable specific sets of **claims** in the access or ID token.
    
- **Example (OIDC Standard Mapping)**:
    
    - Scope: `profile`  
        → Claims: `name`, `family_name`, `given_name`, `nickname`, `preferred_username`, `profile`, `picture`, `website`, `gender`, `birthdate`, `zoneinfo`, `locale`, `updated_at`
        
    - Scope: `email`  
        → Claims: `email`, `email_verified`
        
    - Scope: `address`  
        → Claim: `address`
        
    - Scope: `phone`  
        → Claims: `phone_number`, `phone_number_verified`
        

These mappings **aren’t one-to-one**; a single scope can authorize **multiple claims**.

---

## 🧩 **Scopes → Application Privileges**

- Define what **actions** the client can take.
    
- Example:
    
    - `invoice.read` → May unlock claims like `subscriber_id`, `cost_center`
        
    - `video.stream` → May unlock `age`, `subscription_level`
        

You can **custom-define scopes and their corresponding claims**.

---

##  📦 **Claims → Inform Authorization**

- Claims describe **user attributes or metadata**.
    
- Used to determine if a particular **action** should be permitted.
    
- Can be:
    
    - **Static**: `subscription_level = gold`
        
    - **Derived**: `is_admin = true` (from group membership or role)
        

---

# 🧠 Why Hierarchy Matters

| Layer     | Function                       | Controls                           |
| --------- | ------------------------------ | ---------------------------------- |
| **Scope** | Permission at app level        | What the **client app** can access |
| **Claim** | User-level context or identity | What the **user is allowed to do** |

---

# 🛠️ Custom Scope → Claim Mapping Example

```yaml
Scopes:
  - invoice.read
  - invoice.write
  - video.stream

Claim Mapping:
  invoice.read:
    - subscriber_id
    - cost_center
  invoice.write:
    - subscriber_id
    - cost_center
    - department
  video.stream:
    - age
    - subscription_level
```

When a client requests `invoice.read` + `video.stream`, the access token might include:

```json
{
  "scope": "invoice.read video.stream",
  "subscriber_id": "abc123",
  "cost_center": "gold-team",
  "age": 21,
  "subscription_level": "gold"
}
```

---

# 🧭 Visualization of the Hierarchy

```
Scope
 ├── invoice.read
 │    ├── subscriber_id
 │    └── cost_center
 ├── invoice.write
 │    ├── subscriber_id
 │    ├── cost_center
 │    └── department
 └── video.stream
      ├── age
      └── subscription_level
```

---

# 🔐 Best Practices

- **Use scopes for coarse-grained access** (e.g., access to modules or APIs).
    
- **Use claims for fine-grained access control** (e.g., user roles, tenant IDs).
    
- **Don't overload scopes with identity info** – put that in claims.
    
- **Design custom mappings** that align with your domain logic.
 