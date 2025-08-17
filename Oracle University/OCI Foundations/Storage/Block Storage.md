# 🧱 **[OCI Block Volume](https://docs.oracle.com/en-us/iaas/Content/Block/home.htm) – Overview**

- **Persistent, durable block storage** attached to OCI compute instances    
- Data **persists independently** of instance lifecycle (compute can be deleted, data remains)    
- Stored on **network-attached disks** managed by Oracle

# 🔐 **Key Features**

|Feature|Description|
|---|---|
|**Persistence**|Data remains even after the compute instance is terminated|
|**Durability**|Multiple redundant copies stored in data center for protection|
|**Encryption at Rest & In Transit**|Always-on encryption (default), BYOK supported|
|**Read/Write Sharing**|Multiple instances can **share a single block volume**|
|**Volume Resizing**|Online (live) or offline resizing supported|
|**Volume Replication**|Asynchronous replication to another region for DR/migration|
|**Volume Groups**|Group volumes to perform **time-consistent backups** across multiple disks/instances|

# 📊 **Block Volume Performance Tiers**

|Tier|Use Case|Performance|IOPS/GB|
|---|---|---|---|
|**Lower Cost**|Large, sequential I/O (e.g., data warehouses)|Moderate|~2 IOPS/GB|
|**Balanced**|General workloads, boot volumes|Balanced|~60 IOPS/GB|
|**High Performance**|I/O-intensive apps|High|~75 IOPS/GB|
|**Ultra High Performance**|Enterprise DBs, OLTP workloads|Highest|Up to 225 IOPS/GB|

# ⚙️ **Performance Optimization: Auto-Tune**

- Automatically reduces performance tier (to **lower cost**) **when detached**
- Restores original performance **when reattached**
- ✅ Saves costs for infrequently used volumes

# 🔁 **Replication & Recovery**

| Feature                                                                       | Use Case                                         | Details                                              |
| ----------------------------------------------------------------------------- | ------------------------------------------------ | ---------------------------------------------------- |
| **[[Cross-Region Replication and Volume Groups\| Cross-Region Replication]]** | Disaster recovery, migration, business expansion | Asynchronous                                         |
| **[[Cross-Region Replication and Volume Groups\| Volume Groups]]**            | Backup and recovery of multiple volumes          | Ensures **time-consistent snapshots** across volumes |

# 💡 **Use Cases**

- Boot volumes for compute instances    
- Durable storage for databases and applications
- Disaster recovery with cross-region replication
- Time-consistent snapshots of complex, multi-volume applications
