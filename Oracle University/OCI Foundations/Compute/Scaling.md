# 🔹 **TL;DR (Too Long; Didn't Read)**

**Scaling** in OCI Compute refers to dynamically adjusting compute capacity to meet demand. Two types:

- **Vertical Scaling**: Change instance shape (CPU, memory). Requires **downtime**.
- **Horizontal Scaling (Autoscaling)**: Add or remove instances automatically based on traffic or usage metrics. Enables **high availability** and **elasticity**.

| Scaling Type   | Description                      | Downtime | High Availability | Common Use Case                   |
| -------------- | -------------------------------- | -------- | ----------------- | --------------------------------- |
| **Vertical**   | Resize instance (CPU/RAM)        | Yes      | No                | Resource upgrade for one instance |
| **Horizontal** | Add/remove instances dynamically | No       | Yes               | Traffic/load-driven scalability   |

Autoscaling is **free to use**, easy to set up, and works in 3 steps:

1. Create a **configuration (template)**.
2. Create an **instance pool**.
3. Define **Autoscaling rules** (min, max, desired capacity + CPU/memory triggers).

---

# **What Is Scaling?**

- **Scaling** = adjusting compute resources to meet workload needs.
- Two types:
    - **Vertical Scaling**: Scaling **up/down** by changing instance **shape** (CPU/memory).
    - **Horizontal Scaling (Autoscaling)**: Scaling **out/in** by adding/removing **instances**.
## **Vertical Scaling**

- **What You Can Scale**:    
    - CPU cores
    - Memory
- **How It Works**:
    - Requires **downtime** because the instance is moved to a new shape/host.
    - Recommended to **stop the instance** before scaling vertically.
- **Use Case**:
    - When you want to upgrade/downgrade a single instance’s capacity.

## **Horizontal Scaling / Autoscaling**

- **What It Is**:
    - Automatically **adds/removes instances** based on demand.
- **Scale-Out** = more VMs (e.g., 1 → 4)
- **Scale-In** = fewer VMs (e.g., 4 → 1)
- **Benefits**:
    - **Handles spikes in traffic**
    - **Improves fault tolerance** (other VMs continue if one fails)
    - **No extra cost** for using the feature (you only pay for added compute)

# **How Autoscaling Works**

## **Step 1: Create a Configuration**

- Called a **config** in OCI.
- It’s a **template** of your instance:
    - OS image
    - Shape (CPU/memory)
    - Metadata
    - Network and storage settings

## **Step 2: Create an Instance Pool**

- A **group** of identical instances using your config.
- You can:
    - Start/stop all at once
    - Distribute across **Availability Domains** for HA

## **Step 3: Define Autoscaling Rules**

- Set:    
    - **Initial size**
    - **Min and max size**
    - **Scaling rules**:
        - Example: If CPU > 70%, add 2 instances
        - If CPU < 30%, remove 1 instance
- **Continuous Monitoring**:
    - Autoscaler checks metrics and automatically adjusts pool size

# ✅ **Example Use Case**

You’re running a webstore:
- During a sales event, traffic spikes.
- Autoscaling adds VMs automatically.
- After traffic drops, VMs are removed.
- You save cost and ensure performance.
