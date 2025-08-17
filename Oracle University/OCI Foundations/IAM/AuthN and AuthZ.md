**Principal**: Any IAM entity (user or resource) allowed to intereact with OCI Resources.
- **Users**: Real people using console, CLI, SDKs.
- **Resource Principals**: OCI resources like compute instances making API calls. 
**Groups**: Collections of users with similar access needs.

![[Pasted image 20250725131654.png]]
---

# ✅ **Authentication (AuthN)** – _"Are you who you say you are?"_

Used to verify identity. OCI supports three main types:

1. **Username/Password**    
    - Standard login to OCI console.
2. **API Signing Keys**    
    - Used for CLI/SDK.
    - RSA key pair (private + public).
    - Signs requests to prove identity.
3. **Auth Tokens**
    - Oracle-generated tokens.
    - Used when third-party tools don't support API signing (e.g., connecting to ADW from third-party clients).

---

# 🛂 **Authorization (AuthZ)** – _"What are you allowed to do?"_

Done using **IAM policies**, which are human-readable statements that grant permissions.

## 💡 **Policy Syntax**
![[Pasted image 20250725130619.png]]

- **Group**: Set of users (can’t assign policies to individual users).
- **Verb** (Permission level):
    - `manage`: Full control (create/update/delete).
    - `use`: Read and limited actions (e.g., start/stop).
    - `read`: View only.
    - `inspect`: Metadata only.
- **Resource-type**: What the group can access (e.g., `all-resources`, `compute-instances`).
- **Location**: `tenancy` or specific `compartment`.
![[Pasted image 20250725131544.png]]
## 📂 **Policy Scope**

- **Tenancy**: Global across all compartments.
- **Compartment**: Local to specific resources.

---

## 🧠 **Key Concepts Recap**

|Concept|Description|
|---|---|
|**Principal**|IAM entity (user or resource) that interacts with OCI.|
|**Authentication**|Confirms identity. Methods: password, API keys, auth tokens.|
|**Authorization**|Grants permissions via policies.|
|**Policy**|Human-readable statement that defines access.|
|**Group**|Set of users with shared access needs.|


