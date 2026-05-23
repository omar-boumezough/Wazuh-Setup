# Wazuh Setup

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
- VirtualBox

---

## 🏗️ Architecture

```text
+-------------------+          +-------------------+
|   Windows/Linux   |  Agent   |   Wazuh Server    |
|     Endpoint      | -------> | Manager + Indexer |
|                   |          |   + Dashboard     |
+-------------------+          +-------------------+
