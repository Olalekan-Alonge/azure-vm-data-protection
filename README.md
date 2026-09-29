# Azure VM Backup & Data Protection

## Overview

This project documents an Azure virtual-machine data protection and disaster-recovery lab based on **AZ-104 Azure Administrator** skills.

The implementation demonstrates how to provision an Azure VM environment with an ARM template, create an Azure Recovery Services vault, configure backup protection, and apply retention/security settings.

> **Security note:** Public screenshots have been sanitized to remove account/subscription-identifying information. Do not commit Azure passwords, secrets, access keys, or unredacted portal screenshots.

## Project Objectives

- Provision Azure infrastructure from an ARM template.
- Deploy an Azure virtual machine and supporting network resources.
- Create and configure an Azure Recovery Services vault.
- Configure geo-redundant backup storage.
- Configure soft-delete protection with a 14-day retention period.
- Create a VM backup policy.
- Configure daily VM backups and retention.
- Demonstrate the operational workflow for Azure backup and recovery.
- Document the implementation for portfolio and professional use.

## Azure Resources Demonstrated

- Azure Virtual Machine
- Azure Virtual Network
- Azure Subnet
- Network Interface
- Public IP Address
- Network Security Group
- Managed OS Disk
- Azure Recovery Services Vault
- Azure Backup
- Backup Policy

## Infrastructure Configuration Observed

| Component | Configuration |
|---|---|
| Resource Group | `az104-rg-region1` |
| Region | Central US |
| VM image | Windows Server 2022 Datacenter |
| VM size | Standard_D2s_v5 |
| Virtual Network | `az104-10-vnet` |
| Address space | `10.0.0.0/24` |
| Subnet | `subnet0` |
| Recovery Services vault | `az104-rsv-region1` |
| Backup storage | Geo-redundant (GRS) |
| Soft delete | 14 days |
| Backup type | Azure VM |
| Backup policy | Standard |
| Backup frequency | Daily |
| Example backup time | 12:00 AM |
| Daily retention | 30 days |

## Architecture

```text
                    Azure Subscription
                           |
                    Resource Group
                    az104-rg-region1
                           |
             +-------------+-------------+
             |                           |
       Virtual Network             Recovery Services
        az104-10-vnet                    Vault
        10.0.0.0/24               az104-rsv-region1
             |                           |
          subnet0                   Azure Backup
             |                           |
          NIC + NSG                Backup Policy
             |                    Daily / Retention
          Public IP
             |
       Windows Server VM
       Standard_D2s_v5
```

## Implementation Workflow

### 1. Provision infrastructure

An ARM deployment template was used to provision the VM and networking components.

The deployment created:

- Virtual network
- Subnet
- Network interface
- Network security group
- Public IP
- Virtual machine
- Managed OS disk

### 2. Create Recovery Services vault

A Recovery Services vault was created in the same Azure region as the deployed VM.

### 3. Configure vault protection

The vault was configured with:

- Geo-redundant storage
- Cross-region restore disabled for this lab configuration
- Soft delete retention of 14 days

### 4. Configure VM backup

The backup workflow was configured for an Azure virtual machine using the **Standard** policy type.

The policy demonstrates:

- Daily backup
- Scheduled backup time
- Instant recovery snapshot retention
- Daily recovery-point retention

### 5. Validate deployment

The screenshots document successful deployment of the infrastructure and Recovery Services vault and the subsequent backup configuration workflow.

## Skills Demonstrated

**Azure Administration**
- Resource groups
- Azure VM deployment
- Azure networking
- ARM templates
- Azure Backup
- Recovery Services vaults

**Data Protection**
- VM-level backup
- Backup policies
- Retention
- Geo-redundant storage
- Soft delete
- Recovery planning

**Infrastructure as Code**
- Azure Resource Manager templates
- Parameter files
- Repeatable infrastructure deployment

## Repository Structure

```text
azure-vm-data-protection/
├── README.md
├── arm-template/
│   ├── README.md
│   ├── template.json
│   └── parameters.json
└── screenshots/
    ├── 01-lab-10-introduction-and-data-protection-architecture.png
    ├── ...
    └── 20-standard-vm-backup-policy-with-daily-schedule-and-retention.png
```

## Important

The screenshots establish the implementation evidence, but the original ARM `template.json` and `parameters.json` files were not included in the uploaded screenshots.

To make this repository **fully deployable**, add the original JSON files from the lab:

```text
arm-template/template.json
arm-template/parameters.json
```

Do **not** upload passwords or secret values. Use secure parameters, Azure Key Vault, or deployment-time secret input.

## Portfolio Summary

**Azure VM Backup & Data Protection**

Designed and implemented an Azure data-protection solution using Azure Virtual Machines, Virtual Network, NSG, Public IP, ARM templates, Azure Recovery Services Vault, and Azure Backup. Configured geo-redundant backup storage, 14-day soft-delete protection, and a daily VM backup policy with defined retention. The project demonstrates practical Azure administration, infrastructure-as-code, backup, recovery, and cloud data-protection skills.

## Author

**Lex**

Azure Cloud Engineering | Cloud Architecture | Cybersecurity

