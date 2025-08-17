# OCI Cost Management Tools

Oracle Cloud Infrastructure (OCI) provides a comprehensive set of **cost control tools** to help you **track, analyze, limit, and forecast** your cloud spending:

# **Budgets**

- **Create budgets** per compartment.    
- **Set alerts** for:
    - Forecasted overspending
    - Actual spend thresholds
- Great for **proactive cost monitoring**.
## Cost Analysis**

- Visualize **historical spending trends**.
- Breaks down spend by service, compartment, etc.
- Helps with **forecasting and optimization**.

# **Usage Reports**

- Daily **CSV files** with detailed resource-level usage data.
- Stored in **Object Storage**, accessible via **cross-tenancy policies**.
- Supports **multi-tenancy analysis**.
# Service Limits

- Default OCI limits **prevent misuse and overspending**.
- Limits are categorized by **availability domain** and **service**.
- Can be **viewed and increased** via a support request.
# Quotas (Compartment Quotas)

- Enforce **resource usage boundaries** at the compartment level.
- Examples:
    - Max 10 VMs in a Dev compartment
    - Block Exadata in a test environment
- Helps with **resource governance and cost control**.
# 🧠 Key Concepts Recap

| Tool                   | Purpose                                                         |
| ---------------------- | --------------------------------------------------------------- |
| **Budgets**            | Alerts when usage nears or exceeds set thresholds               |
| **Cost Analysis**      | Historical insights for spend optimization                      |
| **Usage Reports**      | Raw, exportable daily usage data in CSV format                  |
| **Service Limits**     | OCI-imposed ceilings to prevent abuse, can be raised if needed  |
| **Compartment Quotas** | Policy-based control of specific resource types in compartments |

OCI gives you **multiple layers of cost visibility and control**, ranging from **real-time alerts (budgets)** to **resource caps (quotas)** and **deep usage insights (cost analysis + CSV reports)**. Combined with compartments and IAM policies, you can **govern spending across teams and projects** effectively.
