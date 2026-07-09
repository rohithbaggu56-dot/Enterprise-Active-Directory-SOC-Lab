# Enterprise Active Directory SOC Lab

<p align="center">

![Platform](https://img.shields.io/badge/Platform-VirtualBox-blue?style=for-the-badge)
![Windows Server](https://img.shields.io/badge/Windows_Server-2022-0078D6?style=for-the-badge)
![Windows 10](https://img.shields.io/badge/Windows-10-0078D6?style=for-the-badge)
![Ubuntu](https://img.shields.io/badge/Ubuntu-22.04-E95420?style=for-the-badge)
![Wazuh](https://img.shields.io/badge/SIEM-Wazuh-0265A1?style=for-the-badge)
![Sysmon](https://img.shields.io/badge/Sysmon-Enabled-success?style=for-the-badge)
![PowerShell](https://img.shields.io/badge/PowerShell-Automation-5391FE?style=for-the-badge)

</p>

> ### 📌 Project Highlights
>
> - Built a complete enterprise Active Directory lab from scratch.
> - Integrated Windows telemetry with Wazuh SIEM and Sysmon.
> - Simulated Password Spraying, SMB Enumeration, Kerberoasting, and AS-REP Roasting.
> - Validated detections using Threat Hunting and MITRE ATT&CK mapping.
> - Demonstrated end-to-end SOC investigation workflow in a controlled lab.


# 📌 Project Overview

This project demonstrates the deployment, monitoring, and security validation of an enterprise-style Active Directory environment. A Windows Server 2022 Domain Controller, Windows 10 workstation, Kali Linux attacker, and Ubuntu-based Wazuh SIEM were built inside VirtualBox to simulate how a Security Operations Center (SOC) detects and investigates Active Directory attacks. After deploying the environment, multiple attack techniques were executed from Kali Linux and validated through Wazuh dashboards, Threat Hunting, and MITRE ATT&CK mapping.


# 🎯 Project Objectives

- Build an enterprise Active Directory environment from scratch.
- Configure Organizational Units (OUs), users, groups, and service accounts.
- Join Windows endpoints to the Active Directory domain.
- Centralize Windows and Sysmon logs using Wazuh.
- Simulate common Active Directory attack techniques.
- Detect attacker activity through MITRE ATT&CK mapping.
- Perform threat hunting using collected telemetry.
- Gain practical SOC Analyst experience in detection and investigation.

---

# 🏗️ Lab Architecture

The environment consists of a Domain Controller, a domain-joined Windows workstation, a Kali Linux attack machine, and a Wazuh SIEM server for centralized monitoring.

<p align="center">
<img width="1536" height="1024" alt="enterprise-lab-architecture" src="https://github.com/user-attachments/assets/f0fc3e01-8161-47dd-80ba-4d5b9c5715a0" />
</p>


# 🛠️ Technologies Used

| Category | Technologies |
|-----------|--------------|
| Operating Systems | Windows Server 2022, Windows 10, Ubuntu Server, Kali Linux |
| Identity Management | Active Directory Domain Services (AD DS) |
| SIEM | Wazuh |
| Endpoint Monitoring | Sysmon |
| Log Collection | Windows Event Logs |
| Scripting | PowerShell |
| Attack Simulation | NetExec, Impacket |
| Detection Framework | MITRE ATT&CK |
| Virtualization | VirtualBox |

---

# ⚙️ Active Directory Deployment

The first phase of the project focused on building a functional Active Directory environment capable of supporting enterprise authentication, centralized identity management, and attack simulation.

The deployment included:

- Installing Active Directory Domain Services (AD DS)
- Promoting Windows Server 2022 to a Domain Controller
- Creating the **corp.local** domain
- Joining a Windows 10 workstation to the domain

<p align="center">
<img width="466" height="480" alt="windows10-domain-join" src="https://github.com/user-attachments/assets/566e8341-bd4b-490b-ad24-84ceb71d663c" />
</p>


# 👥 User Account Configuration

To better simulate a real enterprise environment, Organizational Units (OUs), departmental users, security groups, administrative accounts, and service accounts were created instead of relying on the default Active Directory objects.

The environment includes users across multiple departments including **IT, HR, Finance, and Sales**, along with dedicated administrative and service accounts used later during attack simulations.

<p align="center">
<img width="877" height="960" alt="user-account-properties" src="https://github.com/user-attachments/assets/a390881e-4a30-4b4e-83c8-96c91a6035d6" />
</p>


# ⚡ Active Directory Automation

PowerShell automation was used to provision enterprise users, administrative accounts, service accounts, and Kerberos test accounts.

This also included configuring:

- Service Principal Names (SPNs) for Kerberoasting simulations
- An AS-REP roastable user account
- Enterprise account provisioning through PowerShell automation

<p align="center">

<img width="1860" height="1080" alt="powershell-ad-automation" src="https://github.com/user-attachments/assets/11b3e31d-ca68-4d05-8bb7-b1ad568ac1fc" />

<br><br>

<img width="1896" height="1069" alt="configure-spn-service-account" src="https://github.com/user-attachments/assets/45a6f3fe-d744-44b8-927e-023ad1da05cb" />

<br><br>

<img width="1896" height="1069" alt="configure-asreproast-user" src="https://github.com/user-attachments/assets/58317ebc-3a3b-46df-ae00-41b86aaab2e2" />

</p>

---
# 🛡️ Wazuh Integration

The Windows 10 workstation and Windows Server 2022 Domain Controller were onboarded to Wazuh for centralized log collection and endpoint monitoring. Security, System, Application, and Sysmon events were continuously collected, enabling visibility into authentication activity, process execution, and Active Directory operations throughout the lab.

<p align="center">
<img width="1901" height="1080" alt="wazuh-agents" src="https://github.com/user-attachments/assets/b5de83f6-c587-4814-9e1b-8424b2340bf5" />
</p>

>NOTE: Both Windows endpoints successfully connected to Wazuh and continuously forwarding telemetry for monitoring and threat detection.

---

# ⚔️ Active Directory Attack Simulation

After validating the environment, multiple attack techniques were executed from Kali Linux to simulate common Active Directory attacks. Each activity generated endpoint telemetry that was collected by Wazuh for investigation and mapped to the MITRE ATT&CK framework.

The simulations included:

- Password Spraying
- SMB Enumeration
- Kerberoasting
- AS-REP Roasting
- PowerShell-based Active Directory Enumeration

---
## SMB Enumeration

NetExec was used to authenticate against the Domain Controller and enumerate Active Directory users and accessible SMB shares.

<p align="center">

<img width="1915" height="1048" alt="netexec-user-enumeration" src="https://github.com/user-attachments/assets/17c6b0ee-a91f-4ea7-8898-928dac665e71" />

<br><br>

<img width="1839" height="1048" alt="netexec-smb-share-enumeration" src="https://github.com/user-attachments/assets/ff9b5309-5fa6-408f-a403-b08baa1a96c9" />

</p>

---

## Kerberoasting

A Service Principal Name (SPN) account was configured and targeted using Impacket to request Kerberos service tickets, simulating a Kerberoasting attack.

<p align="center">
<img width="1869" height="1038" alt="kerberoasting-service-ticket-request" src="https://github.com/user-attachments/assets/b2eaafb7-18fb-459d-bca9-93d27717ff50" />
</p>

---

## AS-REP Roasting

A user account with Kerberos pre-authentication disabled was configured and targeted using Impacket to simulate an AS-REP Roasting attack.

<p align="center">
<img width="1869" height="1038" alt="asreproast-ticket-extraction" src="https://github.com/user-attachments/assets/442ea0a7-18b4-40c0-94ee-c57a6c1db03d" />
</p>

---

# 📊 Detection & Investigation

Following the attack simulations, Wazuh successfully collected and correlated Windows Security and Sysmon events generated throughout the lab. Authentication activity, process creation, PowerShell execution, and Active Directory events were centralized for investigation through Wazuh dashboards and MITRE ATT&CK mapping.


## 🧠 MITRE ATT&CK Dashboard

The MITRE ATT&CK dashboard provided a high-level view of the techniques observed during the attack simulations, helping correlate Windows events with attacker behavior rather than isolated log entries.

<p align="center">
<img width="1920" height="1080" alt="mitre-attack-weekly-dashboard" src="https://github.com/user-attachments/assets/e390499f-aa2a-485b-8f2a-02dc86b71e3b" />
</p>


## 🔍 Threat Hunting Dashboard

The Threat Hunting dashboard provided centralized visibility into authentication activity, endpoint events, and alerts generated across the monitored environment.

<p align="center">
<img width="1905" height="1080" alt="threat-hunting-weekly-dashboard" src="https://github.com/user-attachments/assets/09933156-ff6e-419c-b5d6-81005ae9cadb" />
</p>

---

# 🕵️ Investigation Examples

Daily investigations were performed using both the Threat Hunting and MITRE ATT&CK views to validate detections generated during the attack simulations.

### MITRE ATT&CK Investigation

<p align="center">
  
<img width="1891" height="1080" alt="mitre-attack-events-day-01" src="https://github.com/user-attachments/assets/4e1083bb-ed6b-4c4a-826b-92a9ff6968e8" />

<br><br>

<img width="1911" height="1080" alt="mitre-attack-events-day-02" src="https://github.com/user-attachments/assets/633794d8-7aa4-4f73-b2a8-ee64559e0372" />

</p>

### Threat Hunting Investigation

<p align="center">
  
<img width="1891" height="1071" alt="threat-hunting-events-day-01" src="https://github.com/user-attachments/assets/b9c7b6e9-0944-4bf0-8476-9ff8e0b4c7c5" />

<br><br>

<img width="1911" height="1080" alt="threat-hunting-events-day-02" src="https://github.com/user-attachments/assets/4ac6ef73-3c6c-48a9-85d9-2a850fcb9fdf" />

</p>

---

# 📈 Detection Highlights
Throughout the lab, Wazuh successfully detected and correlated security events generated by the simulated Active Directory attacks.

Key observations included:

- Windows authentication monitoring
- Kerberos-related activity
- PowerShell execution
- Account discovery
- Process creation
- Active Directory event collection
- MITRE ATT&CK mapping
- Centralized threat hunting using Wazuh

### MITRE ATT&CK Techniques Observed

- **T1087** – Account Discovery
- **T1135** – Network Share Discovery
- **T1018** – Remote System Discovery
- **T1059.001** – PowerShell
- **T1078** – Valid Accounts
- **T1558.003** – Kerberoasting
- **T1558.004** – AS-REP Roasting

---

# 💡 Skills Demonstrated

This project provided hands-on experience with technologies and workflows commonly used by SOC Analysts and Blue Team defenders.

### Active Directory

- Active Directory Domain Services (AD DS)
- Domain Controller Deployment
- Organizational Unit (OU) Administration
- User & Service Account Management
- PowerShell Automation

### Security Operations

- Wazuh SIEM Administration
- Sysmon Configuration
- Windows Event Log Analysis
- Threat Hunting
- Alert Investigation
- Security Event Correlation

### Attack Simulation

- SMB Enumeration
- Password Spraying
- Kerberoasting
- AS-REP Roasting
- Active Directory Reconnaissance

### Security Frameworks

- MITRE ATT&CK
- Windows Security Logging
- Endpoint Monitoring

---

# 📚 Key Takeaways

Building this lab provided practical experience beyond simply deploying Active Directory. It strengthened my understanding of how enterprise identity infrastructure, attack simulation, and security monitoring work together in a modern Security Operations Center (SOC).

Some of the key lessons from this project include:

- Deploying and managing an enterprise Active Directory environment.
- Automating administrative tasks using PowerShell.
- Simulating common Active Directory attack techniques.
- Investigating authentication and endpoint telemetry using Wazuh.
- Understanding how Windows security events map to MITRE ATT&CK techniques.
- Developing practical investigation skills from a defender's perspective.

---

# 🚀 Future Improvements

Potential enhancements for this lab include:

- Deploy additional Windows client systems.
- Configure Group Policy Objects (GPOs).
- Simulate lateral movement scenarios.
- Integrate Microsoft Sentinel for multi-SIEM monitoring.
- Deploy BloodHound for Active Directory analysis.
- Develop custom Wazuh detection rules.
- Add Sigma rules for additional detection coverage.

---

## 🤝 Connect With Me

If you'd like to discuss this project or connect professionally, feel free to reach out.

- [**LinkedIn**](https://www.linkedin.com/in/rohithbaggu/)
- [**TryHackMe**](https://tryhackme.com/p/rohithbaggu56)

---

## ⭐ Support

If you found this project useful or interesting, consider giving it a ⭐. Feedback and suggestions are always welcome.
