## Q2: Phishing Types and Red-Flag Checklist

### Phishing is a social engineering attack where an attacker impersonates a trusted entity to trick a victim into revealing credentials, clicking malicious links, opening malicious attachments, or transferring funds. Below are the main phishing types and their characteristics, followed by a red-flag checklist.

### Table: Phishing Types

| **Type** | **Target** | **Characteristics** | **Example Red Flags** |
|---|---|---|---|
| **Phishing** | Mass audience (broad, untargeted) | - Bulk email sent to many recipients<br>- Impersonates well-known brands (banks, Microsoft, PayPal, Amazon)<br>- Generic greeting ("Dear Customer")<br>- Spoofed sender address and lookalike domains<br>- Malicious links or attachments<br>- Urgency to click or log in | - Generic salutation<br>- Sender domain misspelled (e.g., `micros0ft.com`)<br>- Hovering link shows different URL than displayed<br>- Urgent "verify your account" language<br>- Unexpected attachment (`.zip`, `.html`, `.iso`) |
| **Spear Phishing** | Specific individual or small group | - Highly personalized using OSINT (name, role, colleagues, projects)<br>- References real internal events or documents<br>- Sent from spoofed or compromised trusted contact<br>- Often preludes credential theft or malware delivery<br>- Low volume, high precision | - Email references your real project but sender is external<br>- Unusual request from a known contact (tone/format differs)<br>- Reply-to address differs from sender<br>- Link to a login page on a non-corporate domain<br>- Request to "review" a document requiring sign-in |
| **Whaling** | Senior executives (CEO, CFO, board) | - Targets high-value individuals with authority<br>- Often fake legal notices, subpoenas, or investor documents<br>- May impersonate regulators, law firms, or board members<br>- Used to steal sensitive data or authorize fraudulent payments | - Legal threat or time-sensitive executive matter<br>- Sender domain closely mimics law firm/regulator<br>- Request to open encrypted attachment with password in body<br>- Unusual out-of-band request from a board member |
| **Smishing** | Mobile phone users (SMS/text) | - Phishing via SMS or messaging apps (WhatsApp, iMessage)<br>- Shortened URLs (e.g., `bit.ly`, `tinyurl`)<br>- Fake delivery notices, bank alerts, toll violations<br>- Malicious app install links<br>- Often uses local area codes or spoofed shortcodes | - Text from unknown number with link<br>- "Package delivery failed — pay fee here"<br>- Shortened URL hiding destination<br>- Grammar errors and urgency<br>- Request to install an app or call a number |
| **Vishing** | Phone users (voice calls) | - Voice phishing via phone call or voicemail<br>- Caller ID spoofing (bank, IRS, IT helpdesk)<br>- IVR prompts asking for credentials or card numbers<br>- Pretext: account compromise, refund, tech support<br>- Increasingly uses AI voice cloning | - Caller demands immediate action or payment<br>- Asks for OTP, password, or card CVV over the phone<br>- Caller ID matches bank but number is unverifiable<br>- Pressure to stay on the line / not hang up<br>- Request to install remote-access software |
| **BEC (Business Email Compromise)** | Organizations (finance, HR, executives, vendors) | - Compromised or spoofed executive/vendor mailbox<br>- Requests wire transfers, gift cards, W-2 data, or invoice changes<br>- Uses thread hijacking (replying to real email chains)<br>- Often no links/malware — pure social engineering<br>- Relies on authority and urgency | - Sudden change in vendor bank details<br>- CEO requests urgent wire transfer via email only<br>- Reply-to differs from the executive's real address<br>- Unusual request to keep it confidential<br>- Email from executive's domain but slightly altered (e.g., `ceo@company-co.com`) |


### Red-Flag Checklist
* Use this checklist when triaging any suspicious email, SMS, or call.

### Sender & Header Red Flags
* Sender display name does not match the actual email address
* Domain is misspelled or a lookalike (e.g., paypa1.com, rnicrosoft.com)
* Reply-To address differs from the From address
* SPF, DKIM, or DMARC fail (check authentication results in headers)
* Received chain shows unexpected relays or suspicious originating IP
*  Email claims to be internal but originates from an external serve

### Content & Tone Red Flags

□ Urgency or threat ("act now", "account will be closed", "legal action")
□ Generic greeting when a personalized one is expected
□ Grammar, spelling, or formatting errors
□ Unexpected request for credentials, OTPs, or payment
□ Request to bypass normal process ("don't tell anyone", "keep confidential")
□ Mismatch between sender's role and the request (e.g., HR asking for wire transfer)

### Links & Attachments Red Flags

□ Hovering over a link reveals a different destination than displayed
□ Link uses a URL shortener or raw IP address
□ Link points to a free hosting domain (e.g., *.weebly.com, *.000webhostapp.com)
□ Attachment type is risky (.exe, .scr, .js, .vbs, .iso, .img, .html, password-protected .zip)
□ Macro-enabled Office documents (.docm, .xlsm)
□ Attachment name uses double extension (e.g., invoice.pdf.exe)

### Contextual Red Flags

□ Email is unexpected or out of the blue
□ Request falls outside normal business process
□ Sender's tone or writing style differs from usual
□ Thread hijacking: reply to a real thread but with new, unusual request
□ Timing is suspicious (late night, weekend, during known absence)
□ SMS from unknown number with a link
□ Phone caller asks for OTP, password, or remote access

### Quick Comparison: Which Type Is It?

| **If the attack...** | **Type** |
|---|---|
| Is mass, generic, brand-impersonating | Phishing |
| Is personalized to one person | Spear Phishing |
| Targets a C-level executive | Whaling |
| Arrives by SMS/text | Smishing |
| Arrives by phone call | Vishing |
| Impersonates an executive/vendor to move money or data | BEC |

### Key Takeaways

* Phishing is the entry vector; BEC is often the objective (fraud or data theft).

* Personalization increases success — spear phishing and whaling bypass generic filters.

* Smishing and vishing bypass email controls entirely — user awareness is the main defense.

* BEC often contains no link or malware — it relies purely on authority and urgency, so technical filters alone cannot stop it.

* Always verify out-of-band (call the person on a known number) before acting on financial or credential requests.

