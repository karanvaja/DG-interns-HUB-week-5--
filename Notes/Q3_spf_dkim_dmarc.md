## Q3: SPF, DKIM, and DMARC — What Each Checks (With Pass/Fail Examples)

### SPF, DKIM, and DMARC are three email authentication mechanisms that work together to verify that an email is legitimate and to tell receiving servers what to do when authentication fails.

### Overview Table

| **Mechanism** | **What It Checks** | **Where It Lives** | **Result Values** |
|---|---|---|---|
| **SPF** (Sender Policy Framework) | Whether the **sending IP** is authorized to send mail for the envelope domain (`MAIL FROM` / `HELO`) | DNS TXT record on the domain (`v=spf1 ...`) | `pass`, `fail`, `softfail`, `neutral`, `none`, `permerror`, `temperror` |
| **DKIM** (DomainKeys Identified Mail) | Whether the **message was signed** by the domain and **not modified in transit** (cryptographic signature over headers + body) | DNS TXT record at `selector._domainkey.domain` (public key) | `pass`, `fail`, `none`, `neutral`, `policy`, `permerror`, `temperror` |
| **DMARC** (Domain-based Message Authentication, Reporting & Conformance) | Whether the **From header domain aligns** with an SPF or DKIM pass, and **what to do on failure** (none / quarantine / reject); also enables reporting | DNS TXT record at `_dmarc.domain` (`v=DMARC1; p=...`) | Policy: `none`, `quarantine`, `reject` |

### 1. SPF — Sender Policy Framework

### What it checks: The receiving server looks at the IP address that connected to deliver the message and checks whether that IP is listed in the domain's SPF record (v=spf1 TXT record). SPF authenticates the envelope sender (MAIL FROM), not the visible From: header.

### SPF Pass Example (Authentication-Results header)

Authentication-Results: mx.google.com;
       spf=pass (google.com: domain of sender@example.com designates 203.0.113.25 as permitted sender) smtp.mailfrom=sender@example.com;
       dkim=pass header.i=@example.com header.s=selector1;
       dmarc=pass (p=REJECT sp=REJECT dis=NONE) header.from=example.com


*  Why it passes: 203.0.113.25 is listed in example.com's SPF record as an authorized sender.

### SPF Fail Example

Authentication-Results: mx.google.com;
       spf=fail (google.com: domain of sender@example.com does not designate 198.51.100.77 as permitted sender) smtp.mailfrom=sender@example.com;
       dkim=none;
       dmarc=fail (p=REJECT sp=REJECT dis=NONE) header.from=example.com


* Why it fails: 198.51.100.77 is not in the SPF record — someone is sending as example.com from an unauthorized IP.

* Note: SPF has a 10-DNS-lookup limit and breaks on forwarding (the forwarder's IP is not in the original domain's SPF).

### 2. DKIM — DomainKeys Identified Mail

* What it checks: The sending domain cryptographically signs selected headers and the body using a private key. The receiver fetches the public key from DNS at selector._domainkey.domain and verifies the signature. DKIM proves the message came from the domain that signed it and was not altered in transit.

### DKIM Pass Example

Authentication-Results: mx.google.com;
       spf=pass smtp.mailfrom=sender@example.com;
       dkim=pass header.i=@example.com header.s=selector1 header.b="AbCdEf12";
       dmarc=pass (p=REJECT sp=REJECT dis=NONE) header.from=example.com

* Why it passes: The signature in DKIM-Signature: validates against the public key published at selector1._domainkey.example.com, and the body hash matches — nothing was modified.

### DKIM Fail Example

Authentication-Results: mx.google.com;
       spf=pass smtp.mailfrom=sender@example.com;
       dkim=fail (body hash did not verify) header.i=@example.com header.s=selector1;
       dmarc=fail (p=REJECT sp=REJECT dis=NONE) header.from=example.com

* Why it fails: The body hash did not verify — the message body was modified after signing (or the signature is invalid), so DKIM cannot vouch for integrity.

* Note: DKIM survives forwarding better than SPF (as long as the body isn't modified), and it authenticates the domain, not the IP.

### 3. DMARC — Domain-based Message Authentication, Reporting & Conformance

* What it checks: DMARC ties SPF and DKIM together and adds alignment and policy:

* Alignment: The domain in the visible From: header must match the domain that passed SPF (MAIL FROM) or DKIM (d=). This closes the gap where SPF/DKIM pass for a different domain than the one the user sees.

* Policy: The domain owner publishes p=none | quarantine | reject to tell receivers what to do on failure.

* Reporting: rua/ruf addresses receive aggregate/forensic reports.

### DMARC Pass Example

Authentication-Results: mx.google.com;
       spf=pass smtp.mailfrom=example.com;
       dkim=pass header.i=@example.com header.s=selector1;
       dmarc=pass (p=REJECT sp=REJECT dis=NONE) header.from=example.com

* Why it passes: SPF passed for example.com and the From: domain is example.com → aligned. (DKIM also passed and aligned, which is the strongest case.)

### DMARC Fail Example
Authentication-Results: mx.google.com;
       spf=pass smtp.mailfrom=bounces.attacker.net;
       dkim=pass header.i=@attacker.net header.s=sel1;
       dmarc=fail (p=REJECT sp=REJECT dis=NONE) header.from=example.com

* Why it fails: SPF and DKIM both passed — but for attacker.net, not example.com. The visible From: is example.com, so there is no alignment. DMARC fails even though SPF and DKIM "passed" — this is the classic lookalike/spoofing scenario DMARC is designed to catch.

### How They Work Together

| **Layer** | **Protects Against** | **Authenticates** |
|---|---|---|
| SPF | Unauthorized sending IPs | Envelope domain (`MAIL FROM`) |
| DKIM | Message tampering; proves signing domain | Header `d=` domain |
| DMARC | Visible `From:` spoofing; enforces policy + reporting | Alignment of SPF/DKIM with `From:` |

## Rule of thumb:

* SPF alone → weak (forwarding breaks it, doesn't check From:).

* DKIM alone → good integrity, but attacker can sign with their own domain.

* DMARC = SPF + DKIM + alignment + policy → the only one that protects the domain users actually see.

### Reading an Authentication-Results Header — Quick Guide

| **Field** | **Meaning** |
|---|---|
| `spf=pass/fail (...) smtp.mailfrom=` | SPF result for the envelope sender |
| `dkim=pass/fail header.i=@ header.s=` | DKIM result; `i=` is the signing domain (must align with `From:`), `s=` is the selector |
| `dmarc=pass/fail (p=... sp=... dis=...) header.from=` | DMARC result; `p=` is the published policy, `header.from=` is the visible From domain |

* Triage tip: A message with spf=pass dkim=pass but dmarc=fail is still spoofed — the passes belong to a different domain than the visible From:



