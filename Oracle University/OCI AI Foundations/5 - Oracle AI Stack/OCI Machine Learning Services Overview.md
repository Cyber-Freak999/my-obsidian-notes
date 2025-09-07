# Overview

Oracle Cloud Infrastructure (OCI) provides **Machine Learning (ML) services** that complement its **AI Services**. While AI Services are prebuilt for business users, **ML Services (like OCI Data Science)** are designed for **data scientists** who build, train, and deploy custom ML models using open-source tools.

# Core Focus: **OCI Data Science**

A **fully managed cloud service** supporting the entire machine learning lifecycle — from experimentation to deployment — with built-in security, scalability, and collaboration features.
## What, Whom, Where and How

- What: Build, train and deploy models
- Whom: Data scientists and ML engineers.    
- Where: Jupyter lab notebook
- How: Preserve in model catalog
# Core Principles of OCI Data Science

1. **Accelerated**    
    - Easy access to CPU/GPU compute.
    - JupyterLab interface with preinstalled libraries.
    - Oracle’s own **Accelerated Data Science (ADS) SDK** for AutoML
    - Streamlined approach to building model. 
2. **Collaborative**
    - Shared assets and projects among data science teams.
    - Reproducibility and auditability built-in (e.g., model provenance tracking).
    - Versioned, team-based model management.
3. **Enterprise-Grade**
    - Integrated with OCI’s identity, security, and access controls.       
    - Fully managed infrastructure to meet the needs of modern enterprises (no manual setup for storage, compute, etc.).        
    - Handles patching, maintenance, and upgrades.        
# Features & Terminology

| Term                                                                                                                                                    | Description                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| [**Projects**](https://docs.oracle.com/en-us/iaas/Content/data-science/using/create-projects.htm#create-project)                                        | Containers/workspaces to organize notebooks, models, and assets. Unlimited per tenancy.                                                      |
| [**Notebook Sessions**](https://docs.oracle.com/en-us/iaas/Content/data-science/using/create-notebook-sessions.htm#create-notebooks)                    | JupyterLab environments (Python-based), fully managed. You can choose compute shape (CPU/GPU).                                               |
| [**Conda Environments**](https://docs.oracle.com/en-us/iaas/Content/data-science/using/conda_understand_environments.htm#conda_understand_environments) | Package/environment manager in python used for dependency isolation and reproducibility in notebooks.                                        |
| [**Accelerated Data Science(ADS) SDK**](https://accelerated-data-science.readthedocs.io/en/latest/index.html)                                           | Oracle’s Python library that simplifies all ML steps—data access, training (including AutoML), evaluation, and model explainability.         |
| [**Models**](https://docs.oracle.com/en-us/iaas/Content/data-science/using/models_saving_catalog.htm#saving_models_catalog)                             | Trained ML artifacts (mathematical representations of patterns in your data).                                                                |
| [**Model Catalog**](https://docs.oracle.com/en-us/iaas/Content/data-science/using/models-about.htm)                                                     | Central repository for storing, tracking, and managing models with metadata, versioning, and team sharing.                                   |
| [**Model Deployments**](https://docs.oracle.com/en-us/iaas/Content/data-science/using/ai-quick-actions-model-deploy.htm#ai-quick-actions-model-deploy)  | Converts models into HTTP endpoints for real-time predictions (standard way to serve ML models).                                             |
| [**Jobs**](https://docs.oracle.com/en-us/iaas/Content/data-science/using/jobs-create.htm#jobs_creating)                                                 | Batch-style or repeatable tasks for training or scoring, run on fully managed infrastructure. Useful for scheduling or automating workloads. |

# How It Works (Lifecycle Summary)

1. **Create a project** → organize your team’s work.    
2. **Launch a notebook session** → develop and train models in JupyterLab using open-source tools.
3. **Use ADS SDK** → simplify common ML tasks (data wrangling, AutoML, explainability).    
4. **Store models** in the **Model Catalog** with full metadata and versioning.    
5. **Deploy models** to **HTTP endpoints** for production use.    
6. **Automate workflows** using **Jobs** for training, evaluation, or batch inference.    


> [!NOTE] My view on OCI ML Services
> It's the go-to solution for teams looking to build sophisticated ML models while avoiding infrastructure overhead.
