# Project Overview – SIEM Lab with Elastic Stack

This document provides a high-level overview of the SIEM Lab project, including its goals, structure, and components.

---

## 🎯 Project Goal

Create a fully functional and secure SIEM (Security Information and Event Management) lab using Elastic Stack and Beats to simulate log collection, monitoring, and detection in a real-world environment.

---

## 🧰 Technologies Used

- **Elastic Stack (Elasticsearch + Kibana)**
- **Winlogbeat** (Windows event forwarding)
- **Filebeat** (Linux log forwarding)
- **Sysmon** (Advanced Windows event logging)
- **Ubuntu Server 22.04** (Elastic Stack server)
- **Windows Server 2019** (Active Directory Domain Services + DNS)
- **Windows 11 Client** (Domain-joined endpoint)
- **pfSense** (Planned – Firewall and network logging)

---

## 🛠️ Lab Topology

[Windows Server 2019]  →  [Ubuntu Server 22.04]  →  [Windows 11 Client]  
   (AD + DNS)              (Elastic Stack)           (Domain Joined)  

                             ↓  
               [Optional: pfSense Firewall]

---

## 🔐 Security Features Implemented

- TLS encryption between Elastic components
- User authentication for Kibana and Elasticsearch
- Encrypted saved objects with a custom encryption key

---

## 📚 Documentation Structure

| Document | Purpose |
|:---------|:--------|
| `01-lab-setup.md` | VM setup and network configuration |
| `02-elastic-stack.md` | Installation and security of Elastic Stack |
| `03-winlogbeat-sysmon.md` | Windows logging with Sysmon and Winlogbeat |
| `04-filebeat-ubuntu.md` | Linux log collection with Filebeat |
| `05-kibana-dashboards.md` | Dashboard creation for log visualization |
| `errors-and-fixes.md` | Troubleshooting issues encountered during setup |

---

## 🚀 Future Improvements

- Integrate pfSense for firewall log monitoring
- Simulate attack scenarios using Kali Linux
- Deploy Wazuh as a second SIEM phase

---

## 🏆 Final Note

This project demonstrates hands-on skills in cybersecurity, system administration, troubleshooting, and security monitoring — critical competencies for roles in SOCs and cybersecurity teams.
