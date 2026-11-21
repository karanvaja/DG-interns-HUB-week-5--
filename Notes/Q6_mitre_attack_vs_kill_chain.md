## Q6: MITRE ATT&CK vs Cyber Kill Chain (with Attack Mapping)

### This document explains the structure of MITRE ATT&CK (tactics, techniques, sub-techniques), contrasts it with the Cyber Kill Chain, and maps five common attack scenarios (drawn from Weeks 2–4 topics: phishing, malware, social engineering, credential attacks) to both frameworks.

## 1. MITRE ATT&CK Structure
* MITRE ATT&CK is a knowledge base of adversary behavior organized as a matrix of tactics (the "why") and techniques (the "how"), with sub-techniques providing granular detail .

| **Component** | **Definition** | **Example** |
|---|---|---|
| **Tactic** | The adversary's **tactical goal** — the reason for performing an action ("why") | **Credential Access** (steal credentials) |
| **Technique** | **How** an adversary achieves a tactical goal by performing an action | **OS Credential Dumping** (dump credentials to achieve Credential Access) |
| **Sub-technique** | A **more specific** description of the behavior at a lower level | **LSASS Memory** (dump credentials by accessing LSA Secrets) |
| **Procedure** | The **specific implementation** observed in the wild (e.g., using PowerShell to inject into `lsass.exe`) | APT uses Mimikatz via PowerShell |


* Key point: ATT&CK is behavior-centric and granular — it catalogs what the adversary does at each step, not just where they are in a linear sequence. It covers Enterprise, Mobile, and ICS matrices .

## 2. Cyber Kill Chain Structure
* The Cyber Kill Chain (Lockheed Martin) is a linear, seven-phase model describing the stages an attacker must complete to achieve an objective .

| **Phase** | **Description** |
|---|---|
| 1. **Reconnaissance** | Identify target information (employees, systems, vulnerabilities) |
| 2. **Weaponization** | Adapt malicious activity into a deliverable payload (malware + exploit) |
| 3. **Delivery** | Send the weaponized package (phishing email, malicious link) |
| 4. **Exploitation** | The payload acts on the system, exploiting a vulnerability and executing code |
| 5. **Installation** | Malware is installed on the target |
| 6. **Command & Control (C2)** | Malware communicates with the attacker's infrastructure |
| 7. **Actions on Objectives** | Attacker achieves their goal (data theft, ransomware, etc.) |


* Key point: The Kill Chain is phase-centric and linear — it describes where the attacker is in the intrusion sequence, with less granularity on specific behaviors.

## 3. Comparison: ATT&CK vs Cyber Kill Chain

| **Aspect** | **MITRE ATT&CK** | **Cyber Kill Chain** |
|---|---|---|
| **Structure** | Matrix of tactics × techniques × sub-techniques | Linear 7-phase sequence |
| **Granularity** | **High** — hundreds of techniques/sub-techniques | **Low** — 7 broad phases |
| **Focus** | **Behavior** ("what the adversary does") | **Phase** ("where the adversary is") |
| **Use case** | Detection engineering, threat hunting, alert triage, red teaming | Executive communication, high-level attack narrative, phase-based defense |
| **Flexibility** | Non-linear; techniques can repeat/overlap across tactics | Linear; assumes sequential progression |
| **Mapping to defenses** | Directly maps to detection rules (SIEM/EDR) | Maps to phase-specific controls (block delivery, detect C2) |

* Analogy: The Kill Chain is the chapter outline of an attack; ATT&CK is the detailed index of every action within those chapters.

## 4. Mapping 5 Attacks: Kill Chain Phase → ATT&CK Technique

* The following attacks are representative of topics covered in Weeks 2–4 (phishing, malware, social engineering, credential theft).


| **#** | **Attack Observed** | **Kill Chain Phase** | **ATT&CK Technique (ID)** |
|---|---|---|---|
| 1 | **Spearphishing email with malicious attachment** — targeted email delivers a weaponized Office document or executable to a specific user | **Delivery** → **Exploitation** | **Spearphishing Attachment** (T1566.001) |
| 2 | **Business Email Compromise (BEC) impersonation** — attacker impersonates an executive or vendor to trick finance into a wire transfer | **Delivery** → **Actions on Objectives** | **Impersonation** (T1656) / **Social Engineering: Impersonation** (T1684.001) |
| 3 | **Credential dumping after initial access** — attacker extracts password hashes from LSASS memory to move laterally | **Exploitation** → **Installation** → **Actions on Objectives** | **OS Credential Dumping: LSASS Memory** (T1003.001) |
| 4 | **Malicious macro execution** — user opens a document, enables macros, and code executes to download a payload | **Exploitation** → **Installation** | **User Execution: Malicious File** (T1204.002) / **Command and Scripting Interpreter** (T1059) |
| 5 | **Phishing link to credential harvesting page** — user clicks a link in a spoofed email and enters credentials on a fake login page | **Delivery** → **Exploitation** (credential capture) | **Phishing: Spearphishing Link** (T1566.002) / **Credentials from Password Stores** (T1555) |


## 5. Key Takeaways
* ATT&CK answers "how" (specific behaviors); Kill Chain answers "where" (phase in the intrusion).

* ATT&CK is the operational tool for detection engineers and SOC analysts — map alerts to techniques to build detection coverage .

* Kill Chain is the communication tool — useful for explaining an attack to management or non-technical stakeholders.

* They are complementary, not competing — a single attack spans multiple Kill Chain phases, each containing multiple ATT&CK techniques.

* For IOC/IOA work, ATT&CK's technique IDs provide the shared vocabulary for TTP-level detection (the top of the Pyramid of Pain from Q5).


