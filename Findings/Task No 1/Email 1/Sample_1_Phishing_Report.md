# Phishing Analysis Report - Sample 1

**1. Basic Information**
*   **Sender (From):** security@paypa1-security.com
*   **Recipient (To):** ozania@company.com
*   **Subject:** Urgent: Your PayPal Account Has Been Limited
*   **Date:** Tue, 30 May 2024 14:22:00 -0700

**2. Authentication Results**
*   **SPF:** Fail (IP 185.153.196.42 is not authorized to send for paypa1-security.com)
*   **DKIM:** None (Not present in the header)
*   **DMARC:** Fail (Policy p=REJECT)

**3. Indicators of Compromise (IOCs)**
*   **Defanged URL:** `hxxps://paypa1-verify-security[.]com/`
*   **Domain:** `paypa1-verify-security[.]com`
*   **Attachment Hash (SHA256):** N/A (No attachment found)

**4. Reputation Checks (Evidence)**
*   **URL Scan (urlscan.io):** Suspicious/Malicious - *Domain is never seen before (Newly registered) and is impersonating PayPal.* (See `Findings/Task No 1/Email 1/Sample1_URLScan.png`)
*   **URL Scan (VirusTotal):** Clean (0/93) - *Note: Although VT shows 0 detections, the domain is newly created and currently shows an Error (likely taken down or blocking sandboxes). The context of the email still makes it malicious.* (See `Findings/Task No 1/Email 1/Sample1_VirusTotal.png`)

**5. Red Flags Identified**
*   **Lookalike Domain (Typosquatting):** The sender uses `paypa1-security.com` (using the number '1' instead of the letter 'l').
*   **Mismatched Link:** The link in the HTML body goes to `paypa1-verify-security.com` which is not the official PayPal domain.
*   **Urgency/Threats:** The subject and body use threatening language ("Urgent", "avoid permanent limitation", "expire in 24 hours").
*   **Generic Greeting:** The email starts with "Dear Customer" instead of the recipient's name.
*   **Authentication Failures:** SPF and DMARC explicitly failed, proving the sender is spoofing the domain.

**6. Verdict**
*   **Verdict:** **Malicious**
*   **Justification:** This is a clear credential harvesting phishing attempt. The attacker is using a typosquatted domain to impersonate PayPal, attempting to create panic in the user. The SPF and DMARC checks failed, and the URL leads to a brand new, unverified site designed to steal login credentials.