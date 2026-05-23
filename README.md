# Wazuh Setup Writeup

## 📌 Overview

This writeup documents the setup and configuration of a **Wazuh SIEM lab environment** using the official Wazuh virtual machine image.

The goal of this lab is to deploy Wazuh, access the dashboard, connect it to the local network, and understand how Wazuh can be used for basic SOC monitoring and endpoint visibility.

---

## 🎯 Objectives

- Deploy the Wazuh virtual machine.
- Configure the network adapter.
- Access the Wazuh Dashboard from the browser.
- Identify the Wazuh server IP address.
- Understand the basic Wazuh lab architecture.
- Prepare the environment for future agent deployment and alert monitoring.

---

## 🧠 Lab Environment

| Component | Details |
|---|---|
| SIEM Platform | Wazuh |
| Deployment Type | Wazuh OVA Virtual Machine |
| Virtualization | VirtualBox |
| Network Mode | Bridged Adapter |
| Dashboard Access | Web Browser |
| Default Username | `admin` |
| Default Password | `admin` |

---

## 🛠️ Tools Used

- Wazuh
- VirtualBox
- Linux Terminal
- Web Browser
- Local Network

---

## 🏗️ Architecture

```text
+-------------------+          +-------------------+
|   Windows/Linux   |  Agent   |   Wazuh Server    |
|     Endpoint      | -------> | Manager + Indexer |
|                   |          |   + Dashboard     |
+-------------------+          +-------------------+
```

In this setup, the Wazuh server is deployed as a virtual machine.  
Endpoints can later be connected to the Wazuh server using Wazuh agents.

---

# ⚙️ Installation Steps

## 1. Download the Wazuh OVA Image

First, download the official Wazuh OVA virtual machine image from the Wazuh documentation:

```text
https://documentation.wazuh.com/current/deployment-options/virtual-machine/virtual-machine.html
```

---

## 2. Open VirtualBox

After downloading the OVA file, open **VirtualBox**.

<img width="1262" height="195" alt="VirtualBox opened" src="https://github.com/user-attachments/assets/a4cb3f74-eddc-41e4-a883-009ffc35320b" />

---

## 3. Import the Wazuh Virtual Machine

Click on the option to import or add the downloaded Wazuh OVA image.

<img width="780" height="506" alt="Import Wazuh OVA image" src="https://github.com/user-attachments/assets/f49d313e-0768-4714-8244-25da752a2ddb" />

---

## 4. Finish the Import Process

Click **Finish** and wait until the virtual machine import process is completed.

<img width="931" height="566" alt="Finish Wazuh VM import" src="https://github.com/user-attachments/assets/4e749090-e128-452f-93ef-9484c03f1d3e" />

---

## 5. Configure the Network Adapter

After importing the virtual machine, configure it to be reachable from your real/local network.

Go to:

```text
Settings → Network → Adapter 1
```

Change:

```text
Attached to: Bridged Adapter
```

This allows the Wazuh VM to get an IP address from the same network as your host machine.

<img width="600" height="447" alt="Configure bridged adapter" src="https://github.com/user-attachments/assets/b9478e86-1dde-4269-aa17-7a47e96884c2" />

---

## 6. Start the Wazuh Virtual Machine

Click **OK**, then start the virtual machine.

The default login credentials are displayed during startup.

<img width="804" height="671" alt="Wazuh VM startup credentials" src="https://github.com/user-attachments/assets/44c4f2dd-fa60-46ae-b7ad-48c490073a2e" />

Default credentials:

```text
Username: wazuh-user
Password: wazuh
```

Dashboard credentials:

```text
Username: admin
Password: admin
```

---

## 7. Find the Wazuh Server IP Address

After logging in, run the following command to identify the IP address of the Wazuh virtual machine:

```bash
ifconfig
```

Or:

```bash
ip a
```

Look for the IP address assigned to the active network interface.

<img width="798" height="689" alt="Find Wazuh IP address" src="https://github.com/user-attachments/assets/c3805f82-80b1-4bd9-b35f-94ead7e1be29" />

---

## 8. Access the Wazuh Dashboard

Open a browser from your host machine and visit:

```text
https://<WAZUH-SERVER-IP>
```

Example:

```text
https://192.168.1.50
```

Because Wazuh uses HTTPS with a self-signed certificate, the browser may show a security warning.  
Continue to the site.

<img width="1924" height="988" alt="Wazuh dashboard certificate page" src="https://github.com/user-attachments/assets/a6632f49-b04c-4ee5-8066-4095d02bbdb4" />

---

## 9. Login to Wazuh Dashboard

Use the default dashboard credentials:

```text
Username: admin
Password: admin
```

After logging in, the Wazuh dashboard should appear.

<img width="1917" height="988" alt="Wazuh dashboard home page" src="https://github.com/user-attachments/assets/3da5d73a-97cb-4bab-8de5-bd018ed7e03d" />

---
