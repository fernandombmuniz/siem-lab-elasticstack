# Lab Setup – SIEM Lab with Elastic Stack

This guide describes the complete setup of the lab environment for the SIEM project, including the virtual machines (VMs) and their roles.

---

## 🎯 Objective

Create a controlled virtualized environment simulating a real-world network for log collection, monitoring, and detection using Elastic Stack and Beats.

---

## 🧰 Requirements

- VMware Workstation (or other virtualization platform)
- At least 16 GB RAM (recommended 24 GB)
- At least 120 GB disk space
- Internet connection for package downloads
- ISO images:
  - Ubuntu Server 22.04
  - Windows Server 2019
  - Windows 11 Pro
  - pfSense (optional at this stage)

---

## 🛠️ Lab Topology

[Windows Server 2019]  --->  [Ubuntu Server 22.04]  --->  [Windows 11 Client]
    (AD + DNS)               (Elastic Stack)               (Domain Joined)

                            [Optional: pfSense Firewall]


Each machine will send security event logs to the Ubuntu Server running Elastic Stack.

---

## 🖥️ Virtual Machine Configuration

### Ubuntu Server – Elastic Stack

- **OS**: Ubuntu Server 22.04 LTS
- **vCPU**: 2
- **RAM**: 6 GB
- **Disk**: 50 GB
- **Network**: NAT or Host-Only (with Internet access)
- **Role**: Elastic Stack server (Elasticsearch + Kibana)

### Windows Server 2019 – Domain Controller

- **OS**: Windows Server 2019 Standard
- **vCPU**: 2
- **RAM**: 4 GB
- **Disk**: 40 GB
- **Network**: Same network as Ubuntu Server
- **Role**: Active Directory Domain Services (AD DS) + DNS

### Windows 11 – Client Machine

- **OS**: Windows 11 Pro
- **vCPU**: 2
- **RAM**: 4 GB
- **Disk**: 40 GB
- **Network**: Same network as Domain Controller
- **Role**: Domain-joined workstation, log generation

### pfSense (Optional – Future Stage)

- **OS**: pfSense latest stable release
- **vCPU**: 1
- **RAM**: 1 GB
- **Disk**: 20 GB
- **Network**: Bridged or isolated segment
- **Role**: Network firewall and syslog source

---

## 📋 Initial Setup Steps

1. Install VMware Workstation (or similar).
2. Create the VMs following the specifications above.
3. Install Ubuntu Server 22.04 and update packages.
4. Install Windows Server 2019 and configure AD DS and DNS.
5. Install Windows 11 and join it to the domain.
6. Verify network communication between all VMs (using ping).

---

## ⚡ Tips and Best Practices

- Enable VMware Tools (or similar guest additions) for improved performance.
- Set static IP addresses, especially for the Domain Controller.
- Use VM snapshots after critical configurations.
- Start with NAT network configuration; pfSense integration will come later.

---

## 🚀 Next Step

Proceed to [02 – Installing and Securing the Elastic Stack](02-elastic-stack.md) to set up Elasticsearch and Kibana.

