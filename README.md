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
├── screenshots.md
├── screenshots/
│   ├── 01-*.png
│   ├── ...
│   └── 16-*.png
└── arm-template/
    ├── README.md
    ├── template.json
    └── parameters.json
```

## Important

The ARM files in `arm-template/` are **reconstructed equivalents based on the configuration visible in the lab screenshots**. They are provided to demonstrate infrastructure-as-code structure and are not represented as the original Microsoft lab files.

Before deploying, review the template for your own subscription, region, naming requirements, security controls, and current Azure resource/API versions.

**Security:** `parameters.json` contains a placeholder password only. Never commit real passwords, access keys, connection strings, tokens, or other secrets. Use secure deployment parameters or Azure Key Vault for sensitive values.

## Potential Problems and How to Resolve Them

| Potential problem | How to resolve it |
|---|---|
| ARM deployment fails because a resource name is already in use | Check the deployment error and use unique resource names or adjust the template parameters. |
| VM deployment fails because the selected VM size is unavailable in the region | Choose an available VM size in the target region and update the `vmSize` parameter. |
| Azure Backup cannot protect the VM | Confirm the VM is supported, the Recovery Services vault is in the correct region, and the backup configuration is completed successfully. |
| Backup policy settings do not match the lab | Review the backup policy schedule and retention settings before enabling protection. |
| Recovery Services vault storage configuration cannot be changed after protection is enabled | Select the required redundancy setting during initial vault configuration and verify it before protecting workloads. |
| Soft delete or other protection settings appear different from the lab | Azure portal options can change over time. Verify the current Microsoft Azure Backup documentation and the settings available in the selected region. |
| RDP access to the VM is blocked | Verify the NSG inbound rule, VM status, public IP association, and Windows firewall configuration. For production, restrict RDP to trusted source IPs or use a more secure access method. |
| Deployment exposes credentials in the parameter file | Never commit real credentials. Replace secrets with secure parameters, Key Vault, or deployment-time input and rotate any credential that was accidentally exposed. |
| Screenshot evidence contains subscription or account information | Redact sensitive identifiers before publishing screenshots to a public repository. |

> **Lab security note:** The reconstructed template includes an RDP rule suitable for demonstrating the lab workflow. In a production environment, avoid unrestricted RDP access and apply least-privilege network controls.

## Lessons Learned

- **Infrastructure as Code improves repeatability:** ARM templates make Azure infrastructure easier to reproduce consistently instead of creating every resource manually.
- **Backup planning is more than enabling backup:** Storage redundancy, soft delete, backup frequency, and retention should be considered together as part of a data-protection strategy.
- **Validation matters after deployment:** Successful resource deployment does not automatically mean that backup protection is configured correctly. Each stage should be verified.
- **Security must be considered during implementation:** Network access rules and administrative credentials require careful handling, especially when publishing project work publicly.
- **Screenshots provide useful implementation evidence:** Clear screenshots can demonstrate configuration decisions and successful deployment steps when documenting a cloud project.
- **Azure configurations can change:** Portal interfaces, available VM sizes, backup options, and service capabilities may change, so current Azure documentation should be checked when reproducing an older lab.
- **Production design requires additional controls:** A lab configuration is useful for learning, but production environments should apply least privilege, restricted network access, monitoring, alerting, recovery testing, and appropriate governance.

## Portfolio Summary

**Azure VM Backup & Data Protection**

Designed and implemented an Azure data-protection solution using Azure Virtual Machines, Virtual Network, NSG, Public IP, ARM templates, Azure Recovery Services Vault, and Azure Backup. Configured geo-redundant backup storage, 14-day soft-delete protection, and a daily VM backup policy with defined retention. The project demonstrates practical Azure administration, infrastructure-as-code, backup, recovery, and cloud data-protection skills.

## Author

**Lex**

Azure Cloud Engineering | Cloud Architecture | Cybersecurity

