# 🧭 **How Route Tables Work**

## 📌 **Basic Routing Logic**

 VCN uses **route rules** to forward traffic to:
- **Internet**
- **On-premises networks**        
- **Other VCNs (peering)**        

 ### 📌 **Example Scenario**
A **private subnet** has a **route table** with:
- `0.0.0.0/0 → NAT Gateway` (for outbound internet access)
- `10.10.0.0/16 → DRG` (for traffic to on-premises)

![[Pasted image 20250725154236.png]]

### 🧠 **Routing Priority: Longest Prefix Match**

- The **most specific route wins**.
    - E.g., `/16` is more specific than `/0`, so on-prem traffic (e.g., DNS queries) uses **DRG**.
    - Everything else goes to the **NAT Gateway** for internet access.

---

# 🚪 **Route Table Targets / Gateways**

|Gateway Type|Purpose|
|---|---|
|**Internet Gateway**|Bidirectional access to the internet (public subnets)|
|**NAT Gateway**|Outbound-only access to internet (private subnets)|
|**Service Gateway**|Private access to Oracle services (e.g., Object Storage)|
|**DRG**|Private access to on-premises or remote VCNs|

---

# 🔁 **VCN Peering**

## 🟢 **Local Peering Gateway (LPG)**
- **Within the same region** 
- Used for **VCN-to-VCN** communication without using the internet.

## 🔵 **Remote Peering via DRG**
- **Across different OCI regions**    
- Uses **DRG (Dynamic Routing Gateway)** on both ends.    
- Works similarly to hybrid on-premises connections.    

![[Pasted image 20250725153933.png]]

---

# 📈 **Scaling VCN Communication: DRG v2**

## ⚡ Problem:
If you have **many VCNs** (e.g., 10, 100, 300+), **point-to-point peering** becomes complex and unmanageable.    

## ✅ **Solution: DRG v2**

- No more point-to-point LPG connections.    
- Use **one DRG** to connect **up to 300 VCNs**.
- Enables **full mesh communication**.
- You can **add another DRG** and **peer them remotely** to scale even more.

![[Pasted image 20250725154010.png]]