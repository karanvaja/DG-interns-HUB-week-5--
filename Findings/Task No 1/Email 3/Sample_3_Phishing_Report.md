# Phishing Analysis Report - Sample 3

**1. Basic Information**
*   **Sender (From):** `nao-responder-Visa701035750@promocoes701035750` (Display Name: Visa)
*   **Recipient (To):** `phishing@pot`
*   **Subject:** Copa 2026: Oportunidade de prêmio no valor de R$ 100.000,00 — ID: 152092200
*   **Date:** Mon, 6 Jul 2026 07:27:17 +0000

**2. Authentication Results**
*   **SPF:** None (Sender IP 95.179.194.86 is not authorized)
*   **DKIM:** None (Message is not signed)
*   **DMARC:** None (Action=none)
*   **Note:** The email failed all basic authentication checks. It is completely spoofed and was sent from an unauthorized server.

**3. Indicators of Compromise (IOCs)**
*   **Malicious URL:** `hxxps://cop4asojateosom0-1094100152898.us-central1.run.app/?cid=phishing@pot@hotmail.com` 
*   **Sender IP:** `95.179.194.86` (Vultr Hosting, often used for spam)
*   **Reply-To:** `suporte@notificacoes` (Incomplete and fake email address)
*   **Attachment Hash:** N/A

**4. Reputation Checks (Evidence)**
*   *(તમારે આ લિંકને urlscan.io અને VirusTotal પર સ્કેન કરીને તેનું રિઝલ્ટ અહીં લખવાનું છે)*
*   **URL Scan (urlscan.io):** [તમારું રિઝલ્ટ અહીં લખો] - *(See `Findings/Sample3_URLScan.png`)*
*   **URL Scan (VirusTotal):** [તમારું રિઝલ્ટ અહીં લખો] - *(See `Findings/Sample3_VirusTotal.png`)*

**5. Red Flags Identified**
*   **Fake Sender Address:** The domain `promocoes701035750` is not a real domain (no `.com` or `.com.br`), and it is clearly trying to spoof Visa.
*   **Urgency and Greed:** The email promises massive prizes (R$ 100,000, free trips, Outback dinners) just for spending R$ 10.00. This is a classic "too good to be true" scam.
*   **Suspicious Infrastructure:** The link redirects to `us-central1.run.app`, which is a Google Cloud Run server. While Google is a legitimate service, attackers frequently abuse it to host temporary, free phishing sites that bypass domain blocklists.
*   **Incomplete Reply-To:** The `Reply-To` address is `suporte@notificacoes`, which is missing a valid domain name (TLD).
*   **Data Harvesting Link:** The link explicitly contains the victim's email address as a parameter (`?cid=phishing@pot@hotmail.com`), which is a common tactic to track who clicked the link.

**6. Verdict**
*   **Verdict:** **Malicious (Scam/Phishing)**
*   **Justification:** This is a fraudulent sweepstakes email. The attacker is impersonating Visa to lure victims into clicking the link, which likely leads to a credential harvesting page, a fake survey designed to steal personal data, or a malware download. The use of a cloud-hosted domain (`run.app`) and a completely unauthenticated email proves it is malicious.