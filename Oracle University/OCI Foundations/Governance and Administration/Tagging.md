# 🏷️ TL;DR

**Tags** in Oracle Cloud Infrastructure (OCI) are **key-value pairs** used to **organise, manage, and control access to resources**. They help with:

- 🔍 **Resource organisation**
- 💸 **Cost management**
- 🔐 **Access control via IAM policies**

OCI supports two types of tags:

- **Free-form tags**: Simple key-value pairs with no structure or enforcement.
- **Defined tags**: Structured, governed tags grouped in namespaces, supporting policies and value constraints.

---

# 🔍 **Why Use Tags in OCI?**

## 📁 **Organization**

Tag resources (like compute, storage, networking) to track:
- Application ownership (`project=alpha`)
- Environment (`environment=production`)
- Business unit, team, or function

## 💰 **Cost Management**

Tags let you **track spending by tag values**, e.g.:
- "Show me the cost of all resources tagged with `project=alpha`"
- Supports **granular billing visibility** for chargeback/showback models

## 🛡️ **Access Control**

You can **write IAM policies** based on tag values (instead of resource names or IDs):

```plaintext
Allow group FinanceTeam to manage all-resources in tenancy where target.tag.environment = 'production'
```

This allows **fine-grained access** at scale.

# 🧩 **Types of Tags**

| Type          | Description                                                                                                            | Governance Level |
| ------------- | ---------------------------------------------------------------------------------------------------------------------- | ---------------- |
| **Free-form** | - Simple key-value (`key=value`)<br>- No defined schema or access restriction                                          | Low              |
| **Defined**   | - Created in a **namespace**<br>- Governed by IAM policies- Optional value restrictions (e.g., predefined values only) | High             |

# 🧱 **Defined Tags in Practice**

Structure:

```plaintext
Operations.Environment = "Production"
```

Namespace: operations
Key: environment
Value: production

Features:
- Defined in **tag namespaces** (like folders for tags)    
- You can **restrict who can use tags** (via IAM)
- You can **control what values are allowed** (e.g., only `dev`, `test`, `prod`) based on tag key definitions.

Tag namespace is a container for a set of tag keys with tag key definitions.

> 🔒 **Important**: Defined tag **namespaces cannot be deleted**, but you can **retire** them to stop usage.

# Recap

- **Tag everything**—it's essential for scale and visibility.    
- Use **free-form tags** to get started quickly.    
- Use **defined tags** for controlled environments and automated governance.    
- Tags help with **cost tracking**, **resource management**, and **security**.