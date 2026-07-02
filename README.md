# ADF CI/CD Pipeline – Azure DevOps
📌#  Overview

This repository contains the CI/CD pipeline for Azure Data Factory (ADF) using Azure DevOps. It enables automated deployment of ADF resources (pipelines, datasets, linked services, triggers) across multiple environments:

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
🌍 Environments
Environment	Purpose	Parameter File
Dev	Development & testing	dev.json
QA	Validation & UAT	qa.json
Prod	Production workloads	prod.json
🔐 Prerequisites

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
Azure Data Factory (ADF)
Azure DevOps Pipelines
ARM Templates
YAML Pipelines
Azure Resource Manager
Git (Source Control)
