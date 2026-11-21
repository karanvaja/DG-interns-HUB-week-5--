## Q8: Incident Report Contents, Severity Levels, and Escalation

### An incident report is the formal record of what happened, what was done, and what must change. It serves operations (recovery), management (risk/impact), and compliance (legal/regulatory). A good report is concise, evidence-based, and structured so that both technical and non-technical readers can act on it.

## 1. Incident Report Sections (Template)
* The following template combines statutory-required fields with NIST SP 800-61 best practices. Adjust to your organization's policy and regulatory obligations.

### Section A: General Information

| **Field**                | **Description**                                                                       | **Required** |
|---|---|---|
| **Incident ID**          | Unique identifier (e.g., `INC-2025-0042`)                                             | Yes          |
| **Incident Name/Title**  | Short descriptive title (e.g., "Spearphishing → Credential Compromise → BEC Attempt") | Yes          |
| **Report Type**          | Initial / Follow-up / Final                                                           | Yes          |
| **Classification**       | Restricted / Confidential / Internal                                                  | Yes          |
| **Date/Time Occurred**   | When the incident began (best estimate)                                               | Yes          |
| **Date/Time Discovered** | When it was first detected                                                            | Yes          |
| **Detected By**          | Tool, user, or analyst (SIEM alert, user report, third party)                         | Yes          |
| **Incident Category**    | Phishing, malware, unauthorized access, DoS, BEC, data breach, etc.                   | Yes          |
| **Severity**             | Critical / High / Medium / Low (see Section 4)                                        | Yes          |
| **Current Status**       | Open / Contained / Eradicated / Recovered / Closed                                    | Yes          |



### Section B: Executive Summary
* What happened (2–4 sentences, plain language).
* Business impact (systems, data, users affected).
* Current state (contained? recovered? ongoing?).
* Key decisions needed (if any).

### Section C: Timeline

| **Event**                           | **Date/Time (UTC)** | **Responsible Party** | **Evidence/Source**    |
|---|---|---|---|
| First malicious email received      | 2025-11-17 09:14    | Email gateway         | Mail logs              |
| User clicked link                   | 2025-11-17 09:22    | User `jdoe`           | Proxy logs             |
| Credential entered on phishing page | 2025-11-17 09:23    | User `jdoe`           | Proxy/TLS logs         |
| SIEM alert triggered                | 2025-11-17 09:31    | SIEM rule `PHISH-001` | SIEM                   |
| Analyst triaged and confirmed       | 2025-11-17 09:45    | Tier 1 analyst        | Ticket `INC-2025-0042` |
| Account disabled                    | 2025-11-17 09:52    | Identity team         | AD logs                |
| ...                                 | ...                 | ...                   | ...                    |


* Rule: Log every significant action with time (UTC), actor, and evidence source. This timeline becomes the authoritative record for lessons learned and legal review

### Section D: Indicators of Compromise (IOCs)

| **IOC Type**       | **Value**                               | **Context**                       | **Confidence** |
|---|---|---|---|
| Sender address     | `ceo@company-co[.]com`                  | Lookalike domain                  | High           |
| Phishing URL       | `hxxps://login-company[.]com/auth`      | Credential harvester              | High           |
| Source IP          | `198.51.100.77`                         | Sending IP (from Received header) | High           |
| File hash (SHA256) | `a1b2c3...`                             | Malicious attachment              | Medium         |
| User-Agent         | `Mozilla/5.0 (compatible; EvilBot/1.0)` | C2 beacon                         | Medium         |

* Note: Defang all indicators (hxxp, [.]) to prevent accidental clicks.

### Section E: Impact Assessment

| **Dimension**        | **Assessment**                               |
|---|---|
| **Confidentiality**  | Credentials exposed? Data accessed?          |
| **Integrity**        | Systems/files modified?                      |
| **Availability**     | Services disrupted? Downtime duration?       |
| **Users affected**   | Count and roles                              |
| **Systems affected** | Hostnames, IPs, applications                 |
| **Regulatory/legal** | Personal data breach? Notification required? |
| **Financial**        | Estimated cost (response, downtime, fines)   |


### Section F: Containment, Eradication, Recovery

| **Phase**       | **Actions Taken**                                                           | **Status**  |
|---|---|---|
| **Containment** | Account disabled, host isolated, domain blocked, password reset             | Complete    |
| **Eradication** | Malware removed, persistence deleted, vulnerability patched                 | Complete    |
| **Recovery**    | System restored from backup, user re-enabled with MFA, monitoring increased | In progress |

### Section G: Recommendations & Lessons Learned

* Root cause (how did it happen? e.g., lack of DMARC enforcement, user clicked link, MFA not enforced).
* What went well (detection speed, communication).
* What needs improvement (tooling gaps, process delays, training).
* Corrective actions with owner and due date.

| **Recommendation**                       | **Owner**          | **Due Date** | **Status** |
|---|---|---|---|
| Enforce DMARC `p=reject` on all domains  | Email team         | 2025-12-01   | Open       |
| Add phishing simulation for finance      | Security awareness | 2025-12-15   | Open       |
| Tune SIEM rule to reduce false positives | SOC                | 2025-11-30   | Open       |


## 2. Severity Levels

* Severity determines urgency, escalation path, and resource allocation. The table below uses a four-tier model consistent with common practice.



| **Severity** | **Definition**                                                                                                                              | **Examples**                                                                                         | **Response Target** |
|---|---|---|---|
| **Critical** | Incident affecting **critical systems or sensitive data** with potential to impact operations, revenue, customers, or result in data breach | Multi-system ransomware, unauthorized access to critical infrastructure, confirmed data exfiltration | **Immediate** — escalate to Incident Commander within **15–30 minutes** |
| **High**     | Incident affecting **non-critical systems** or with **significant impact** on operations, revenue, customers, or data                       | Malware on a single system, confirmed credential compromise, targeted phishing with successful click | **Urgent** — escalate to Tier 2/manager within **1 hour** |
| **Medium**   | Possible incident affecting non-critical systems; **limited impact** or contained                                                           | Phishing email reported but not clicked, suspicious login attempt blocked                            | **Standard** — triage within **4 hours** |
| **Low**      | Possible incident or **informational**; not time-sensitive                                                                                  | Blocked phishing attempts, policy violation without compromise, user investigation                   | **Routine** — handle within **24–48 hours** |

* Severity is dynamic: An incident may be reclassified as the investigation unfolds (e.g., a Medium phishing report becomes High when the user confirms clicking the link). The incident responder, not the reporter, has final authority on classification based on evidence.

## 3. Escalation

* Escalation is the structured process of raising an incident to the right people with the right authority when it exceeds the current handler's scope, severity, or time threshold.

### Escalation Triggers
* An incident should be escalated when any of the following occurs:

| **Trigger**                 | **Example**                                                      |
|---|---|
| **Severity threshold met**  | Incident classified as High or Critical                          |
| **Time threshold exceeded** | Incident open > 4 hours without containment                      |
| **Scope expansion**         | New hosts/users confirmed compromised; lateral movement detected |
| **Data exposure confirmed** | PII/PHI/financial data confirmed accessed or exfiltrated         |
| **Legal/regulatory clock**  | Breach notification timeline triggered (e.g., GDPR 72 hours)     |
| **System/business impact**  | Critical service down; executive or customer-facing impact       |
| **Handler requests help**   | Analyst identifies gap in tools, access, or authority            |

### Escalation Path (Example)

Tier 1 Analyst → Tier 2 Analyst → SOC Manager → IR Lead / Incident Commander → CISO → CEO/Legal/Comms

| **Level**              | **Who**                 | **When**                                                            |
|---|---|---|
| **Tier 1**             | SOC analyst             | Initial triage; handle Low/Medium per playbook                      |
| **Tier 2**             | Senior analyst          | Confirmed High; complex investigation                               |
| **SOC Manager**        | Operations lead         | Resource allocation; cross-team coordination                        |
| **Incident Commander** | Designated IR authority | Critical incidents; declares incident; owns response                |
| **CISO / Executive**   | C-level                 | Business impact; external communication; legal/regulatory decisions |
| **Legal / PR / HR**    | Support functions       | Data breach notification; reputational management; insider threat   |


* Key rule: Any responder can escalate — not just the incident lead. If the lead is stuck or unavailable, anyone who recognizes the trigger should escalate.

### Escalation Communication Rules
* Phone first for Critical/High — email is too slow for urgent incidents.
* Use out-of-band channels if primary comms may be compromised (e.g., Slack/Teams down → phone/SMS).
* Document every escalation: who, when, how, and acknowledgment received.
* Keep the status tracker updated so leadership has a single source of truth

## 4. Quick Reference: Report Quality Checklist

□ Incident ID and severity assigned
□ Timeline is complete with UTC timestamps and evidence sources
□ IOCs are defanged and confidence-rated
□ Impact covers CIA triad, users, systems, and regulatory exposure
□ Containment/eradication/recovery actions are documented with status
□ Recommendations have owners and due dates
□ Escalation log is included (who was notified, when, how)
□ Report is classified and stored per retention policy

## Key Takeaways

* An incident report must answer what, when, how, impact, actions, and prevention — structured so both SOC and leadership can act on it.

* Severity drives urgency: Critical = immediate escalation; High = urgent; Medium = standard; Low = routine.

* Escalation is triggered by severity, time, scope, data exposure, or legal clocks — and any responder can escalate.

* Documentation is evidence — timestamps, sources, and chain of custody matter for both operations and compliance.