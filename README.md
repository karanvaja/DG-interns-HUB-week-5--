# Week 5 - Phishing, Malware Triage, Threat Intelligence & Incident Response

**Analyst:** [તમારું નામ અહીં લખો]
**Role Scope:** Tier 1 / Tier 2 SOC Analyst Workflow
**Date:** November 2026

---

## 📌 Project Overview
This repository contains the theoretical notes, hands-on lab writeups, malware analysis reports, and incident response documentation completed during Week 5. The focus of this week was on understanding email-borne threats, performing safe malware triage, mapping adversary behavior using MITRE ATT&CK, and writing formal incident reports.

---

## 📂 Folder Structure

```text
Week-5-Project/
│
├── README.md                  <-- You are here
├── Notes/                     <-- Theoretical Q&A Documents
│   ├── Q1_incident_response_lifecycle.md
│   ├── Q2_phishing_types_and_red_flags.md
│   ├── Q3_spf_dkim_dmarc.md
│   ├── ... (All Q1 to Q8 notes)
│
├── Writeups/                  <-- TryHackMe Lab Writeups
│   ├── THM_CyberKillChain_Writeup.md
│   ├── THM_PyramidOfPain_Writeup.md
│   ├── THM_IntroToCyberThreatIntel_Writeup.md
│   ├── THM_PhishingAnalysisFundamentals_Writeup.md
│   └── THM_ThreatIntelligenceTools_Writeup.md
│
├── Findings/                  <-- Screenshots and Evidence
│   ├── EICAR_Defender_Log.png
│   ├── Report1_ProcessTree.png
│   ├── Report1_NetworkIOCs.png
│   ├── T1059_Sysmon.png
│   ├── T1136_Event4720.png
│   ├── T1053_Sysmon.png
│   └── Navigator_Screenshot.png
│
├── Incident Report/           <-- Final Incident Report
│   └── Incident_Report_Remcos_RAT.md
│
├── Cheat Sheet/               <-- Quick Reference Guides
│   ├── IOC_Cheat_Sheet.md
│   └── Phishing_Red_Flag_Checklist.md
│
└── Reports/                   <-- Weekly Summary (PDF/PPT)
    ├── Week5_Report.pdf
    └── Week5_Presentation.pptx

```


## 📚 1. Theoretical Notes (Notes Folder)
* *ncident Response Lifecycle: Documented the NIST SP 800-61 four-phase model.

* Phishing Types: Detailed Spear Phishing, Whaling, Smishing, Vishing, and BEC.

* Email Authentication: Explained SPF, DKIM, and DMARC with pass/fail examples.

* Email Headers: Created a guide on how to read Received, Return-Path, and Authentication-Results.

* IOC vs IOA & Pyramid of Pain: Explained the difference between static indicators and behavioral TTPs.

* MITRE ATT&CK vs Kill Chain: Compared both frameworks and mapped attacks to techniques.

* Malware Analysis: Documented static vs dynamic analysis and sandbox safety rules.

* Incident Report Structure: Outlined severity levels, escalation paths, and report sections.

## 🧪 2. TryHackMe Labs (Writeups Folder)
* Completed the following rooms and documented step-by-step walkthroughs:

* Cyber Kill Chain: Learned the 7 phases of an attack.

* Pyramid of Pain: Understood the value of detecting TTPs over IOCs.

* Intro to Cyber Threat Intel: Learned CTI lifecycle, TLP, and STIX/TAXII.

* Phishing Analysis Fundamentals: Mastered raw email header and HTML body analysis.

* Threat Intelligence Tools: Hands-on with URLScan.io, Abuse.ch, and PhishTool.

## 🛠️ 3. Hands-On Tasks Completed
### Task 1: Phishing Analysis
* Analyzed 3 public phishing samples (PayPal Spoof, OKX Homograph, Visa Scam).

* Extracted headers, defanged URLs, and checked reputations on VirusTotal and URLScan.io.

* Verdict: All were malicious. The OKX sample used a Punycode/Homograph attack.

### Task 2: Safe Malware Triage
* EICAR Test: Successfully triggered the EICAR test file on Windows. Verified detection via Windows Defender Event ID 1116.

* Any.run Analysis: Analyzed two public reports:

* 1 madau.exe (Remcos RAT): Extracted C2 IPs (104.21.29.156, etc.) and mapped process injection (T1055).
* 2 alnahdacentre.com: Analyzed a drive-by compromise using obfuscated JavaScript.
### Task 3: ATT&CK Map
* Built a custom MITRE ATT&CK Navigator layer mapping techniques observed in Weeks 2-5 (e.g., T1059.001, T1136.001, T1189).

* Exported the layer as JSON and took a screenshot.

### Task 4: Atomic Red Team
*  Manually simulated 3 attack techniques:

* 1 T1059.001 (PowerShell): Verified via Sysmon Event ID 1.
* 2 T1136.001 (Local User): Verified via Windows Security Event ID 4720.
* 3 T1053.005 (Scheduled Task): Verified via Sysmon schtasks.exe execution.
* Detection Gap: Identified the absence of SIEM alerts for these specific events.

### Task 5: Incident Report
* Authored a formal 2-page incident report based on the Remcos RAT malware analysis.

* Documented timeline, IOCs, ATT&CK mapping, severity (High), and containment recommendations.

### Task 6: Cheat Sheets
* Created a 12-entry IOC Reference Table (Where to find it -> Tool to check it).

* Created a 1-page Phishing Red-Flag Checklist for daily triage.


## 🏁 Conclusion & Key Takeaways
* Week 5 provided a complete, end-to-end view of the SOC Analyst workflow. The most critical takeaway was the identification of detection gaps—specifically the lack of centralized logging (Sysmon/SIEM) for endpoint events like PowerShell execution and local user creation. Implementing the recommendations in the Incident Report will significantly improve the organization's security posture.