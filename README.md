# SMB Brute Force Detection using Wazuh

## 📌 Project Overview

This project demonstrates the detection of an SMB brute-force attack in a controlled lab environment using Wazuh SIEM.

A Kali Linux machine was used to simulate SMB brute-force attempts against a Windows 11 victim system.  
The Windows system was configured with a Wazuh agent, which forwarded security logs to the Wazuh Manager for analysis and alerting.

The goal of this project is to showcase hands-on SOC skills such as attack simulation, log analysis, alert validation, and threat detection.


## 🏗️ Lab Architecture

## Lab Architecture & Network Diagram

The lab environment was built using VirtualBox with all machines connected to an internal network to ensure isolation from the host system.

### Network Details
- **Virtualization Platform**: VirtualBox  
- **Network Mode**: Internal Network  
- **Subnet**: 192.168.0.0/24  
- **All VMs on Same Subnet**: Yes  

### Virtual Machines
| VM Name          | Operating System | Role                         | IP Address     |
|------------------|------------------|------------------------------|----------------|
| Kali-Attacker    | Kali Linux       | SMB Brute-force attacker     | 192.168.0.3    |
| Windows-Victim   | Windows 11       | Victim / Log Source          | 192.168.0.4    |
| Wazuh-Manager    | Wazuh Server     | SIEM / Log Correlation       | 192.168.0.20   |
| Windows-SOC      | Windows 11       | SOC Analyst Workstation      | 192.168.0.10   |

### Log Flow
1. Kali Linux launches SMB brute-force attempts against the Windows victim.
2. Windows records authentication events in the Security Event Log.
3. Wazuh Agent forwards logs from the Windows victim to the Wazuh Manager.
4. Wazuh Manager correlates events and generates alerts.
5. Alerts are reviewed by the SOC analyst via the Wazuh Dashboard.

## Network Architecture Diagram

                 ┌────────────────────────────┐
                 │        Kali-Attacker       │
                 │  OS: Kali Linux            │
                 │  Role: Attacker            │
                 │  IP: 192.168.0.3           │
                 └──────────────┬─────────────┘
                                │
                                │ SMB Brute Force (NTLM)
                                │ TCP 445 / 139
                                ▼
        ┌──────────────────────────────────────────────┐
        │                Windows-Victim                │
        │  OS: Windows 11                              │
        │  Role: Victim                                │
        │  IP: 192.168.0.4                             │
        │                                              │
        │  Windows Security Events:                    │
        │   • Event ID 4625 – Failed Logon             │
        │   • Event ID 4624 – Successful Logon         │
        │                                              │
        │  Wazuh Agent Installed                       │
        └──────────────┬───────────────────────────────┘
                       │
                       │ 
                       │ (Wazuh Agent → Manager)
                       ▼
        ┌──────────────────────────────────────────────┐
        │                Wazuh Manager                 │
        │  OS: Wazuh Server                            │
        │  IP: 192.168.0.20                            │
        │                                              │
        │  • Log Ingestion                             │
        │  • Rule Correlation                          │
        │  • Alert Generation                          │
        └──────────────┬───────────────────────────────┘
                       │
                       │ Alerts & Dashboards
                       ▼
        ┌──────────────────────────────────────────────┐
        │                Windows-SOC                   │
        │  OS: Windows 11                              │
        │  Role: SOC Analyst Workstation               │
        │  IP: 192.168.0.10                            │
        │                                              │
        │  • Wazuh Dashboard                           │
        │  • Threat Hunting                            │
        │  • Log & Alert Analysis                      │
        └──────────────────────────────────────────────┘

---

## Network Configuration

* **Virtualization Platform**: VirtualBox
* **Network Mode**: Internal Network
* **Subnet**: 192.168.0.0/24
* **All VMs on Same Subnet**: Yes

---

## Attack & Detection Flow

1. Kali Linux initiates an SMB brute-force attack against the Windows victim (192.168.0.4).
2. Windows victim processes authentication attempts using NTLM.
3. Failed and successful logon events are recorded in Windows Security logs.
4. Wazuh Agent forwards logs to the Wazuh Manager (192.168.0.20).
5. Wazuh Manager analyzes logs and generates alerts.
6. SOC analyst monitors alerts and performs threat hunting via the Wazuh Dashboard on Windows-SOC (192.168.0.10).

---

## Lab Objective

Simulate SMB brute-force attacks and detect failed authentication attempts using Wazuh SIEM in a controlled lab environment.



## ⚙️ Tools & Technologies Used

## 🧪 Attack Simulation - SMB Brute-force

- **Target Machine**: Windows-Victim  
- **IP Address**: 192.168.0.4  
- **Service Attacked**: SMB  
- **Ports**: TCP 445, TCP 139  
- **Authentication Protocol**: NTLM

Before launching the attack, an Nmap scan was performed to verify that SMB ports were open on the target system.
nmap -p 139,445 192.168.0.4

<img width="822" height="260" alt="SMB-port-validation" src="https://github.com/user-attachments/assets/867226da-60ff-4b1c-aa3a-d2cb1a377b7e" />

<img width="1135" height="357" alt="SMB-attack-Kali" src="https://github.com/user-attachments/assets/67d50c19-d8e7-4f13-ad44-077f721d9af9" />

## 📊 Detection & Analysis (Wazuh)

## 🚨 Alerts & Logs Observed

## 🔐 Security Concepts Demonstrated

## 📸 Screenshots

## 🎯 Key Takeaways
