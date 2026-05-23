# Wazuh Setup Writeup - Part 1: Installation and Agent Deployment

## 📌 Overview

This writeup documents the setup and configuration of a **Wazuh SIEM lab environment** using the official Wazuh virtual machine image.

The goal of this lab is to deploy Wazuh, access the dashboard, configure the network, connect an endpoint agent, and prepare the environment for basic SOC monitoring and endpoint visibility.

---

## 🎯 Objectives

- Deploy the Wazuh virtual machine using VirtualBox.
- Configure the Wazuh VM network adapter.
- Access the Wazuh Dashboard from a browser.
- Identify the Wazuh server IP address.
- Deploy a Wazuh agent on a Linux endpoint.
- Verify that the agent is active.
- Prepare the lab for future alert generation and investigation.

---

## 🧠 Lab Environment

| Component | Details |
|---|---|
| SIEM Platform | Wazuh |
| Deployment Type | Wazuh OVA Virtual Machine |
| Virtualization | VirtualBox |
| Network Mode | Bridged Adapter |
| Endpoint OS | Debian Linux |
| Dashboard Access | Web Browser |
| Wazuh Server IP | `192.168.1.19` |
| Dashboard Username | `admin` |
| Dashboard Password | `admin` |

> Note: Default credentials should be changed in a real environment.

---

## 🛠️ Tools Used

- Wazuh
- VirtualBox
- Debian Linux
- Linux Terminal
- Web Browser
- Local Network

---

## 🏗️ Architecture

```text
+-------------------+          +-------------------+
|   Linux Endpoint  |  Agent   |   Wazuh Server    |
|     Debian VM     | -------> | Manager + Indexer |
|                   |          |   + Dashboard     |
+-------------------+          +-------------------+
```

In this lab, the Wazuh server is deployed as a virtual machine.  
The endpoint is connected to the Wazuh server using a Wazuh agent.

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

After importing the virtual machine, configure it to be reachable from the local network.

Go to:

```text
Settings → Network → Adapter 1
```

Change the network mode to:

```text
Attached to: Bridged Adapter
```

Using **Bridged Adapter** allows the Wazuh VM to receive an IP address from the same network as the host machine.

<img width="600" height="447" alt="Configure bridged adapter" src="https://github.com/user-attachments/assets/b9478e86-1dde-4269-aa17-7a47e96884c2" />

---

## 6. Start the Wazuh Virtual Machine

Click **OK**, then start the virtual machine.

The default login credentials are displayed during startup.

<img width="804" height="671" alt="Wazuh VM startup credentials" src="https://github.com/user-attachments/assets/44c4f2dd-fa60-46ae-b7ad-48c490073a2e" />

Default VM credentials:

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

After logging in to the Wazuh VM, run one of the following commands to identify the IP address:

```bash
ifconfig
```

Or:

```bash
ip a
```

Look for the IP address assigned to the active network interface.

<img width="798" height="689" alt="Find Wazuh IP address" src="https://github.com/user-attachments/assets/c3805f82-80b1-4bd9-b35f-94ead7e1be29" />

In this lab, the Wazuh server IP address is:

```text
192.168.1.19
```

---

## 8. Access the Wazuh Dashboard

Open a browser from the host machine and visit:

```text
https://<WAZUH-SERVER-IP>
```

Example:

```text
https://192.168.1.19
```

Because Wazuh uses HTTPS with a self-signed certificate, the browser may show a security warning.  
Continue to the website manually.

<img width="1924" height="988" alt="Wazuh dashboard certificate warning" src="https://github.com/user-attachments/assets/a6632f49-b04c-4ee5-8066-4095d02bbdb4" />

---

## 9. Login to the Wazuh Dashboard

Use the default dashboard credentials:

```text
Username: admin
Password: admin
```

After logging in, the Wazuh dashboard should appear.

<img width="1917" height="988" alt="Wazuh dashboard home page" src="https://github.com/user-attachments/assets/3da5d73a-97cb-4bab-8de5-bd018ed7e03d" />

---

# 🖥️ Agent Deployment

## 10. Deploy a Wazuh Agent

After logging in to the dashboard, click on **Deploy new agent**.

<img width="591" height="240" alt="Deploy new Wazuh agent" src="https://github.com/user-attachments/assets/1a3f5bb9-08d2-4f35-a9c5-cd1d383cf871" />

---

## 11. Select the Endpoint Operating System

Choose the operating system of the endpoint where the Wazuh agent will be installed.

In this lab, the endpoint is a Debian-based Linux machine, so I selected:

```text
Linux
```

<img width="1878" height="671" alt="Select Linux agent" src="https://github.com/user-attachments/assets/ca036b4d-abe2-4b5c-bfd5-ecb96d4effeb" />

---

## 12. Configure the Agent Settings

Configure the agent using the Wazuh server IP address and an agent name.

Example configuration:

```text
Wazuh Manager IP: 192.168.1.19
Agent Name: debian-server
Agent Group: default
```

<img width="1874" height="748" alt="Configure Wazuh agent settings" src="https://github.com/user-attachments/assets/3eb3e73c-9751-4024-a49a-a5a77322c981" />

---

## 13. Install the Agent on the Endpoint

After selecting the correct settings, Wazuh generates an installation command.

Copy the generated command and run it on the endpoint machine.

Example:

```bash
wget https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.14.5-1_amd64.deb && sudo WAZUH_MANAGER='192.168.1.19' WAZUH_AGENT_NAME='debian-server' dpkg -i ./wazuh-agent_4.14.5-1_amd64.deb
```

<img width="1872" height="161" alt="Wazuh agent installation command" src="https://github.com/user-attachments/assets/5c6ce0ae-70da-4d5f-aeaa-a58d254822f9" />

---

## 14. Start and Enable the Wazuh Agent

After installing the agent, start and enable the Wazuh agent service.

```bash
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```

To verify the service status:

```bash
sudo systemctl status wazuh-agent
```

<img width="1855" height="246" alt="Start Wazuh agent service" src="https://github.com/user-attachments/assets/00475c2a-5b65-4f4b-ba18-1919fe843a9c" />

---

## 15. Verify the Agent Status

After completing the installation and starting the service, go back to the Wazuh dashboard.

The agent should appear as **Active**.

<img width="1909" height="523" alt="Active Wazuh agent" src="https://github.com/user-attachments/assets/9bd069ec-bdf7-43bb-a1d1-c64dabcef945" />

---

# ✅ Results

At the end of this part:

- The Wazuh virtual machine was successfully imported.
- The VM network adapter was configured in Bridged Adapter mode.
- The Wazuh server received an IP address from the local network.
- The Wazuh Dashboard was accessed from the browser.
- A Linux endpoint was connected using the Wazuh agent.
- The agent appeared as active in the dashboard.

---

# 🔍 SOC Analyst Notes

This setup is the foundation of a basic SOC home lab.

From a SOC analyst perspective, Wazuh can help with:

- Collecting endpoint logs.
- Monitoring Linux and Windows systems.
- Detecting suspicious authentication activity.
- Monitoring file integrity.
- Viewing alerts from a central dashboard.
- Mapping security events to MITRE ATT&CK techniques.
- Practicing alert triage and investigation workflows.

---

# 🧾 Troubleshooting

| Issue | Possible Cause | Fix |
|---|---|---|
| Dashboard does not open | Wrong IP address | Check the Wazuh server IP using `ip a` or `ifconfig` |
| Browser shows HTTPS warning | Self-signed certificate | Continue manually to the website |
| VM does not get an IP address | Wrong network mode | Use Bridged Adapter |
| Agent does not appear | Agent service not started | Run `sudo systemctl start wazuh-agent` |
| Agent is disconnected | Wrong Wazuh manager IP | Verify the manager IP inside the agent configuration |
| Installation shows hostname warning | Hostname not mapped in `/etc/hosts` | Add the hostname to `/etc/hosts` |

---

# 📚 Lessons Learned

- Wazuh can be quickly deployed using the official OVA image.
- Bridged Adapter mode makes the Wazuh server reachable from the local network.
- The Wazuh dashboard is accessed through HTTPS.
- Wazuh agents are used to collect endpoint logs and send them to the manager.
- An active agent means the endpoint is ready to generate logs and alerts.
- This lab can be extended into a complete SOC monitoring environment.

---

# 🔜 Part 2: Working with Wazuh Alerts

In the next part, I will focus on using Wazuh from a SOC analyst perspective.

Part 2 will cover:

- Navigating the Wazuh dashboard.
- Understanding Wazuh alerts.
- Generating failed login alerts.
- Investigating authentication events.
- Testing File Integrity Monitoring.
- Reviewing alert severity and rule IDs.
- Mapping alerts to MITRE ATT&CK.
- Writing a small SOC investigation report.

---

# 🧠 Conclusion

This lab demonstrated how to deploy Wazuh using VirtualBox, access the Wazuh Dashboard, and connect a Linux endpoint using the Wazuh agent.

The environment is now ready for log collection, alert generation, and SOC-style investigation practice.
