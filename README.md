# Two-Tier Architecture Deployment in Microsoft Azure

## Watch me build the lab here:
https://www.loom.com/share/bbb0a8d0c484497bb17f1d65bb7eb652

## Overview

This lab demonstrates the deployment of a **two-tier architecture in Microsoft Azure** using **virtual machines, subnet segmentation, and controlled network access**. The environment is designed with a publicly accessible web tier and a privately secured database tier, following common cloud security and architecture best practices.

---

## Architecture Summary

The solution consists of two Ubuntu-based virtual machines deployed within a single Azure virtual network:

### Web Tier
- Publicly accessible via SSH
- Deployed in a dedicated subnet
- Acts as the entry point into the environment

### Database Tier
- No public IP address
- Accessible only from within the virtual network
- Deployed in a separate subnet for isolation

This separation ensures that backend resources are protected from direct public access.

---

## Resource Organization

All resources were deployed into a dedicated resource group:

- **Resource Group:** `RG-Lab-001`

This approach improves manageability and simplifies cleanup.

---

## Virtual Network Design

A custom virtual network was created with the following configuration:

- **Virtual Network:** `RG-Lab-001-VNet`
- **Address Space:** `172.16.0.0/16`

### Subnets

| Subnet Name       | Address Range       | Purpose        |
|------------------|---------------------|----------------|
| VM-Web-Subnet    | 172.16.1.0/24       | Web Tier       |
| VM-DB-Subnet     | 172.16.2.0/24       | Database Tier  |

Subnet segmentation enables tighter access control and reflects real-world production architectures.

---

## Web Server Virtual Machine

**VM Name:** `VM-Web-001`

**Configuration:**
- OS: Ubuntu Server (x64)
- Region: East US
- Size: 4 vCPUs, 16 GiB RAM
- Authentication: SSH public key
- Public IP: Enabled
- Inbound Access: SSH (port 22) allowed via NSG
- Auto-shutdown: Enabled

This VM serves as the externally accessible tier.

---

## Database Virtual Machine

**VM Name:** `DB-001`

**Configuration:**
- OS: Ubuntu Server
- Authentication: Username and password
- Public IP: Disabled
- Inbound Access: All public inbound ports disabled
- Subnet: VM-DB-Subnet
- Auto-shutdown: Enabled

The database VM is fully isolated from the public internet.

---

## Connectivity Validation

Validation steps were performed from the web server:

- ICMP (ping) to the database VM private IP succeeded
- SSH access from the web VM to the database VM succeeded
- Direct SSH access to the database VM from the public internet failed as expected

These results confirm proper network segmentation and access controls.

---

## Security Principles Applied

- Least privilege access
- Network segmentation
- Private backend infrastructure
- Minimal public exposure

The database tier can only be accessed from within the Azure virtual network.

---

## Conclusion

This lab successfully demonstrates how to deploy a **secure two-tier architecture in Azure** using virtual machines, virtual networks, and subnet isolation. The design mirrors common production patterns used in cloud environments to protect backend resources while allowing controlled access from an application tier.

---

## Skills Demonstrated

- Azure Virtual Machine deployment
- Virtual Network and subnet design
- Network Security Group configuration
- SSH authentication and access control
- Cloud security best practices
- Two-tier architecture design

---

## Future Enhancements

- Add Network Security Group rules to further restrict east-west traffic
- Replace password authentication with SSH keys for internal access
- Introduce a load balancer for the web tier
- Deploy a managed database service (Azure SQL / PostgreSQL)




