# TryHackMe: Threat Intelligence Tools — Complete Writeup

- **Room Link:** https://tryhackme.com/room/threatintelligencetools
- **Difficulty:** Easy
- **Estimated Time:** 60 mins
- **Tags:** Threat Intelligence, OSINT, SOC Level 1

---

## Overview

This room covers the concepts of Threat Intelligence and various open-source tools that are useful for security analysts. The learning objectives include understanding threat intelligence classifications, using URLScan.io, Abuse.ch, PhishTool, and Cisco Talos Intelligence.

---

## Task 1: Room Outline

**Notes:**

This room covers:

- Understanding the basics of threat intelligence & its classifications.
- Using UrlScan.io to scan for malicious URLs.
- Using Abuse.ch to track malware and botnet indicators.
- Investigating phishing emails using PhishTool.
- Using Cisco's Talos Intelligence platform for intel gathering.

**Question 1:** Read the description! Continue to the next task.
**Answer:** No answer needed

---

## Task 2: Threat Intelligence

**Notes:**

Threat Intelligence is the analysis of data and information using tools and techniques to generate meaningful patterns on how to mitigate against potential risks associated with existing or emerging threats.

**Classifications:**

| Type | Description |
|------|-------------|
| **Strategic Intel** | High-level intel that looks into the organisation's threat landscape and maps out risk areas based on trends, patterns, and emerging threats |
| **Technical Intel** | Looks into evidence and artefacts of attack used by an adversary (e.g., IPs, hashes) |
| **Tactical Intel** | Assesses adversaries' tactics, techniques, and procedures (TTPs) |
| **Operational Intel** | Looks into an adversary's specific motives and intent to perform an attack |

**Question 1:** I've read on Threat Intel and the classifications.
**Answer:** No answer needed

---

## Task 3: UrlScan.io

**Notes:**

- UrlScan.io is a free service developed to assist in scanning and analysing websites. It records the domains and IP addresses contacted, resources requested, and provides a snapshot of the web page.
- **Key areas of scan results:** Summary, HTTP, Redirects, Links, Behaviour, Indicators.
- You can view the page screenshot, domain registrar, and IP information.

**Scenario Questions (based on the TryHackMe screenshot):**

**Question 1:** What was TryHackMe's Cisco Umbrella Rank based on the screenshot?
**Answer:** `345612`

**Question 2:** How many domains did UrlScan.io identify on the screenshot?
**Answer:** `13`

**Question 3:** What was the main domain registrar listed on the screenshot?
**Answer:** `NAMECHEAP INC`

**Question 4:** What was the main IP address identified for TryHackMe on the screenshot?
**Answer:** `2606:4700:10::ac43:1b0a`

---

## Task 4: Abuse.ch

**Notes:**

Abuse.ch is a research project hosted by the Institute for Cybersecurity and Engineering at the Bern University of Applied Sciences in Switzerland. It tracks malware and botnets through several platforms:

| Platform | Purpose |
|----------|---------|
| **MalwareBazaar** | A resource for sharing malware samples |
| **Feodo Tracker** | Tracks botnet command and control (C2) infrastructure linked with Emotet, Dridex, and TrickBot |
| **SSL Blacklist** | Collects and provides a blocklist for malicious SSL certificates and JA3/JA3s fingerprints |
| **URLhaus** | A resource for sharing malware distribution sites |
| **ThreatFox** | A resource for sharing indicators of compromise (IOCs) |

**Questions:**

**Question 1:** The IOC `212.192.246.30:5555` is identified under which malware alias name on ThreatFox?
**Answer:** `Katana`

**Question 2:** Which malware is associated with the JA3 Fingerprint `51c64c77e60f3980eea90869b68c58a8` on SSL Blacklist?
**Answer:** `Dridex`

**Question 3:** From the statistics page on URLHaus, what malware-hosting network has the ASN number AS14061?
**Answer:** `DIGITALOCEAN-ASN`

**Question 4:** Which country is the botnet IP address `178.134.47.166` associated with according to FeodoTracker?
**Answer:** `Georgia`

---

## Task 5: PhishTool

**Notes:**

- Email phishing is one of the main precursors of any cyber attack.
- PhishTool seeks to elevate the perception of phishing as a severe form of attack and provide a responsive means of email security. Through email analysis, security analysts can uncover email IOCs, prevent breaches, and provide forensic reports.
- There are two accessible versions: **Community** and **Enterprise**.
- **Features include:** Email header analysis, return path, originating IP, and displaying the email body in rendered HTML, HTML source, or plain text format.

**Scenario Questions (based on analysing `Email1.eml`):**

**Question 1:** What social media platform is the attacker trying to pose as in the email?
**Answer:** `LinkedIn`

**Question 2:** What is the sender's email address?
**Answer:** `darkabutla@sc500.whpservers.com`

**Question 3:** What is the recipient's email address?
**Answer:** `cabbagecare@hotsmail.com`

**Question 4:** What is the Originating IP address? Defang the IP address.
**Answer:** `204[.]193[.]183[.]11`

**Question 5:** How many hops did the email go through to get to the recipient?
**Answer:** `4`

---

## Task 6: Cisco Talos Intelligence

**Notes:**

- Cisco Talos Intelligence provides threat intelligence on IPs, domains, and files.
- It includes a **Reputation Center** for lookups and **Email & Spam Data** to track top senders and spam networks.

**Scenario Questions (using `Email1.eml` data on Talos):**

**Question 1:** What is the listed network owner of the IP address from the previous task?
**Answer:** `DEFT.COM`

**Question 2:** What is the customer name of the IP address?
**Answer:** `Complete Web Reviews`

---

## Task 7: Scenario 1

**Notes:**

Analyzed `Email2.eml` found on the VM.

**Question 1:** According to `Email2.eml`, what is the recipient's email address?
**Answer:** `chris.lyons@supercarcenterdetroit.com`

**Question 2:** On VirusTotal, which year recorded the first submission details of the mentioned file?
**Answer:** `2017`

---

## Task 8: Scenario 2

**Notes:**

Analyzed `Email3.eml` found on the VM.

**Question 1:** What is the name of the attachment on `Email3.eml`?
**Answer:** `Sales_Receipt 5606.xls`

**Question 2:** What malware family is associated with the attachment on `Email3.eml`?
**Answer:** `Dridex`

---

## Task 9: Conclusion

**Notes:**

Reached the end of the room. The room recommends further learning with other TryHackMe rooms: **Yara**, **MISP**, and **Red Team Threat Intel**.

**Question 1:** Read the above and completed the room
**Answer:** No answer needed
