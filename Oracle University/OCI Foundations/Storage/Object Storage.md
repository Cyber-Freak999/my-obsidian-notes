# ✅ **What is [Object Storage](https://docs.oracle.com/en-us/iaas/Content/Object/home.htm)?**

- **Internet-scale**, **high-performance**, **regional** object storage service
- Ideal for **unstructured data** (logs, images, videos, backups)
- Public by default, but can be **privately accessed** by OCI resources (e.g. Compute)
# 🔑 **Key Concepts**

|Term|Description|
|---|---|
|**Object**|Fundamental unit of storage (key = name, value = data)|
|**Bucket**|Container that holds objects, uniquely named within a tenancy|
|**Namespace**|Top-level container (globally unique per tenancy)|
|**Flat hierarchy**|All objects exist in one level; folder structure is simulated using _prefixes_|

---

## 🌐 **Accessing Object Storage**

- Public API endpoint format:`https://objectstorage.<region>.oraclecloud.com/n/<namespace>/b/<bucket>/o/<object>`
- Access via:    
    - **HTTP verbs**: `PUT`, `GET`, `DELETE`, etc.
    - CLI, SDK, REST API
![[Pasted image 20250731180012.png]]

---

## 🧊 **Storage Tiers**

| Tier                                                                       |Use Case|Key Features|Limitations|Cost|
| -------------------------------------------------------------------------- | ---------------------------------------------- | ---------------------------------- | ----------------------------------------------------------------------- | --------------- |
| **Standard (Hot)**                                                         |Frequently accessed critical data|Instant access, strong consistency|None|💲 Full cost|
| **Infrequent Access**                                                      |Long-term, less-accessed critical data|60% cheaper, strong consistency|31-day minimum retention, retrieval fee|💲💲 Lower|
| **[Archive](https://docs.oracle.com/en-us/iaas/Content/Archive/home.htm)** |Rarely accessed (e.g., compliance/tape backup)|Ultra-low cost, long retention|90-day minimum retention, **restore required** before access (1–40 hrs)|💲💲💲 Cheapest|

---

## 🔄 **Auto-Tiering**

- Monitors access patterns and **automatically moves objects** between **Standard ↔ Infrequent Access**
- ✅ No retrieval fee
- ✅ No prorated storage charges
- 🔽 **Reduces cost dynamically**

---

## 🔧 **Key Features**

| Feature                         | Description                                                                                |
| ------------------------------- | ------------------------------------------------------------------------------------------ |
| **Object Lifecycle Management** | Automate transitions and deletions (e.g., move to Archive after 30 days, delete after 180) |
| **Versioning**                  | Enable versioning at bucket level to retain multiple versions of objects                   |
| **Encryption**                  | Always-on encryption at rest (OCI-managed or **BYOK** – bring your own key)                |
| **Event Triggers**              | Can integrate with **Oracle Events**, **Functions**, or **Notifications** for automation   |

---

## 📌 **Typical Use Cases**

- Application logs and audit trails
- Web assets and static websites
- Big data lake
- Media storage (photos, videos, documents)
- Backup and disaster recovery
- Compliance and cold archival storage