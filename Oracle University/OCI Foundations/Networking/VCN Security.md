OCI provides **two main ways to control network traffic** within a VCN:
# 🔐 **1. Security Lists**
Think of a **Security List** as a basic firewall applied to **all VNICs in a subnet**.
##  **Key Characteristics**
- Rules are based on **CIDR blocks** (e.g., `0.0.0.0/0`). 
- Can be **stateful** (automatic return traffic allowed) or **stateless** (return traffic must be explicitly allowed).
- Apply **inbound and outbound** rules.
- **Simpler**, but **less flexible** than NSGs.
## **Example Rules**
![[Pasted image 20250725155424.png]]

# 🧱 **2. Network Security Groups (NSGs)**
Think of **NSGs** as **application-specific firewalls** for individual instances (VNICs).
##  **Key Characteristics**
- Applied to **specific VNICs**, not the entire subnet. 
- **NSGs can reference other NSGs** in rules (more dynamic than CIDRs).
- Allow **multiple NSGs per VNIC**.
- Great for **microsegmentation** and **granular control** in shared subnets.
## **Example Rules with NSGs**
![[Pasted image 20250725155530.png]]

# Useful Comparison

|Feature|**Security Lists**|**NSGs**|
|---|---|---|
|Scope|Entire Subnet|Individual VNICs (instances)|
|Rule Targets|Only CIDR blocks|CIDRs **and** NSGs|
|Flexibility|Lower|Higher|
|Use Case|Simple apps, legacy setups|Granular app-level segmentation|
|Can assign multiple per VNIC|❌ No|✅ Yes|
|Common in|Quick-start deployments|Production-grade architectures|