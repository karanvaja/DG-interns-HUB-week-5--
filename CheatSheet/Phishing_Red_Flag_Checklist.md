# Phishing Red-Flag Checklist

Use this checklist during Tier 1 triage to quickly determine if an email is suspicious or malicious.

## 1. Sender & Header Red Flags
- [ ] The sender's display name does not match the actual email address.
- [ ] The domain is misspelled or a lookalike (e.g., `rnicrosoft.com`, `paypa1.com`).
- [ ] The `Reply-To` address is different from the `From` address.
- [ ] SPF, DKIM, or DMARC checks failed (check the `Authentication-Results` header).
- [ ] The email claims to be from an internal executive but originates from an external IP.

## 2. Content & Tone Red Flags
- [ ] The email creates a false sense of urgency (e.g., "Act Now!", "Account will be locked").
- [ ] It uses threatening language (e.g., "Legal action will be taken").
- [ ] The greeting is generic (e.g., "Dear Customer" instead of your name).
- [ ] There are obvious grammar, spelling, or formatting errors.
- [ ] It asks for sensitive information (passwords, OTPs, credit card numbers).
- [ ] It asks you to bypass normal procedures (e.g., "Keep this confidential").

## 3. Links & Attachments Red Flags
- [ ] Hovering over a link reveals a different destination URL.
- [ ] The URL uses a URL shortener (e.g., bit.ly, tinyurl) or a raw IP address.
- [ ] The link points to a free hosting site (e.g., `*.weebly.com`, `*.000webhostapp.com`).
- [ ] The attachment has a dangerous extension (e.g., `.exe`, `.scr`, `.js`, `.vbs`, `.iso`).
- [ ] The attachment is a password-protected ZIP file (often used to bypass AV).
- [ ] The attachment uses a double extension (e.g., `invoice.pdf.exe`).

## 3. Contextual Red Flags
- [ ] The email is completely unexpected and out of the blue.
- [ ] The timing is suspicious (e.g., sent at 3:00 AM on a Sunday).
- [ ] It is a reply to an old thread, but the topic has suddenly changed to a financial request (Thread Hijacking).
- [ ] The sender's tone or writing style is different from how they usually write.