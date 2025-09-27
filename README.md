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

<div align="left"><h3> Integration</h3></div>

<ins>***Virustotal***</ins>

⦁ Integrated the *Virustotal API* for Malware Detection.</br>

```
https://www.virustotal.com/gui/my-apikey
```
Get your *Virustotal API* from here.

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

⦁ Wazuh successfully collected logs from endpoints.<br>
⦁ Real-time alerts and dashboards displayed in the Wazuh interface.<br>

<div align="left"> <h3>File Integrity Monitoring</h3></div>

File Integrity Monitoring `FIM` in Wazuh is a powerful feature designed to detect unauthorized changes to files and directories - crucial for maintaining system integrity and spotting potential security breaches.<br>

<img width="" height="323" alt="Screenshot 2025-08-22 021704" src="https://github.com/user-attachments/assets/f1712bb3-d177-4e6f-b860-3a95eadb4d0d" /><br>

Dashboard of File Integrity Monitoring.<br>

#

<img width="" height="347" alt="Screenshot (8)" src="https://github.com/user-attachments/assets/189ffc36-7dc3-4276-9325-087e422e0a62" /><br>

```bash
<directories check_all="yes" report_changes="yes" realtime="yes">C:\Users\swast\Downloads</directories>
```

Added this lines in **ossec.conf** to monitor the desired directories.<br>

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
<div align="left"> <h3>IT Hygiene</h3></div>

<ins>*Dashboard*</ins>

<img width="" height="323" alt="Screenshot 2025-09-22 023437" src="https://github.com/user-attachments/assets/9cd30c78-5245-4473-9022-5f208f3d838f" /><br>

Wazuh IT Hygiene dashboard visualizes endpoint *OS*, *packages*, *processes*, and *hardware* details for real-time system health insights.<br>

#

<ins>*System | OS*</ins>

<img width="" height="323" alt="Screenshot 2025-09-22 023634" src="https://github.com/user-attachments/assets/8bf53c85-1f98-4038-b530-4599a2d0042c" /><br>

Wazuh system section summarizes host *OS*, *platform*, and *architecture* details to support endpoint hygiene and configuration tracking.<br>

<ins>*System | Hardware*</ins>

<img width="" height="323" alt="Screenshot 2025-09-22 023646" src="https://github.com/user-attachments/assets/1e228494-a7e7-428d-ab8f-1e4e704dd383" /><br>

This Wazuh IT Hygiene dashboard highlights endpoint hardware specs - showing *CPU model*, *core count*, and *memory usage* for the **`MSI`** host running an **AMD Ryzen 7 4700U**.<br>

#

<ins>*Software | Packages*</ins>

<img width="" height="323" alt="Screenshot 2025-09-22 023656" src="https://github.com/user-attachments/assets/398cb77f-240a-4f7f-8ace-04e251ff743b" /><br>

This Wazuh Software dashboard catalogs `69` installed packages by vendor and type, spotlighting **Microsoft** as the dominant contributor to the system’s software inventory.<br>

<ins>*Software | Windows KBs*</ins>

<img width="" height="323" alt="Screenshot 2025-09-22 023709" src="https://github.com/user-attachments/assets/8ca93549-5de7-4c47-ac9f-23feeca65bc1" /><br>

<img width="" height="323" alt="Screenshot 2025-09-22 023718" src="https://github.com/user-attachments/assets/1cde4fbe-46a7-4e75-acd0-a2e046320b51" /><br>

Wazuh tracks **Windows KBs** *{Knowledge Base}* updates, visualizing the most and least common patches across endpoints to support effective vulnerability and compliance management.<br>

#

<ins>*Processes*</ins>

<img width="" height="323" alt="Screenshot 2025-09-22 023729" src="https://github.com/user-attachments/assets/958f4fbd-2d91-46e9-bf17-55717728df16" /><br>

Wazuh process section visualizes top processes and start times to support anomaly detection and endpoint hygiene.<br>

<img width="" height="323" alt="Screenshot 2025-09-22 023745" src="https://github.com/user-attachments/assets/a1ae90ee-bc67-45d5-8a6c-9a577a6ce1cb" /><br>

Lists active processes per agent with *PID*, *parent PID*, and *command-line* details for forensic and performance analysis.<br>

<img width="" height="345" alt="Screenshot (11)" src="https://github.com/user-attachments/assets/d7178c28-676b-43f4-9a9f-a245e3c812e5" /><br>

This Wazuh Processes dashboard surfaces the top running executables and their start times, helping track system activity and detect anomalies like persistent or suspicious processes. Windows Task Manager and Wazuh process logs correlate ***svchost.exe*** activity, aiding validation and threat investigation.<br>

#

<ins>*Network | Addresses*</ins>

<img width="" height="323" alt="Screenshot 2025-09-22 023916" src="https://github.com/user-attachments/assets/d2393499-61c6-46c0-a2d2-d5f99175e72a" /><br>

<img width="" height="323" alt="Screenshot 2025-09-22 023925" src="https://github.com/user-attachments/assets/82df6098-9ee9-4b64-a725-0f56ebee3ec9" /><br>

This Wazuh Networks dashboard maps active interfaces and IP configurations, revealing `14` unique network addresses across *Wi-Fi*, *loopback*, and *virtual adapters* for the monitored host.<br>

<ins>*Network | Interfaces*</ins>

<img width="" height="323" alt="Screenshot 2025-09-22 024005" src="https://github.com/user-attachments/assets/0c5b6049-b69b-464a-ab35-f53b9388d4c6" /><br>

<img width="" height="323" alt="Screenshot 2025-09-22 024040" src="https://github.com/user-attachments/assets/f547ec7f-1897-408c-9469-92d0c353731e" /><br>

Wazuh interface section details *interface names*, *types*, *MTU values*, and *MAC* addresses to support network diagnostics and hygiene tracking.<br>

<ins>*Network | Protocols*</ins>

<img width="" height="323" alt="Screenshot 2025-09-22 024021" src="https://github.com/user-attachments/assets/e0ed995a-a135-4416-8953-dccf9f7858be" /><br>

Wazuh system section visualizes *DHCP* metrics and interface configurations to assess protocol hygiene and network accessibility.<br>

<img width="" height="323" alt="Screenshot 2025-09-22 024031" src="https://github.com/user-attachments/assets/e7bcd074-763a-42ad-9d88-33217864981b" /><br>

Lists *DHCP status*, *interface names*, *types*, and *metrics* per agent to support network configuration audits and hygiene tracking.<br>

<ins>*Network | Services*</ins>

<img width="" height="323" alt="Screenshot 2025-09-22 024050" src="https://github.com/user-attachments/assets/cab07ce9-434c-48cb-99c3-dd0602eef9c5" /><br>

Wazuh system section visualizes *source ports*, *transport protocols*, and *process activity* to uncover traffic patterns and potential threats.<br>

<img width="" height="323" alt="Screenshot 2025-09-22 024100" src="https://github.com/user-attachments/assets/d9b55aa3-006f-4075-a794-c6e46f8f71a7" /><br>

Lists agent-level network connections with source *IPs*, *ports*, *protocols*, and initiating processes for hygiene audits and anomaly detection.<br>

<ins>*Network | Traffic*</ins>

<img width="" height="323" alt="Screenshot 2025-09-22 024109" src="https://github.com/user-attachments/assets/4265f77f-433a-4170-87bd-b723d8159545" /><br>

Wazuh system section visualizes destination *ports*, *transport protocols*, and *process-level* traffic to uncover usage patterns and potential risks.<br>

<img width="" height="323" alt="Screenshot 2025-09-22 024120" src="https://github.com/user-attachments/assets/a7878f56-ba33-496a-ad39-58888eeebe3b" /><br>

Lists destination *IPs*, *ports*, *transport types*, and *initiating processes* per agent to support traffic audits and hygiene validation.<br>

<img width="" height="323" alt="Screenshot 2025-09-22 023033" src="https://github.com/user-attachments/assets/6cba24d2-6c40-497a-813c-91a2f4cfa3aa" /><br>

The traffic section is not enabled by default, we have to configure it manually by doing some changes in Wazuh Manager. We have to change the following line to.<br>

```xml
<ports all="no">yes</ports>
```

<img width="" height="323" alt="Screenshot 2025-09-22 023047" src="https://github.com/user-attachments/assets/c17effec-09d6-4f14-b5f5-fb3e64420433" /><br>

```xml
<ports all="yes">yes</ports>
```

After changing the ***no*** to ***yes*** in Wazuh Manager.<br>

<img width="" height="323" alt="Screenshot 2025-09-22 023057" src="https://github.com/user-attachments/assets/2b5bb8c7-61a9-4474-a8ae-3718a6532338" /><br>

Then we have to, restart the Wazuh Mananger to make traffic section visible.

---

In this video, I walk you through essential IT hygiene practices using Wazuh, a powerful open-source security platform. Whether you're managing endpoints, monitoring logs, or enforcing compliance, good hygiene is the backbone of a secure infrastructure - and Wazuh makes it actionable.
[***Youtube***](https://youtu.be/InprtVmPQxo?si=UHiuESRIPSMgR0uo)

#

<div align="left"> <h3>Reporting</h3></div>

We can generate the report of desired event can be seen under reporting section and could be deleted or downloaded in **PDF** format. 

> [!NOTE]
> The sample report has been uploaded under the [***Report***](https://github.com/swastiksagar/wazuhlabproject/tree/main/Report) folder of file section in the wazuhlabproject repositories<br>
##
<img width="" height="323" alt="Screenshot 2025-08-21 203726" src="https://github.com/user-attachments/assets/dc280f49-0f8e-41bb-b6c9-fdbd42bb7645" /><br>
<img width="" height="323" alt="Screenshot 2025-08-21 203845" src="https://github.com/user-attachments/assets/270ccfe8-059a-4a6a-9a4e-061c56ff00d6" /><br>
