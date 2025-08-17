# **🔹 TL;DR (Too Long; Didn't Read)**

An **instance** in Oracle Cloud Infrastructure (OCI) is a compute host (VM or bare metal) that depends on **networking**, **storage**, and **resilience features** like **live migration**. Key components include:

- **VCN & Subnets**: Provide network connectivity.
- **vNICs**: Connect the instance to a subnet with a private IP.
- **Boot & Block Volumes**: Provide OS and data storage.
- **Live Migration**: Keeps your VMs running during failures or maintenance by automatically moving them to healthy hosts.

---

# **What Is an Instance?**
An **instance** = a compute host (virtual or physical). It requires underlying **network** and **storage** services to function properly.
An **OCI Region** is made up of **Availability Domains (ADs)** (i.e., data centers). Instances are launched within these regions and ADs.   
Before launching a compute instance, you need a **VCN**. A VCN is segmented into **subnets** (public or private). Subnets act as containers for network resources like VMs.

![[Pasted image 20250730014751.png]]
## **vNICs and IP Addressing**

- Each compute instance is connected to the subnet using a **virtual NIC (vNIC)**.
- The vNIC is a **virtualized** version of a physical network interface card (NIC).
- The **private IP** of the instance is assigned from the subnet.
## **Boot and Block Volumes**

- Instances don’t store their OS locally; they use **boot volumes**, which are remote and persistently stored.    
    - Boot volume = OS and initial software image.
- **[[Block Storage|Block volumes]]** are used for data (e.g., file systems, applications).
- Both are managed by the **Block Volume Service** (remote, network-attached storage).
## **Control Plane Dependencies**

Compute relies on:
- **Networking Control Plane** (VCN, subnets, vNICs).
- **Block Storage Control Plane** (boot volumes, block volumes).
# **Live Migration**

- **Live Migration** allows VMs to move to a healthy host **without rebooting**.
- Ensures **high availability** during:
    - Hardware failure
    - Maintenance events
- You can **opt-in or opt-out** of this feature.
- Provides enterprise-grade resilience **built-in** to OCI.