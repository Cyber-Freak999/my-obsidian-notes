# **🔹 TL;DR (Too Long; Didn't Read)**

Oracle Cloud Infrastructure (OCI) Compute offers flexible, scalable virtual machines (VMs) and bare metal servers. Key benefits include:

- **Scalability** with customizable compute shapes (choose your own CPU & memory).    
- **High Performance**, including support for ARM (Ampere A1), AMD, and Intel processors.
- **Lower Pricing**, with cost-effective options like preemptible VMs and pay-as-you-go billing.

---

# **Introduction to [OCI Compute](https://docs.oracle.com/en-us/iaas/Content/Compute/home.htm)**

- OCI Compute provides infrastructure to run applications via **VMs, bare metal servers,** and **dedicated hosts**.
- Designed for **scalability**, **performance**, and **cost-efficiency**.
- You can choose custom CPU and memory configurations using sliders.
- No need to stick to fixed "t-shirt sizes" (small, medium, large).
- Enables better **resource right-sizing**, avoiding under/over-provisioning.
# **Types of Compute Instances**

- **Virtual Machines (VMs):**
    - Shared and multi-tenant.
    - Strong isolation despite shared infrastructure.
- **Bare Metal Servers:**
    - Entire physical server dedicated to a single tenant.
- **Dedicated Hosts:**
    - Physical servers where you can run your own VMs.
    - No other customers' workloads on the same host.
## **Choice of Processors**

OCI is one of only two major cloud providers offering multiple processor architectures:

- **AMD EPYC**
- **Intel Xeon**
- **ARM (Ampere Altra A1)**:
    - Great for mobile-optimized and web workloads.
    - Proven to have superior **price-performance**:
        - 32% better than AMD.
        - 69% better than Intel (based on Nginx Reverse Proxy benchmark, no auth).

# **Pricing Advantages**

- **Pay-as-you-go** pricing: only pay for what you use.
- **~50% cheaper** than competing cloud providers.
- **Preemptible VMs**:
    - Short-lived, budget-friendly VMs for fault-tolerant or batch jobs.
    - Priced **50% lower** than regular instances.