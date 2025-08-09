<div align="middle">
<img height="200" src="https://i.postimg.cc/TPt92ZmJ/Copy-of-s-Block.png" />
</div>

##  Description
This project demonstrates the deployment and testing of a **Security Information and Event Management (SIEM)** system using *Wazuh*.  
The setup uses a **pre-built Wazuh OVA file** running inside a virtual machine, making it a quick and easy way to learn about Wazuh's monitoring and detection capabilities.


##  Objectives
- Deployed Wazuh SIEM using an OVA file in a virtual environment.
- Configured network settings for agent–manager communication.
- Installed Wazuh agents on monitored endpoints (Windows).
- Generated and detected simulated security events.
- Analyzed and visualized security logs in the Wazuh Dashboard.

##  Tools & Technologies
| Tool / Technology        | Purpose |
|--------------------------|---------|
| **Wazuh OVA**            | Pre-configured SIEM with Wazuh Manager, OpenSearch, and Dashboard |
| **VMware Workstation**   | Virtualization platform for Wazuh VM |
| **Windows 11**           | Endpoint systems for Wazuh agents |
| **Wazuh Agent**          | Installed on endpoints to send logs/events |
| **Web Browser**          | For accessing the Wazuh Dashboard |

##  Lab Architecture
```
+--------------------+        +-------------------+         +----------------------+
|  Endpoint (Agent)  |  --->  |                   |         |                      |
|  Windows / Linux   |        |                   |         |                      |
+--------------------+        |                   |         |                      |
|   Wazuh Manager    |  <-->  |    OpenSearch /   |         |      Dashboard       |
+--------------------+        |     (OVA VM)      |         |                      |
|  Endpoint (Agent)  |  --->  |                   |         |                      |
+--------------------+        +-------------------+         +----------------------+
```
##  Deployment Steps of Wazuh OVA
1. Downloaded the .ova from official Wazuh downloads section.
2. Imported the .ova into **VMware**.
3. Allocated at least **4GB RAM**, **2 CPU cores**, and **50GB storage**.
4. Configured **Bridged Networking** or **NAT with Port Forwarding**.

###  Starting Wazuh VM
1. Booted up the VM and log in with default credentials.
2. Found the VM IP using:

   ```bash
   ip addr
   ```

###  Access of Wazuh Dashboard
- Opened a browser and navigated to:
 ```
  https://<WAZUH_VM_IP>
  ```
- Login's with default credentials and change the password.
###  Installation of Wazuh Agents
- From the dashboard: **Agents Deployed new agent**.
- Followed the installer instructions for **Windows**
- Example (Powershell):

 ```bash
 .\wazuh-agent-4.12.0-1.msi /q WAZUH_MANAGER="10.0.0.2"
  ```

###  Testing Detection
- Running a port scan:

   ```bash
  nmap -A <agent-ip>
  ```
- Trying failed login attempts.
- Uploaded test malware samples.

##  Results
- Wazuh successfully collected logs from endpoints.
- Detected simulated attacks like **port scanning** and **brute-force attempts**.
- Real-time alerts and dashboards displayed in the Wazuh interface.

*Disclaimer: Only use this in closed environment.* 
