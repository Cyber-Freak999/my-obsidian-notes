# 🔹 **TL;DR (Too Long; Didn’t Read)**

- **Containers vs. Virtual Machines**:  
    Containers are lightweight, fast, and portable. Unlike VMs, containers **don’t include an OS**, making them more **resource-efficient** and **faster to boot**.
- **Kubernetes**:  
    An open-source **container orchestration** system for **automating deployment, scaling, and management** of containerized apps.
- **OKE (Oracle Kubernetes Engine)**:  
    A **fully managed Kubernetes service** by Oracle Cloud Infrastructure (OCI). Offers features like **autoscaling, self-healing nodes**, and **zero-cost control plane**.
- **Key Concepts**:
    - **Node**: A VM or bare metal server running Kubernetes (also called worker node).
    - **Pod**: Smallest deployable unit in Kubernetes (1+ containers).
    - **Node Pool**: Group of nodes in a cluster.
    - **Control Plane**: Managed by Oracle, handles orchestration (e.g. scheduling, scaling, etc.).
    - **Cluster Types**:
        - **Enhanced Clusters**: Full features + SLA
        - **Basic Clusters**: Core features + SLO (no SLA)
    - **Node Types**:
        - **Virtual Nodes**: Serverless, Oracle-managed, only in enhanced clusters.
        - **Managed Nodes**: Customer-managed, available in both cluster types.

---

#  **Containers vs. Virtual Machines (VMs)**

|Feature|Virtual Machines|Containers|
|---|---|---|
|OS|Each VM has its own OS|Share host OS, no OS inside|
|Boot Time|Minutes|Seconds|
|Size|GBs|MBs|
|Portability|Low|High|
|Resource Use|High (due to multiple OSes)|Low (shared kernel)|

**Key takeaway**: Containers are ideal for **cloud-native**, **microservices-based** apps due to speed, size, and portability.

#  **What Is Kubernetes?**

- Open-source **container orchestration** platform.
- Automates:
    - Deployment
    - Scaling
    - Health checks (self-healing)
    - Networking and service discovery
- Great for **high availability** and **autoscaling** workloads.

![[Pasted image 20250730021320.png]]
# **OKE Benefits**

- **Fully managed** by Oracle, scalable and highly available
- Uses kubernetes.
- Supports **Arm** and **GPU-based** instances
- **CLI/API** support, one-click cluster creation
- **Free control plane** (no charge for Kubernetes masters)
- DevOps-friendly: autoscaling, auto-upgrades, self-healing nodes

## Components of a Cluster

|Component|Description|
|---|---|
|**Worker Node**|VM where containers run (Kubernetes agent installed)|
|**Node Pool**|Group of worker nodes|
|**Pod**|Smallest Kubernetes unit (1+ containers, shared resources)|
|**Control Plane**|Manages cluster state (scheduling, scaling, health) - fully managed by OCI|
|**etcd**|Key-value store that holds the cluster state|

![[Pasted image 20250730021830.png]]

# 🏗️ **Cluster Types in OKE**

|Cluster Type|Features|SLA/SLO|Supports Virtual Nodes?|
|---|---|---|---|
|**Enhanced**|Full features, autoscaling, patching|**SLA** (financially backed)|✅ Yes|
|**Basic**|Core Kubernetes only|**SLO** (no SLA)|❌ No|

# **Node Types**

|Node Type|Managed By|Cluster Types Supported|Notes|
|---|---|---|---|
|**Virtual Nodes**|Oracle|Enhanced only|Serverless, Oracle handles patching, scaling, upgrades, HA|
|**Managed Nodes**|Customer|Basic and Enhanced clusters|More control, you manage updates, sizing, and lifecycle|
