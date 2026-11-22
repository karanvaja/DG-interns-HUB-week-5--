# IOC Cheat Sheet: IOC Type - Where to Find It - Tool to Check It

This table provides a quick reference for Tier 1/Tier 2 analysts to locate and verify common Indicators of Compromise (IOCs) during an investigation.

| # | IOC Type | Where to Find It | Tool to Check It |
|---|----------|------------------|------------------|
| 1 | **IP Address** | Firewall logs, Proxy logs, PCAP files | VirusTotal, AbuseIPDB, AlienVault OTX |
| 2 | **Domain Name** | DNS logs, Email headers, Proxy logs | URLScan.io, VirusTotal, DomainTools |
| 3 | **URL** | Email body, Web proxy logs, Browser history | URLScan.io, Any.run, VirusTotal |
| 4 | **File Hash (MD5/SHA256)** | EDR logs, Antivirus alerts, Sandbox reports | VirusTotal, Hybrid Analysis, MalwareBazaar |
| 5 | **Email Address** | Email headers (`From`, `Reply-To`, `Return-Path`) | Have I Been Pwned, MXToolbox, Hunter.io |
| 6 | **User-Agent String** | Web server logs, Proxy logs, PCAP files | Wireshark (filter by http.user_agent) |
| 7 | **Registry Key** | Sysmon (Event ID 12/13/14), EDR logs | Regedit (on VM), Autoruns |
| 8 | **Scheduled Task** | Sysmon (Event ID 1), Windows Event ID 4698 | Task Scheduler, Autoruns |
| 9 | **Named Pipe** | Sysmon (Event ID 17/18), EDR | Process Explorer, Pipelist |
| 10 | **File Path** | Sysmon (Event ID 11), EDR logs, AV logs | Event Viewer, File Explorer |
| 11 | **Mutex** | Sandbox reports (Any.run, Hybrid Analysis) | Process Explorer (Find Handle) |
| 12 | **SSL/TLS Certificate** | PCAP files, Proxy logs | Censys, Shodan, SSL Blacklist (Abuse.ch) |