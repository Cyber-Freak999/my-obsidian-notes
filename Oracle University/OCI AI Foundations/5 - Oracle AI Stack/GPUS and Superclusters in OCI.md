# **OCI Supercluster: RDMA-Based Architecture for Massive GPU Workloads**

## What Is RDMA and Why It Matters?

- **RDMA (Remote Direct Memory Access)** allows **zero-CPU-overhead** data transfers between machines.
- Enables **ultra-low latency** and **high-bandwidth** communication between GPUs and across servers.
- Used across Oracle services like:
    - Autonomous Database
    - Exadata Cloud Service (ExaCS)
    - High-Performance Computing (HPC)
    - Large-scale AI/GPU workloads
## Strategic Bet on RoCE (RDMA over Converged Ethernet)

- OCI adopted **RoCE** to support RDMA over standard Ethernet networks.
- Now used across **GPU**, **HPC**, and **database workloads**.
- This infrastructure supports:
    - **High performance**
    - **Scalability**
    - **Cost efficiency**
# **OCI GPU Supercluster: Architecture Highlights**

## **Node and Fabric Architecture**

- Each GPU node has:
    - **8× NVIDIA A100 GPUs** (interconnected with **NVLinks**).
- Nodes connect to a **non-blocking RDMA fabric**:
    - **1.6 Tbps per node** (i.e., **200 Gbps per GPU**).
    - Fully non-blocking: any GPU can talk to any other concurrently.
## **Three-Tier Clos Network Fabric**

- Supercluster uses a **three-tier Clos** topology to scale **tens to hundreds of thousands of GPUs**.
- Composed of **multiple blocks**, each with 2-tier Clos fabrics.
- GPU-to-GPU latency:
    - **Within a block**: ~**6.5 µs**
    - **Across blocks**: up to ~**20 µs**

## **Lossless Networking & Quality of Service (QoS)**

- **Lossless RDMA fabric**:
    - Avoids packet drops via **intelligent congestion management** and **high buffer allocation**.
    - Tailored switch buffer sizes to accommodate long cable distances and higher latencies.        

# **Optimizing Performance: Smart Placement & Locality Awareness**

## Control Plane Placement Logic

- Latency-sensitive workloads (e.g., HPC, DB) are **kept within a block** or even a **single Top-of-Rack (ToR)** switch.
- Ensures **lowest possible latency** (~6.5 µs or lower).
## Network Locality Hints

- For larger workloads (spanning blocks), OCI provides **network topology hints** to help optimize GPU communication patterns.
- Helps ML/DL frameworks localize traffic:
    - **~85% of traffic remains local** to block or ToR
    - Minimizes cross-block hops
    - Improves **latency** and **throughput**
## Reduced Flow Collisions

- Traffic locality also reduces **flow collisions** (contention on shared links).
- Leads to **higher sustained throughput** and **more efficient use of fabric**.

# **Supercluster Design: Key Takeaways**

|Feature|Benefit|
|---|---|
|**RDMA & RoCE fabric**|Ultra-low latency, zero-CPU overhead|
|**1.6 Tbps per node**|Massive bandwidth per GPU|
|**Three-tier Clos network**|Scalability to 100,000+ GPUs|
|**QoS-enabled & lossless design**|Predictable, reliable performance|
|**Smart workload placement**|Optimal performance based on workload size/latency needs|
|**Locality hints for ML/DL orchestration**|Reduced latency and network congestion|
