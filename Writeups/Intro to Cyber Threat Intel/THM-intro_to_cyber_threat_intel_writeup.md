# TryHackMe: Intro to Cyber Threat Intel --- Writeup

**Room Link:** <https://tryhackme.com/room/introtocyberthreatintel>\
**Difficulty:** Easy\
**Estimated Time:** 45 mins\
**Tags:** Cyber Defence Frameworks, Threat Intelligence, SOC Level 1

------------------------------------------------------------------------

## Overview

This room introduces the fundamentals of Cyber Threat Intelligence (CTI)
and how it applies to daily SOC operations. It covers the difference
between data, information, and intelligence, the CTI lifecycle, sharing
standards, and practical application of threat intelligence to triage
alerts.

------------------------------------------------------------------------

## Task 1: Introduction

**Notes:**

-   This room translates abstract CTI into everyday tasks: enriching
    indicators, triaging alerts, and turning raw data into actionable
    stories.
-   Objective: Learn how to recognize *why* an IP address spells trouble
    and how to prove it.

**Question 1:** Ready to get started!\
**Answer:** `No answer needed`

------------------------------------------------------------------------

## Task 2: Cyber Threat Intelligence

**Notes:**

-   **Data, Information, Intelligence:**
    -   **Data:** Unprocessed observable (e.g., `45.155.205.3 :443`).
    -   **Information:** Data + factual annotation (e.g., IP registered
        to Hetzner, seen 2023-07-14).
    -   **Intelligence:** Analyzed information answering "so-what"
        (e.g., IP belongs to BumbleBee C2; block immediately).
-   **Indicator Types:**
    -   **IOC (Indicator of Compromise):** Evidence of a breach (e.g.,
        C2 address in logs).
    -   **IOA (Indicator of Attack):** Malicious action underway (e.g.,
        PowerShell launching an unknown service).
    -   **TTP (Tactics, Techniques, and Procedures):** Adversary's
        detailed methodologies (MITRE ATT&CK IDs).
-   **Intelligence Sources:** Internal telemetry, Commercial services,
    OSINT (Open-Source Intelligence), and Communities & ISACs.
-   **Threat Intelligence Classifications:**
    -   **Strategic Intel:** High-level (threat landscape, emerging
        trends, business decisions).
    -   **Tactical Intel:** Adversary TTPs (e.g., Advisory notes on
        T1059.005).
    -   **Operational Intel:** Campaign-specific details (motives,
        intent, critical assets).
    -   **Technical Intel:** Atomic indicators (IPs, hashes).

**Question 1:** What does CTI stand for?\
**Answer:** `Cyber Threat Intelligence`

**Question 2:** IP addresses, Hashes and other threat artefacts would be
found under which Threat Intelligence classification?\
**Answer:** `Technical Intel`

------------------------------------------------------------------------

## Task 3: CTI Lifecycle

**Notes:**

-   **6-Phase CTI Lifecycle:** Planning & Direction → Collection →
    Processing → Analysis → Dissemination → Feedback.
-   **TLP (Traffic Light Protocol):** Rules for sharing intelligence.
    -   **TLP:CLEAR:** No restriction.
    -   **TLP:GREEN:** Share with peer community but not publicly.
    -   **TLP:AMBER:** Organization-wide, external sharing only with
        need-to-know.
    -   **TLP:RED:** Named recipients only (do not post without
        clearance).
-   **STIX:** Structured Threat Information Expression (JSON schema for
    threat intel).

**Question 1:** At which phase of the CTI lifecycle is data converted
into usable formats through sorting, organising, correlation and
presentation?\
**Answer:** `Processing`

**Question 2:** During which phase do security analysts get the chance
to define the questions to investigate incidents?\
**Answer:** `Direction`

------------------------------------------------------------------------

## Task 4: CTI Standards & Frameworks

**Notes:**

-   **MITRE ATT&CK:** Knowledge base of adversary tactics and techniques
    (e.g., T1059.001 PowerShell).
-   **MITRE D3FEND:** Counterpart to ATT&CK, cataloging defensive
    techniques.
-   **Cyber Kill Chain:** 7 phases (Recon → Weaponization → Delivery →
    Exploitation → Installation → C2 → Actions on Objectives).
-   **CVE, CVSS, and NVD:**
    -   **CVE:** Common Vulnerabilities and Exposures (e.g.,
        CVE-2023-4863).
    -   **CVSS:** Common Vulnerability Scoring System (0-10 severity).
    -   **NVD:** National Vulnerability Database.
-   **TAXII:** Trusted Automated Exchange of Indicator Information (API
    for exchanging intel). Supports **Collection** and **Channel**
    models.

**Question 1:** What sharing models are supported by TAXII?\
**Answer:** `Collection and Channel`

**Question 2:** When an adversary has obtained access to a network and
is extracting data, what phase of the kill chain are they on?\
**Answer:** `Actions on Objectives`

------------------------------------------------------------------------

## Task 5: Practical Analysis

**Notes:**

-   Clicked "View Site" to open the static site lab.
-   Analyzed a simulated email threat report and filled in the details
    on the right panel.
-   Identified the source email address and the downloaded file.

**Question 1:** What was the source email address?\
**Answer:** `vipviliain@badbank.com`

**Question 2:** What was the name of the file downloaded?\
**Answer:** `flbpfuh.exe`

**Question 3:** After building the threat profile, what message do you
receive?\
**Answer:** `THM{NOW_I_CAN_CTI}`
