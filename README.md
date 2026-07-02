# ADF CI/CD Pipeline – Azure DevOps
# 📌 Overview
CI/CD in Azure Data Factory (ADF) using Azure DevOps is a process where you develop and test pipelines in the Dev environment, store them in a Git repository, and then automatically validate and deploy them to other environments like QA and Prod. Continuous Integration (CI) ensures that every change is validated and converted into deployable ARM templates, while Continuous Deployment (CD) uses these templates to reliably move changes across environments using parameter files such as dev.json, qa.json, and prod.json, ensuring consistent and automated releases without manual intervention.

🟦 Development (Dev)
🟨 Testing / QA
🟥 Production (Prod)

The pipeline follows Infrastructure as Code (IaC) principles using ARM templates generated from ADF Publish branch.

# CI/CD Workflow Overview
# 1. Continuous Integration (CI)

## Pipeline: CI_build.yml

Responsibilities:

Validate ADF JSON files
Check syntax & dependencies
Generate ARM template
Publish build artifacts

Output:

ARM template
Parameter files
Deployment-ready package
# 2. Continuous Deployment (CD)

## Pipeline: cd_deploy.yml

Responsibilities:

Deploy ARM template to target environment
Apply environment-specific parameters (Dev / QA / Prod)
Configure linked services dynamically
Trigger post-deployment validation
# 3. Master Pipeline

## Pipeline: cicd_pipeline.yml

Responsibilities:

Orchestrates CI → CD flow
Supports multi-stage deployments
Handles approvals (QA → Prod gates)
## Environment Configuration

| Environment | Purpose               | Parameter File |
|------------|-----------------------|----------------|
| Dev        | Development & testing | `dev.json`     |
| QA         | Validation & UAT      | `qa.json`      |
| Prod       | Production workloads  | `prod.json`    |
# 🔐 Prerequisites

Before running pipelines, ensure:

Azure Data Factory instance created
Azure DevOps Service Connection configured
Proper RBAC permissions assigned
ARM deployment permissions enabled
Self-hosted or Microsoft-hosted agent ready

# Deployment Flow

ADF Code Changes
      ↓
CI Pipeline (Validation)
      ↓
ARM Template Generation
      ↓
CD Pipeline Trigger
      ↓
Deploy to Dev
      ↓
Approval Gate
      ↓
Deploy to QA
      ↓
Approval Gate
      ↓
Deploy to Prod

# Key Features
✔ Automated validation of ADF JSON artifacts
✔ Multi-environment deployment support
✔ ARM-based infrastructure deployment
✔ Parameterized configuration per environment
✔ Azure DevOps YAML-based pipelines
✔ Scalable CI/CD design for enterprise workloads
# Technologies Used
1. Azure Data Factory (ADF)
2. Azure DevOps Pipelines
3. ARM Templates
4. YAML Pipelines
5. Azure Resource Manager
6. Git (Source Control)
## 📁 Project Structure
```
cicd/
├── README.md                          # This file
├── package.json                       # Node.js project configuration
├── .gitignore                         # Git ignore rules
├── build/                             # Build output directory
│   └── (generated ARM templates)
├── src/                               # Source code
│   ├── dataflows/                    # Data flow definitions
│   ├── datasets/                     # Dataset configurations
│   ├── factories/                    # Factory configurations
│   ├── integrationruntimes/          # Integration runtime configs
│   ├── linkedservices/               # Linked service definitions
│   ├── pipelines/                    # Pipeline definitions
│   └── triggers/                     # Trigger configurations
├── templates/                         # ARM templates
│   ├── arm-template.json
│   ├── parameters-dev.json
│   ├── parameters-staging.json
│   └── parameters-prod.json
├── scripts/                          # Deployment scripts
│   ├── deploy.ps1
│   ├── validate.ps1
│   └── rollback.ps1
└── azure-pipelines.yml               # CI/CD configuration
```

👤 Author

Maintained by: Amanuel Lefebo
