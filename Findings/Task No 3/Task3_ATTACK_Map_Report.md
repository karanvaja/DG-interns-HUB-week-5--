# Task 3: MITRE ATT&CK Map Documentation

## Overview
This report documents a custom MITRE ATT&CK layer built using the ATT&CK Navigator. It maps the adversary techniques observed during the theoretical and hands-on exercises in Weeks 2 through 5. 

*   **Navigator Screenshot:** `Findings/Task No 3/Navigator_Screenshot.png`
*   **Navigator JSON Export:** `Findings/Task No 3/Navigator_Layer.json`

---

## Technique Documentation Table

| Technique ID | Technique Name | Why It Was Included | Week Observed | Log Source / Detection Rule |
| :--- | :--- | :--- | :--- | :--- |
| **T1566** | Phishing | Observed in phishing emails analyzed during the labs (delivering malicious links/attachments). | Week 5 | Email Gateway Logs, PhishTool, URLScan.io |
| **T1046** | Network Service Discovery | Scanners like Nmap were used to discover open ports and services on target machines. | Week 2/3 | Firewall Logs, IDS/IPS Alerts (e.g., Snort) |
| **T1110** | Brute Force | Attempting to guess credentials (SSH/RDP) was practiced using tools like Hydra. | Week 3 | Windows Event ID 4625 (Failed Logon), Linux Auth.log |
| **T1059.001** | PowerShell | Malicious scripts utilizing PowerShell were observed in the malware triage report (Report 1 / Report 2). | Week 5 | Sysmon Event ID 1 (Process Creation), Script Block Logging (Event ID 4104) |
| **T1136.001** | Create Local Account | Creating a backdoor user account for persistence was learned during privilege escalation. | Week 4 | Windows Event ID 4720 (User Account Created) |
| **T1189** | Drive-by Compromise | Observed in Report 2 (alnahdacentre.com) where a malicious website attempted to exploit the browser via obfuscated JS. | Week 5 | Proxy Logs, Browser History, EDR (msedge.exe child processes) |
| **T1055** | Process Injection | Observed in Report 1 (madau.exe) where the malware injected code into App.exe. | Week 5 | Sysmon Event ID 8 (CreateRemoteThread) or Event ID 10 (ProcessAccess) |

---

## Conclusion
By mapping these techniques in ATT&CK Navigator, we can visualize the attacker's behavior (TTPs) and identify detection gaps in our environment. This layer can be shared with the SOC team to prioritize the creation of new SIEM rules and EDR alerts.