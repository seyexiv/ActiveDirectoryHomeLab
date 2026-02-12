# Active Directory Lab Using VirtualBox




## Overview

This lab was designed to simulate a real-world Active Directory environment and provide hands-on experience with configuring a Windows-based network. The goal of this project is to build a detailed understanding of how Active Directory functions while also exploring key Windows networking concepts.

Using Oracle VirtualBox, I created a controlled environment consisting of two virtual machines: one running Windows Server 2019 as the Domain Controller and one running Windows 10 as the client machine.

---

## Objectives




During this lab, the following tasks were completed:

- Set up Active Directory Domain Services (AD DS) from scratch.
- Create a dedicated Domain Admin account for secure administration.
- Deploy a DHCP server to dynamically assign IP addresses.
- Create an Organizational Unit (OU) to improve user management and organization.
- Configure Routing and Remote Access (RRAS) to simulate a corporate intranet.
- Configure the Network Interface Cards (NICs) to provide both internal communication and internet connectivity.
- Automate mass user creation using PowerShell by generating over 1000 users.
- Log into the Windows 10 client using one of the newly created domain accounts.

---

## Technologies Used

- Oracle VirtualBox  
- Windows Server 2019 ISO  
- Windows 10 ISO  
- PowerShell  

---

## IP Addressing Plan

To ensure proper communication between the Domain Controller and the client machine, the lab was built using a dedicated internal subnet.

| Device | Role | IP Address | Subnet Mask | Default Gateway | DNS Server |
|--------|------|------------|-------------|----------------|------------|
| DC | Domain Controller | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 | 192.168.10.10 |
| CLIENT | Domain Client | DHCP Assigned | 255.255.255.0 | 192.168.10.1 | 192.168.10.10 |

This setup ensures that all domain authentication and name resolution requests from the client are handled through the Domain Controller.

---




## VirtualBox Network Configuration

A dual NIC configuration was used for the Domain Controller to simulate a realistic enterprise network design.

### Domain Controller (DC) NIC Setup

#### NIC 1 (External / Internet Access)
- **Adapter Type:** NAT  
- **Purpose:** Allows the Domain Controller to access the internet for updates and external connectivity.

#### NIC 2 (Internal / Private Network)
- **Adapter Type:** Internal Network  
- **Purpose:** Allows communication between the Domain Controller and client machine within an isolated environment.

### Windows 10 Client (CLIENT) NIC Setup

- **Adapter Type:** Internal Network  
- **Purpose:** Ensures the client communicates only inside the lab environment and receives its IP configuration from the Domain Controller via DHCP.

This configuration provides an isolated internal network while still allowing the Domain Controller to connect externally through NAT.

---

## Installation

### Create Virtual Machines in VirtualBox

- Open Oracle VirtualBox and click **New**.
- Name the first machine **DC** and select Microsoft Windows as the type and Windows (64-bit) as the version.
- Assign at least **2GB RAM** and create a virtual hard disk of at least **50GB**.
- Repeat the process for the Windows 10 VM and name it **CLIENT**.

---

### Installing the Operating Systems and Initial Setup

After creating the virtual machines, I attached the ISO files and installed both operating systems. The installation process was straightforward, but Windows Server 2019 required additional setup to ensure administrative access.

During the installation:

- Install Windows Server 2019 using the on-screen instructions.
- Create an administrator account with a strong password since the account will have elevated permissions.

---





## Integrating Active Directory Domain Services

After booting into Windows Server 2019, I opened **Server Manager** and installed the **Active Directory Domain Services (AD DS)** role.

---





## Crafting a Domain Admin Account

To create a dedicated Domain Admin account:

- Open **Active Directory Users and Computers**
- Right-click the Users container or OU and select **New > User**
- Create the account and assign a strong password
- Add the account to the **Domain Admins** group

---

## DHCP Configuration Details

To allow the Windows 10 client machine to receive IP configuration automatically, the **DHCP Server** role was installed and configured on the Domain Controller.

### DHCP Setup Steps

- Install the DHCP role via Server Manager
- Authorize the DHCP server inside Active Directory
- Create and activate a DHCP scope







This ensures the client machine receives an IP address dynamically and automatically uses the Domain Controller for DNS resolution.

---
