# 📝 **TL;DR: OCI Load Balancers**
OCI provides two main types of load balancers to help you achieve **high availability**, **scalability**, and **performance**:
##  **1. HTTP(S) Load Balancer (Layer 7)**
- Operates at **Layer 7 (Application Layer)** of the OSI model.    
- Understands **HTTP/HTTPS protocols**.    
- Supports **content-based routing**, **SSL termination**, etc.    
- Use when you need **intelligent routing** (e.g., based on URLs or headers).   
## **2. Network Load Balancer (NLB) (Layer 4)**
- Operates at **Layer 3/4 (Network/Transport Layers)**. 
- Understands **TCP**, **UDP**, and **ICMP**.    
- Has **lower latency**, **faster performance**.    
- Use when **speed is critical**, and you don’t need packet inspection.    

---

# 🚦 **Why Use Load Balancers?**

| Benefit               | Description                                                           |
| --------------------- | --------------------------------------------------------------------- |
| **High Availability** | Routes traffic away from failed backend servers.                      |
| **Scalability**       | Add/remove backend servers as client demand changes.                  |
| **Reverse Proxy**     | Clients connect to the load balancer, which proxies to backends.      |
| **Security**          | Hides backend infrastructure from public internet.                    |
| **Advanced Features** | SSL termination, path-based routing, sticky sessions (HTTP LBs only). |

# 🧱 **Load Balancer Types in Detail**

## **1. HTTP(S) Load Balancer (Layer 7)**

- **Understands**: HTTP, HTTPS
- **Use Cases**: Websites, REST APIs, intelligent routing.
- **Key Features**:
    - SSL termination
    - Header/path-based routing (content-based)
    - Session persistence
- **Shapes**:
    - **Flexible**: Scales between a min/max bandwidth (e.g., 10 Mbps – 8 Gbps)
    - **Predefined/Dynamic**: Micro, small, medium, large (auto-scales instantly)
- **Public or Private**:
    - **Public**: Exposed to internet (e.g., public websites)
    - **Private**: Internal app tiers (e.g., web → DB)

## **2. Network Load Balancer (NLB, Layer 3/4)**

- **Understands**: TCP, UDP, ICMP
- **Use Cases**: Performance-sensitive apps, low-latency networking.
- **Key Features**:
    - Faster connection processing
    - Lower latency than HTTP Load Balancer
    - Less intelligent (no packet inspection or content-based routing)
- **Public or Private**: Supports both.

---

# 🤔 **Which Load Balancer Should You Use?**

|Requirement|Best Option|
|---|---|
|Advanced routing (URL-based, SSL)|HTTP(S) Load Balancer|
|Low latency, high throughput|Network Load Balancer|
|Internal service communication|Private Load Balancer|
|Public-facing web traffic|Public Load Balancer|
|Need to scale automatically|Flexible or Dynamic shape|
![[Pasted image 20250727110458.png]]