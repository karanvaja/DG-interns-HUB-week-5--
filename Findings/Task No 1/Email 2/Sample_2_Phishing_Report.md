# Phishing Analysis Report - Sample 2

**1. Basic Information**
*   **Sender (From):** `hpayMonitorPlatform@handpay.com.cn` (Display Name: OKX Extension)
*   **Recipient (To):** `phishing@pot`
*   **Subject:** rodrigo-f-p ⭐ 4.7/5 Rating: OKX Web3 Extension on Chrome Web Store
*   **Date:** Wed, 08 Jul 2026 07:16:23 +0000

**2. Authentication Results**
*   **SPF:** None (Sender IP 180.168.61.82 is not authorized)
*   **DKIM:** Fail (Key not found in DNS for `dev.roombird.ru`)
*   **DMARC:** None (Action=none)
*   **Note:** Microsoft Exchange added `compauth=pass reason=105`, which is a composite check, but the standard SPF/DKIM failed. The DKIM signature explicitly claims the email came from `dev.roombird.ru`, which contradicts the actual sender address.

**3. Indicators of Compromise (IOCs)**
*   **IOC 1 (Suspicious Domain in Header):** `dev.roombird[.]ru` (Hosted on IP `5.188.28.177`)
*   **IOC 2 (Malicious URL / Punycode):** `hxxps://chromewebstore.google.com/detail/%D0%BE%D2%9B%D1%85-w%D0%B0ll%D0%B5t-dashboard/inophbikolocpigmkhllfkdkiccjpggh` *(Note: The URL contains URL-encoded Cyrillic characters for "okx" and "wallet", tricking the user into thinking it's an official link).*
*   **Attachment Hash:** N/A (No attachment)

**4. Reputation Checks (Evidence)**
*   **Domain (`dev.roombird.ru`) Scan (urlscan.io):** No classification (Shows 410 Gone, indicating the malicious content might have been taken down). IP located in Russia. - *(See `Findings/Sample2_urlscan_roombird.png`)*
*   **URL (Chrome Store) Scan (urlscan.io):** No classification (It redirects to `consent.google.com`). - *(See `Findings/Sample2_urlscan_chrome.png`)*
*   **URL (Chrome Store) Scan (VirusTotal):** 0/93 Vendors flagged it as malicious. (Clean reputation, but highly suspicious context). - *(See `Findings/Sample2_vt_chrome.png`)*

**5. Red Flags Identified**
*   **Homograph / Punycode Attack:** The URL uses Cyrillic characters (URL-encoded as `%D0%BE%D2%9B%D1%85`) to make the Chrome Web Store extension name look like "okx-wallet-dashboard". To a normal user, it looks like a legitimate OKX extension.
*   **Spoofed Sender / Display Name:** The display name claims to be "OKX Extension", but the email address is a compromised or spoofed `handpay.com.cn` server.
*   **DKIM Header Mismatch:** The email header shows the DKIM signature belongs to `dev.roombird.ru` (a Russian domain), which has no relation to OKX or handpay.com.cn.
*   **Hidden Tracking / Unsubscribe:** The `List-Unsubscribe` header contains the exact same suspicious URL-encoded link, forcing victims to click it if they try to unsubscribe.
*   **Hidden Chinese Text:** At the bottom of the raw email, there is a hidden confidentiality notice written in Chinese, which is a common tactic used by spam bots.

**6. Verdict**
*   **Verdict:** **Malicious**
*   **Justification:** Even though URL scanners show 0 detections, this is a highly sophisticated **Punycode Phishing Attack**. The attacker is using a Cyrillic lookalike domain within the official Chrome Web Store URL to trick users into downloading a fake crypto wallet extension that will likely drain their funds. The mismatch between the sender, the DKIM signature, and the URL characters confirms it is malicious.