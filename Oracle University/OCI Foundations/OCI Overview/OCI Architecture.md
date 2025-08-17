# Physical Architecture Overview

## ✅ **1. Region**

- A **region** is a **geographic area** that contains one or more **Availability Domains (ADs)**.    
- Each region is **isolated** from others for data sovereignty and high availability.
- OCI has **global coverage** with many regions, including partnerships like **Oracle-Azure Interconnect** and hybrid offerings like **Dedicated Region Cloud@Customer**.

## ✅ **2. Availability Domain (AD)**

- An **Availability Domain** is a **fault-isolated data center** within a region.
- Multiple ADs are **connected by a low-latency, high-bandwidth network**, allowing for synchronous replication.
- ADs **do not share** key infrastructure like:
    - Power supply
    - Cooling
    - Physical network (ToR switches, etc.)
- A **failure in one AD won’t impact others**, enabling high availability designs.
Example:
- A **region may have 3 ADs**.
- If AD1 fails, AD2 and AD3 continue functioning independently.
## ✅ **3. Fault Domain (FD)**

- **Fault Domains** are **logical groupings** of hardware within an AD.    
- Each AD typically has **3 Fault Domains**.
- Resources in different FDs **don’t share hardware components** like:
    - Physical servers
    - Racks
    - Top-of-Rack (ToR) switches
    - Power Distribution Units (PDUs)
- OCI uses FDs to limit **blast radius** of failures or maintenance events.
Example:
- OCI ensures that **only one fault domain** is undergoing updates at any time to minimize downtime risk. 
# Region Selection Criteria

When choosing a region, consider the following:

|Criteria|Description|
|---|---|
|🛰️ **Proximity**|Choose a region closest to your users for **lowest latency and best performance**|
|🏛️ **Compliance**|Some countries require **data residency** due to regulatory laws|
|⚙️ **Service Availability**|Not all services are available in all regions; consider **feature availability**|

# Designing for High Availability 

To avoid single points of failure, use OCI’s physical constructs wisely:
## 🧱 **Inside one AD**

- Use multiple **Fault Domains** for:   
    - Application instances
    - Databases
    - Load balancers
## 🧱 **Across multiple ADs**

- Replicate your workloads (App + DB) across ADs    
- Ensure **data synchronization** with tools like **Oracle Data Guard** for active-passive or active-active setups

**Example Architecture:**
- **App tier** replicated across FD1, FD2, FD3 in AD1 
- **DB tier** also distributed across FDs
- Entire stack replicated in **AD2**, enabling failover
- Use **Virtual Cloud Networks (VCNs)** to interconnect resources

Even if a region has only one AD:
- Still leverage **Fault Domains** to improve resilience 
- Suitable for many workloads with proper redundancy

Many countries have **at least two OCI regions**    
- Use the second region for:
    - Disaster Recovery (DR)
    - Backups
    - Regulatory compliance

OCI provides **service-level agreements (SLAs)** for:
- **Availability**
- **Manageability**
- **Performance**
These SLAs reflect Oracle's commitment to reliable infrastructure.