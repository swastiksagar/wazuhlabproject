<div align="middle">
<img height="200" src="https://i.postimg.cc/TPt92ZmJ/Copy-of-s-Block.png" />
</div>

<div align="left"> <h3>Description</h3></div>

This project demonstrates the deployment and testing of a **Security Information and Event Management** `SIEM` system using Wazuh. The setup uses a pre-built **Wazuh OVA** file running inside a virtual machine, making it a quick and easy way to learn about Wazuh's monitoring and detection capabilities.</p>

<div align="left"> <h3>Objectives</h3></div>

⦁ Deployed Wazuh `SIEM` using an `OVA` file in a virtual environment.<br>
⦁ Configured network settings for agent–manager communication.<br>
⦁ Installed Wazuh agents on monitored endpoints.<br>
⦁ Generated and detected simulated security events.<br>
⦁ Analyzed and visualized security logs in the Wazuh Dashboard.<br>

<div align="left"> <h3>Tools & Technologies</h3></div>

| Tool / Technology        | Purpose |
|--------------------------|---------|
| **Wazuh OVA**            | Pre-configured SIEM with Wazuh Manager, and Dashboard |
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
|   Wazuh Manager    |  <-->  |     (OVA VM)      |       |     Dashboard     |
+--------------------+        |                   |       |                   |
|  Endpoint (Agent)  |  --->  |                   |       |                   |
+--------------------+        +-------------------+       +-------------------+
```
<div align="left"> <h3>Deployment Steps of Wazuh OVA</h3></div>

⦁ Downloaded the `.ova` from official Wazuh [**Downloads**](https://documentation.wazuh.com/current/deployment-options/virtual-machine/virtual-machine.html) section.<br>
⦁ Imported the `.ova` into **VMware**.<br>
⦁ Allocated at least **8GB RAM**, **2 CPU cores**, and **50GB storage**.<br>
⦁ Configured **Bridged Networking** or **NAT with Port Forwarding**.<br>


<div align="left"> <h3>Starting Wazuh in Virtual Machine</h3></div>

<img width="" height="323" alt="Screenshot 2025-08-31 061146" src="https://github.com/user-attachments/assets/d52f9878-1446-4af3-8fa5-446e779f4b7e" /><br>

<img width="" height="327" alt="Screenshot 2025-09-17 084733" src="https://github.com/user-attachments/assets/d9ec29bd-4428-4240-83ca-813b1f2a4c2b" /><br>


Booting up the Virtual Machine.<br>

#

<img width="" height="323" alt="Screenshot 2025-08-31 061411" src="https://github.com/user-attachments/assets/a6e89191-958b-4416-a7e9-28614a817105" /><br>

Log in with Default Credentials.<br>

`Username:`
```
wazuh-user
```
`Password:`
```
wazuh
```

#

Found the Virtual Machine IP using:<br>

```bash
   ip addr
```
<img width="" height="348" alt="Screenshot (8)" src="https://github.com/user-attachments/assets/19cbca14-78a9-45eb-aafd-db46f5b49d12" /><br>

<div align="left"> <h3>Testing Connection</h3></div>

⦁ Running a ping scan:<br>

```bash
  ping <agent-ip>
```
<img width="" height="329" alt="Screenshot 2025-09-01 045943" src="https://github.com/user-attachments/assets/f131249f-f8f6-4cac-a20e-eda860216f74" /><br>

Ping return `0%` Loss the Wazuh IP is reachable and responsive.

<div align="left"> <h3>Accessing of Wazuh Dashboard</h3></div>

⦁ Opened a *browser* and navigated to:<br>

```bash
  https://<WAZUH_VM_IP>
```

<img width="" height="323" alt="Screenshot 2025-09-20 225259" src="https://github.com/user-attachments/assets/7cc5bef8-3901-40d9-885b-d53fbba94a62" /><br>

<img width="" height="323" alt="Screenshot 2025-09-20 225310" src="https://github.com/user-attachments/assets/8eda7604-54ee-43d7-8898-3a4bc8984895" /><br>

Then the browser *Google Chrome, Edge* displayed the `Your connection isn't private` page.<br>
*Clicked on Advanced -> Continue to website(unsafe).*<br>

<img width="" height="323" alt="Screenshot 2025-08-22 030624" src="https://github.com/user-attachments/assets/4e566e1c-3407-4b36-b554-7baa67e1d195" /><br>

⦁ Login's with default credentials and changed the password.<br>

`Username:`
```
admin
```
`Password:`
```
admin
```

<div align="left"> <h3>Installation of Wazuh Agents</h3></div>

<img width="" height="323" alt="Screenshot 2025-09-01 042019" src="https://github.com/user-attachments/assets/0f29552c-9b41-4509-b250-8639d259944a" /><br>

<img width="" height="323" alt="Screenshot 2025-09-17 085142" src="https://github.com/user-attachments/assets/f5c75b73-d061-4251-b181-a4c55c8b65b5" /><br>

From the dashboard: **Deployed new agent**.<br>
Followed the installer instructions for **Windows**<br>

```powershell
Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.12.0-1.msi -OutFile $env:tmp\wazuh-agent; msiexec.exe /i $env:tmp\wazuh-agent /q WAZUH_MANAGER='10.22.137.106' WAZUH_AGENT_NAME='Windows-Swastik'
```

```bash
 .\wazuh-agent-4.12.0-1.msi /q WAZUH_MANAGER="10.22.137.106"
```
Pasted this in Windows Powershell.<br>

#

<img width="" height="345" alt="Screenshot (9)" src="https://github.com/user-attachments/assets/d9edefdd-38fa-4c84-aa26-59f1df4db7e3" /><br>

***GUI*** of a Wazuh Agent.

<div align="left"><h3>Overview</h3></div>

<img width="" height="288" alt="Screenshot 2025-08-17 221511" src="https://github.com/user-attachments/assets/d33b3f56-0b62-4ff2-9aea-493f68ae57ac" /><br>

Overview Dashboard of Wazuh.

#

<img width="" height="322" alt="Screenshot 2025-08-31 061821" src="https://github.com/user-attachments/assets/50f670ce-9a62-415d-bab3-cd70ac653b7e" /><br>

The Configuration Assessment dashboard provides the benchmarks to scan and monitor endpoint for security misconfigurations, ensuring compliance with security best practices.

<div align="left"> <h3>Results</h3></div>

<img width="" height="287" alt="Screenshot 2025-08-17 221458" src="https://github.com/user-attachments/assets/06eaffac-69fe-4af8-ad6c-c90e556e6cb3" /><br>

Wazuh successfully collected logs from endpoints. Real-time alerts and dashboards displayed in the Wazuh interface.<br>

<div align="left"> <h3>File Integrity Monitoring</h3></div>

File Integrity Monitoring `FIM` in Wazuh is a powerful feature designed to detect unauthorized changes to files and directories - crucial for maintaining system integrity and spotting potential security breaches.<br>

<img width="" height="323" alt="Screenshot 2025-08-22 021704" src="https://github.com/user-attachments/assets/f1712bb3-d177-4e6f-b860-3a95eadb4d0d" /><br>

Dashboard of File Integrity Monitoring.<br>

#

<img width="" height="347" alt="Screenshot (8)" src="https://github.com/user-attachments/assets/189ffc36-7dc3-4276-9325-087e422e0a62" /><br>

```bash
<directories check_all="yes" report_changes="yes" realtime="yes">C:\Users\swast\Downloads</directories>
```

Added this lines in Wazuh agent **ossec.conf** to monitor the desired directories.<br>

#

<img width="" height="323" alt="Screenshot 2025-08-21 203532" src="https://github.com/user-attachments/assets/a1bae4ca-e9d2-48ab-872b-3b31525e722f" /><br>

Created a Notepad file for realtime monitoring.<br>

#

<img width="" height="323" alt="Screenshot 2025-08-21 203551" src="https://github.com/user-attachments/assets/45044c8a-a35d-406e-9c37-9a9ffe2df23b" /><br>

The entry of **.txt** is visible in wazuh alert.<br>

#

<img width="" height="311" alt="Screenshot 2025-08-21 203620" src="https://github.com/user-attachments/assets/d8ab00b3-894d-450e-bbed-bd55574390c4" /><br>

Made some text changes in **.txt** file.<br>

#

<img width="" height="323" alt="Screenshot 2025-08-21 203652" src="https://github.com/user-attachments/assets/91189be4-e00f-43ba-bb29-84640babac81" /><br>

Wazuh showed the file has been modified and it's content under **syscheck.diff** in event section.<br>

#

<img width="" height="323" alt="Screenshot 2025-08-22 021639" src="https://github.com/user-attachments/assets/36bb743b-f8ee-480e-ada8-7b02d39f775e" /><br>

The Logs of file changes of desired directories are visible in Event section.<br>

<div align="left"><h3>Malware Detection</h3></div>

Configured Wazuh to send file hashes or suspicious files to **VirusTotal** for scanning against multiple antivirus engines.
> [!CAUTION]
> The following content includes a known malware source. Proceed with extreme caution.

<img width="" height="323" alt="Screenshot 2025-08-26 065955" src="https://github.com/user-attachments/assets/29c4ced9-a80c-4fbc-a368-a6c816cee07c" /><br>

Dashboard of Malware Detection.<br>

#

<img width="" height="323" alt="Screenshot 2025-09-17 063558" src="https://github.com/user-attachments/assets/f298e935-ae6b-4bc0-847e-82938d3ddfb8" /><br>

```xml
<integration>
  <name>virustotal</name>
  <api_key>API_KEY</api_key> <!-- Your Virustotal API Key -->
  <group>syscheck</group>
  <alert_format>json</alert_format>
</integration>
```
Added this *.xml* line in **ossec.conf** on Wazuh Manager.<br>

<ins>***Virustotal***</ins>

⦁ Integrated the *Virustotal API* for Malware Detection.</br>

```
https://www.virustotal.com/gui/my-apikey
```
Get your *Virustotal API* from here.

#

<img width="" height="323" alt="Screenshot 2025-08-26 065856" src="https://github.com/user-attachments/assets/83d76169-04cb-497f-83f7-dc09f10ef28b" /><br>

Downloaded **Madman.exe**<br>
Downloaded the malware from this [***source***](https://github.com/Da2dalus/The-MALWARE-Repo) for testing.

#

<img width="" height="323" alt="Screenshot 2025-08-26 070007" src="https://github.com/user-attachments/assets/83d58116-34fb-40ee-b6fd-9180273901d8" /><br>

Wazuh was successfully detected and alerted that **Madman.exe** as a virus.

#

<img width="" height="323" alt="Screenshot 2025-08-26 070022" src="https://github.com/user-attachments/assets/3d4014e5-1550-4232-9701-6ece478ec0ab" /><br>

Wazuh provided the virustotal scanned link in the details section of the event. The malware got detected as malicious on `36` engines in virustotal website.

```http
https://www.virustotal.com/gui/file/17d81134a5957fb758b9d69a90b033477a991c8b0f107d9864dc790ca37e6a23/detection/f-17d81134a5957fb758b9d69a90b033477a991c8b0f107d9864dc790ca37e6a23-1754894123
```

#

---

In this video, I walk you through essential [*IT hygiene*](./ithygiene.md) practices using Wazuh, a powerful open-source security platform. Whether you're managing endpoints, monitoring logs, or enforcing compliance, good hygiene is the backbone of a secure infrastructure - and Wazuh makes it actionable.
[***Youtube***](https://youtu.be/InprtVmPQxo?si=UHiuESRIPSMgR0uo)

#

<div align="left"> <h3>Reporting</h3></div>

We can generate the report of desired event can be seen under reporting section and could be deleted or downloaded in **PDF** format. 

> [!NOTE]
> The sample report has been uploaded under the [***Report***](https://github.com/swastiksagar/wazuhlabproject/tree/main/Report) folder of file section in the wazuhlabproject repositories<br>
##
<img width="" height="323" alt="Screenshot 2025-08-21 203726" src="https://github.com/user-attachments/assets/dc280f49-0f8e-41bb-b6c9-fdbd42bb7645" /><br>
<img width="" height="323" alt="Screenshot 2025-08-21 203845" src="https://github.com/user-attachments/assets/270ccfe8-059a-4a6a-9a4e-061c56ff00d6" /><br>
