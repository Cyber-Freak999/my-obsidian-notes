# **What is OCI File Storage Service (FSS)?**

OCI File Storage Service is a **scalable, distributed, and managed file system** that provides **shared file storage** for compute instances in OCI. It is **POSIX-compliant**, which means it behaves like traditional file systems you're used to on Linux or UNIX environments.

## 🔑 **Key Features of OCI File Storage**

|Feature|Description|
|---|---|
|**NFS v3 support**|Standard for UNIX/Linux environments; allows seamless integration|
|**Shared access**|Multiple compute instances (within a VCN) can **mount the same file system** simultaneously|
|**Scalable**|Scales automatically to meet performance and capacity needs without provisioning|
|**Snapshots**|Point-in-time, space-efficient backups for recovery or versioning|
|**Durability**|Data is replicated across multiple fault domains in an Availability Domain|
|**Security**|Data-at-rest and in-transit encryption, with optional **IAM-based access control**|
|**Backup**|Integration with **OCI Backup service** to protect file systems from accidental deletion/data loss|
# 📁 **Typical Use Cases**

1. **Enterprise Applications** (e.g., Oracle E-Business Suite, PeopleSoft)
    - Require shared storage between multiple compute nodes.
2. **Home Directories / User Folders**
    - Shared directories in an enterprise for collaborative access.
3. **Microservices and Containers**
    - Use a shared filesystem to **store session state, configs, or logs**.
4. **HPC (High Performance Computing)**
    - File storage is suitable for storing large datasets accessed by many compute nodes.
5. **Analytics and Big Data Workloads**
    - For shared data access across clusters or data pipelines.

# How It Works:

- Compute instances in an OCI availability domain mount the **same filesystem**.
- Data is read/written by all clients sharing the mount.
- Operates using **NFSv3** (for Linux/Unix).
- File system is **regionally resilient**, built in a single data center (availability domain).

# 🧠 **Advanced Capabilities**

## 🔄 **Snapshots**

- Can be taken manually or scheduled.    
- Stored within the same region.
- Used for:
    - **Data protection**
    - **Versioning**
    - **Restoration of deleted files or folders**
## 🔐 **Security and Access Control**

- **Encryption at Rest**: Always-on, using OCI Vault keys or your own customer-managed keys (CMK).    
- **Encryption in Transit**: NFS protocol secured using **TLS tunneling** (client-side).    
- **IAM Integration**: Apply access control at the **API level**, not at the file level (use OS-level permissions for that).
## 📏 **Performance and Scaling**

- **Elastic Performance**: Automatically adjusts based on throughput and IOPS demand.  
- No need to provision IOPS or throughput manually.
- Supports **high concurrency** and is **ideal for distributed workloads**.

# 💡 **Best Practices**

|Category|Best Practice|
|---|---|
|**Security**|Use network security groups (NSGs) to restrict access to mount targets.|
|**Backup**|Use snapshots regularly and integrate with Object Storage for long-term archival.|
|**Performance**|For performance-sensitive workloads, spread IO across multiple compute nodes and mount targets.|
|**Monitoring**|Use OCI Monitoring and Logging to track performance and access behavior.|

---

## 🧭 Comparison with Other Storage Types

| Feature   | File Storage                  | Block Volume      | Object Storage            |
| --------- | ----------------------------- | ----------------- | ------------------------- |
| Interface | NFS (POSIX)                   | iSCSI             | HTTP(S)                   |
| Use Case  | Shared access to files        | OS disks, DBs     | Static files, media, logs |
| Structure | Files & folders(hierarchical) | Fixed-size blocks | Key-value pairs (objects) |
| Mounting  | Network file mount            | Local disk mount  | Access via API/CLI/UI     |

![[Pasted image 20250801102930.png]]