# TryHackMe: Cyber Kill Chain --- Writeup

**Room Link:** <https://tryhackme.com/room/cyberkillchainzmt>\
**Difficulty:** Easy\
**Estimated Time:** 45 mins\
**Tags:** Cyber Defence Frameworks, MITRE ATT&CK, Threat Intelligence

------------------------------------------------------------------------

## Overview

The Cyber Kill Chain framework, developed by Lockheed Martin in 2011, is
a military-inspired model used to identify and prevent cyber intrusions.
It breaks down an attack into seven sequential phases. This writeup
documents the answers and notes from the TryHackMe room.

------------------------------------------------------------------------

## Task 1: Introduction

**Notes:**

-   The term "kill chain" comes from the military (target identification
    → decision → attack → destruction).
-   The framework helps SOC Analysts, Threat Hunters, and Incident
    Responders understand adversary goals and identify missing security
    controls.
-   The 7 phases: Reconnaissance, Weaponization, Delivery, Exploitation,
    Installation, Command & Control (C2), and Actions on Objectives.

**Question 1:** Read the above.\
**Answer:** `No answer needed`

------------------------------------------------------------------------

## Task 2: Reconnaissance

**Notes:**

-   **Reconnaissance** is the research and planning phase where
    adversaries gather information about the target.
-   **OSINT** (Open-Source Intelligence) is a valuable piece of recon,
    gathering data from search engines, social media, forums, WHOIS,
    etc.
-   **Passive Recon:** No direct interaction with the target (e.g.,
    WHOIS, social media scraping).
-   **Active Recon:** Direct interaction (e.g., port scanning, banner
    grabbing, social engineering).
-   **Email Harvesting:** The process of obtaining email addresses from
    public/paid services for phishing attacks. Tools include
    `theHarvester`, `Hunter.io`, and the `OSINT Framework`.

**Question 1:** What is the name of the Intel Gathering Tool that is a
web-based interface to the common tools and resources for open-source
intelligence?\
**Answer:** `OSINT Framework`

**Question 2:** What is the definition for the email gathering process
during the stage of reconnaissance?\
**Answer:** `email harvesting`

------------------------------------------------------------------------

## Task 3: Weaponization

**Notes:**

-   **Weaponization** is turning raw information into actionable attack
    tools by crafting **malware** and **exploits** into a **payload**.
-   **Malware:** Software designed to damage, disrupt, or gain
    unauthorized access.
-   **Exploits:** Code that takes advantage of a vulnerability.
-   **Payload:** Malicious code the attacker runs on the system.
-   Tactics include creating infected Microsoft Office documents
    (macros), creating malicious worms, setting up C2 infrastructure,
    and creating backdoors.

**Question 1:** What is the term for automated scripts embedded in
Microsoft Office documents that can be used to perform tasks or
exploited by attackers for malicious purposes?\
**Answer:** `Macro`

------------------------------------------------------------------------

## Task 4: Delivery

**Notes:**

-   **Delivery** is the method used to transmit the payload to the
    target environment.
-   Methods include:
    -   **Phishing email:** Spear phishing or mass phishing with
        malicious links/attachments.
    -   **USB drops:** Physical delivery of infected USB drives in
        public areas.
    -   **Watering hole attacks:** Compromising a website frequently
        visited by a specific group to redirect them to malware.

**Question 1:** What do you call an attack targeting a specific group by
infecting their frequently visited website?\
**Answer:** `Watering hole attack`

------------------------------------------------------------------------

## Task 5: Exploitation

**Notes:**

-   **Exploitation** occurs when the attacker's code executes on the
    target system, taking advantage of a vulnerability.
-   Techniques: Malicious macro execution, Zero-day exploits, Known
    CVEs.
-   **Signs of exploitation:** Unexpected process spawns, registry
    changes, new services created, suspicious command-line arguments in
    logs.

**Question 1:** What is the term for a cyber attack that exploits a
software vulnerability that is unknown by software vendors?\
**Answer:** `Zero-day`

------------------------------------------------------------------------

## Task 6: Installation

**Notes:**

-   **Installation** is when the attacker installs a **persistent
    backdoor** to maintain access if the initial connection is lost or
    removed.
-   Methods of persistence:
    -   Installing a **web shell** on a web server (malicious ASP, PHP,
        JSP script).
    -   Installing a backdoor (e.g., using Metasploit).
    -   Creating/modifying Windows Services (MITRE ATT&CK T1543.003).
    -   Adding entries to the "run keys" in the Registry or Startup
        Folder.
-   Attackers also use **Timestomping** (modifying file timestamps) to
    evade forensic detection.

**Question 1:** What technique is used to modify file time attributes to
hide new or changes to existing files?\
**Answer:** `Timestomping`

**Question 2:** What malicious script can be planted by an attacker on
the web server to maintain access to the compromised system and enables
the web server to be accessed remotely?\
**Answer:** `Web shell`

------------------------------------------------------------------------

## Task 7: Command & Control

**Notes:**

-   **Command & Control (C2)** is the channel established between the
    compromised host and the attacker's server to remotely control the
    victim.
-   The infected host consistently "beacons" to the C2 server.
-   Common C2 channels:
    -   **HTTP/HTTPS (Port 80/443):** Blends malicious traffic with
        legitimate traffic to evade firewalls.
    -   **DNS:** The infected machine makes constant DNS requests (DNS
        Tunneling).
-   IRC is an older, outdated C2 channel that is easily detected.

**Question 1:** What is the C2 communication where the victim makes
regular DNS requests to a DNS server and domain which belong to an
attacker?\
**Answer:** `DNS Tunneling`

------------------------------------------------------------------------

## Task 8: Actions on Objectives (Exfiltration)

**Notes:**

-   **Actions on Objectives** is the final phase where the attacker
    achieves their original goals.
-   Actions include:
    -   Collecting credentials from users.
    -   Performing privilege escalation.
    -   Internal reconnaissance and lateral movement.
    -   Collecting and exfiltrating sensitive data.
    -   Deleting backups and shadow copies (e.g., to prepare for
        ransomware).
    -   Overwriting or corrupting data.

**Question 1:** What technology is included in Microsoft Windows that
can create backup copies or snapshots of files or volumes on the
computer, even when they are in use?\
**Answer:** `Shadow Copy`

------------------------------------------------------------------------

## Task 9: Practice Analysis

**Notes:**

-   **Scenario:** The Target data breach (Nov 27, 2013), where 40
    million credit/debit card accounts were stolen, resulting in an
    \$18.5 million settlement.
-   **Task:** Deploy the static site and map the provided 6 items to the
    correct Kill Chain phases.
-   **Mapping:**
    -   `spearphishing attachment` → **Delivery**
    -   `exploit public-facing application` → **Exploitation**
    -   `powershell` → **Installation**
    -   `dynamic linker hijacking` → **Installation** (often used for
        persistence)
    -   `fallback channels` → **Command & Control**
    -   `data from local system` → **Actions on Objectives**

**Question 1:** What is the flag after you complete the static site?\
**Answer:** `THM{7HR347_1N73L_12_4w35om3}`

------------------------------------------------------------------------

## Task 10: Conclusion

**Notes:**

-   The traditional Cyber Kill Chain (from 2011) is not perfect. It was
    designed to protect the network perimeter against malware.
-   It struggles to detect **Insider Threats**.
-   Modern threats use combined TTPs and bypass traditional detection.
-   It is recommended to use the Cyber Kill Chain alongside **MITRE
    ATT&CK** and the **Unified Kill Chain** for a comprehensive defense
    approach.

**Question 1:** Read the above.\
**Answer:** `No answer needed`
