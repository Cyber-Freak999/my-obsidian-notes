# 🌐 **Virtual Cloud Network (VCN)**

- A **VCN** is a **private, software-defined network** in OCI, used for **secure communication** between resources (within cloud, across regions, or with on-premises). A **VCN** is like your own private data center inside Oracle Cloud.
- It is defined by an **IP address range**, using **CIDR notation** (e.g., `10.0.0.0/16`).
- You split the VCN into **subnets** (e.g., public and private), which host your compute instances.

📌 Example:
- VCN CIDR block: `10.0.0.0/16`
- Subnets:
    - `10.0.1.0/24` → Public Subnet (for web servers)
    - `10.0.2.0/24` → Private Subnet (for databases)

---

# 🚪 **Connectivity Mechanisms Inside VCN**

## 🔹 **Internet Gateway (IGW)**
- Allows **bidirectional** internet traffic. 
- Used for public-facing instances (e.g., web servers).
- Requires instances in **public subnets** with public IPs.

### 🔹 **NAT Gateway**
- Allows **outbound-only** traffic to internet from **private subnets**.
- Inbound traffic from the internet is **blocked**.
- Ideal for patching or downloading software from internet securely.

### 🔹 **Service Gateway**
- Lets instances in VCN access **OCI public services (e.g., Object Storage)** **without** using the internet or NAT.
- Communication stays within Oracle’s backbone.

### 🔹 **Dynamic Routing Gateway (DRG)**
- Connects your VCN to:
    - **On-premises** data centers (via FastConnect or VPN).
    - **Other VCNs** in different regions (VCN peering).
- Used for **hybrid cloud** or **multi-region** architectures.
	

![[Pasted image 20250725142509.png]]