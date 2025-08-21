<div align="middle">
<img height="200" src="https://i.postimg.cc/TPt92ZmJ/Copy-of-s-Block.png" />
</div>

<div align="left"> <h3>Description</h3></div>

This project demonstrates the deployment and testing of a **Security Information and Event Management (SIEM)** system using *Wazuh*.  
The setup uses a **pre-built Wazuh OVA file** running inside a virtual machine, making it a quick and easy way to learn about Wazuh's monitoring and detection capabilities.</p>


<div align="left"> <h3>Objectives</h3></div>
⦁ Deployed Wazuh SIEM using an OVA file in a virtual environment.<br>
⦁ Configured network settings for agent–manager communication.<br>
⦁ Installed Wazuh agents on monitored endpoints (Windows).<br>
⦁ Generated and detected simulated security events.<br>
⦁ Analyzed and visualized security logs in the Wazuh Dashboard.<br>

<div align="left"> <h3>Tools & Technologies</h3></div>

| Tool / Technology        | Purpose |
|--------------------------|---------|
| **Wazuh OVA**            | Pre-configured SIEM with Wazuh Manager, OpenSearch, and Dashboard |
| **VMware Workstation**   | Virtualization platform for Wazuh VM |
| **Windows 11**           | Endpoint systems for Wazuh agents |
| **Wazuh Agent**          | Installed on endpoints to send logs/events |
| **Web Browser**          | For accessing the Wazuh Dashboard |

<div align="left"> <h3>Lab Archietecture</h3></div>

```bash
+--------------------+        +-------------------+       +-------------------+
|  Endpoint (Agent)  |  --->  |                   |       |                   |
|  Windows / Linux   |        |                   |       |                   |
+--------------------+        |                   |       |                   |
|   Wazuh Manager    |  <-->  |    OpenSearch /   |       |     Dashboard     |
+--------------------+        |     (OVA VM)      |       |                   |
|  Endpoint (Agent)  |  --->  |                   |       |                   |
+--------------------+        +-------------------+       +-------------------+
```
<div align="left"> <h3>Deployment Steps of Wazuh OVA</h3></div>

1. Downloaded the .ova from official Wazuh downloads section.
2. Imported the .ova into **VMware**.
3. Allocated at least **4GB RAM**, **2 CPU cores**, and **50GB storage**.
4. Configured **Bridged Networking** or **NAT with Port Forwarding**.

<div align="left"><h3> Integration</h3></div>

**Virustotal**

⦁ Integrated the Virustotal API for Malware Scanning.</br>

```bash
<integration>
  <name>virustotal</name>
  <api_key>API_KEY</api_key> <!-- Your Virustotal API Key -->
  <group>syscheck</group>
  <alert_format>json</alert_format>
</integration>
```
Using this command line in *.ossec.conf* file.
<div align="left"> <h3>Starting Wazuh in Virtual Machine</h3></div>
1. Booted up the Virtual Machine and log in with default credentials.<br>
2. Found the Virtual Machine IP using:<br></br>
 
 ```bash
   ip addr
 ```

<img width="" height="300" alt="Screenshot (1)" src="https://github.com/user-attachments/assets/0a465c63-b572-4da0-8da7-70a986fb6d7e" /><br>
*Preview of Virtual Machine ip addr command.* 
<div align="left"> <h3>Accessing of Wazuh Dashboard</h3></div>
⦁ Opened a browser and navigated to:<br></br>

 ```bash
  https://<WAZUH_VM_IP>
  ```
⦁ Login's with default credentials and change the password.

<img width="" height="300" alt="Screenshot 2025-08-17 191051" src="https://github.com/user-attachments/assets/0d515e2f-abc4-448b-bef9-0565340406d0" />

<div align="left"> <h3>Installation of Wazuh Agents</h3></div>

⦁ From the dashboard: **Agents Deployed new agent**.<br>
⦁ Followed the installer instructions for **Windows**<br>

 ```bash
 .\wazuh-agent-4.12.0-1.msi /q WAZUH_MANAGER="10.0.0.2"
  ```
*Paste this in Windows Powershell.*
<div align="left"> <h3>Testing Detection</h3></div>
⦁ Running a port scan:<br></br>

   ```bash
  nmap -A <agent-ip>
  ```
⦁ Trying failed login attempts.<br>
⦁ Uploaded test malware samples.<br>
<div align="left"><h3>Overview</h3></div>
<img width="" height="300" alt="Screenshot 2025-08-17 221511" src="https://github.com/user-attachments/assets/d33b3f56-0b62-4ff2-9aea-493f68ae57ac" />

<div align="left"> <h3>Results</h3></div>
<img width="" height="300" alt="Screenshot 2025-08-17 221458" src="https://github.com/user-attachments/assets/06eaffac-69fe-4af8-ad6c-c90e556e6cb3" />

⦁ Wazuh successfully collected logs from endpoints.<br>
⦁ Detected simulated attacks like **port scanning** and **brute-force attempts**.<br>
⦁ Real-time alerts and dashboards displayed in the Wazuh interface.<br>

<div align="left"> <h3>File Integrity Monitoring</h3></div>
<img width="" height="300" alt="image" src="https://github.com/user-attachments/assets/ab31a78d-b5a3-4be7-beb4-76cf21e0d57b" /><br>

*Added this lines in ossec.conf to monitor the desired directories*<br>

<img width="" height="300" alt="Screenshot 2025-08-21 203532" src="https://github.com/user-attachments/assets/a1bae4ca-e9d2-48ab-872b-3b31525e722f" /><br>

*Created a Notepad File for realtime monitoring*<br>

<img width="" height="300" alt="Screenshot 2025-08-21 203551" src="https://github.com/user-attachments/assets/45044c8a-a35d-406e-9c37-9a9ffe2df23b" /><br>

*The **.txt** is visible in wazuh alert*<br>

<img width="" height="300" alt="Screenshot 2025-08-21 203620" src="https://github.com/user-attachments/assets/d8ab00b3-894d-450e-bbed-bd55574390c4" /><br>

*Made changes in **.txt** file*<br>

<img width="" height="300" alt="Screenshot 2025-08-21 203652" src="https://github.com/user-attachments/assets/91189be4-e00f-43ba-bb29-84640babac81" /><br>

*Wazuh showing the file has been modified and it's content under **syscheck.diff***<br>


*Disclaimer: Only use this in closed environment.* 
