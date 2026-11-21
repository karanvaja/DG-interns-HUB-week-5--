 ### Q1: Incident Response Lifecycle (NIST SP 800-61 Four-Phase Model)

###  The NIST SP 800-61 (Computer Security Incident Handling Guide) defines an incident response lifecycle with four phases. Below is the table of actions for each phase.

### Table: Actions in Each Phase

| **Phase** | **Purpose** | **Key Actions** |
|---|---|---|
| **1. Preparation** | Get ready before incidents happen | • Create IR policy, plan, and procedures<br>• Build and train CSIRT team<br>• Deploy SIEM, EDR, IDS/IPS, AV, firewalls<br>• Set up logging and monitoring<br>• Maintain asset inventory and network diagrams<br>• Prepare contact lists and communication plans<br>• Define severity levels and escalation paths<br>• Conduct tabletop exercises and drills<br>• Maintain backups and baselines |
| **2. Detection & Analysis** | Identify and confirm the incident | • Monitor SIEM, EDR, IDS alerts and user reports<br>• Triage alerts (false positive vs true positive)<br>• Validate and confirm the incident<br>• Determine incident type and severity<br>• Establish scope and impact<br>• Collect and preserve evidence (disk image, memory)<br>• Perform email header analysis, hash/URL reputation, sandbox analysis<br>• Extract IOCs and map to MITRE ATT&CK / Kill Chain<br>• Document findings and notify stakeholders |
| **3. Containment, Eradication & Recovery** | Stop spread, remove threat, restore operations | **Containment:**<br>• Isolate affected hosts<br>• Disable compromised accounts<br>• Block malicious IPs/domains/hashes<br>• Apply short-term and long-term containment<br><br>**Eradication:**<br>• Remove malware and persistence mechanisms<br>• Reset compromised credentials<br>• Patch vulnerabilities<br>• Verify no residual IOCs<br><br>**Recovery:**<br>• Restore from clean backups<br>• Reintroduce systems in monitored phases<br>• Validate functionality<br>• Increase monitoring for re-infection |
| **4. Post-Incident Activity** | Learn and improve | • Conduct lessons-learned meeting<br>• Document timeline and actions taken<br>• Identify root cause and gaps<br>• Update playbooks and detection rules<br>• Implement corrective actions<br>• Update risk register and asset inventory<br>• Improve training and awareness<br>• Retain evidence per policy |

### Quick Reference

| **Phase** | **Analyst Question** |
|---|---|
| Preparation | "Are we ready?" |
| Detection & Analysis | "Is this real, and how bad is it?" |
| Containment, Eradication & Recovery | "How do we stop it and recover?" |
| Post-Incident Activity | "What did we learn?" |

### Key Points

* The four phases are cyclical, not strictly linear.

* Preparation is the most important phase — it makes all other phases faster.

* Evidence preservation is critical during Detection & Analysis.

* Lessons Learned feeds improvements back into Preparation.



