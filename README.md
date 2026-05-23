# Wazuh Setup Writeup

## 📌 Overview

This writeup documents the setup and configuration of a Wazuh SIEM lab environment.  
The goal of this lab is to deploy Wazuh, connect an endpoint agent, collect security events, and understand how Wazuh can be used for SOC monitoring and incident detection.

---

## 🎯 Objectives

- Install and configure Wazuh.
- Access the Wazuh Dashboard.
- Deploy a Wazuh Agent on an endpoint.
- Verify log collection from the endpoint.
- Generate test alerts.
- Understand basic SOC monitoring workflow using Wazuh.

---

## 🧠 Lab Environment

| Component | Details |
|---|---|
| SIEM Platform | Wazuh |
| Wazuh Server OS | Ubuntu / Debian / Kali / VM |
| Endpoint OS | Windows / Linux |
| Virtualization | VirtualBox / VMware / Cloud VM |
| Network Mode | NAT / Bridged / Host-only |
| RAM | 4 GB / 8 GB / 16 GB |
| CPU | 2 vCPU / 4 vCPU |
| Disk | 50 GB+ |

---

## 🛠️ Tools Used

- Wazuh
- Wazuh Dashboard
- Wazuh Agent
- Linux Terminal
- Windows Event Viewer
- PowerShell / Bash
- VirtualBox / VMware

---

## 🏗️ Architecture

```text
+-------------------+          +-------------------+
|   Windows/Linux   |  Agent   |   Wazuh Server    |
|     Endpoint      | -------> | Manager + Indexer |
|                   |          |   + Dashboard     |
+-------------------+          +-------------------+
```
---

## Start Installation

after download the OVA file from this link : https://documentation.wazuh.com/current/deployment-options/virtual-machine/virtual-machine.html
++++Run VirtualBox
    <img width="1262" height="195" alt="image" src="https://github.com/user-attachments/assets/a4cb3f74-eddc-41e4-a883-009ffc35320b" />
    <br>
++++Then add the image here:
    <br>
    <img width="780" height="506" alt="image" src="https://github.com/user-attachments/assets/f49d313e-0768-4714-8244-25da752a2ddb" />
    <br>
++++Click Finish and wait until finish
    <br>
    <img width="931" height="566" alt="image" src="https://github.com/user-attachments/assets/4e749090-e128-452f-93ef-9484c03f1d3e" />
    <br>
