# TryHackMe: Phishing Analysis Fundamentals — Writeup

- **Room Link:** https://tryhackme.com/room/phishingemails1tryoe
- **Difficulty:** Easy
- **Estimated Time:** 30 mins
- **Tags:** Phishing Analysis, SOC Level 1, Email Security

---

## Overview

This room introduces the core components of an email and how to analyze them for phishing indicators. It covers email structure, delivery protocols, header analysis, reading raw HTML source code, and identifying different types of phishing attacks.

---

## Task 1: Introduction

**Notes:**

- Spam and phishing are common social engineering threats. A single click can give attackers initial access.
- **Goal:** Inspect raw email files to identify true origin and intent.
- The lab uses a split-screen virtual machine with sample `.eml` files located in the `Email Samples` folder on the desktop.

**Question 1:** I am ready to learn about phishing analysis!
**Answer:** No answer needed

---

## Task 2: The Email Address

**Notes:**

An email address consists of two main parts separated by the `@` symbol:

- **Username:** Identifies the specific mailbox (e.g., `david`).
- **Domain Name:** Specifies the mail server responsible for receiving the message (e.g., `tryhackme.com`).

**Question 1:** Identify the domain used in the following email address: `hatsaleesang@tryhame.com`
**Answer:** `tryhame.com`

---

## Task 3: Email Delivery

**Notes:**

| Protocol | Purpose |
|----------|---------|
| **SMTP** (Simple Mail Transfer Protocol) | Sends emails from client to server, and server to server |
| **POP3** (Post Office Protocol) | Downloads emails to a single device (removes from server) |
| **IMAP** (Internet Message Access Protocol) | Syncs emails across multiple devices (remains on server) |

**Email Journey:** Sender Client (SMTP) → Sender Mail Server → DNS Query → Recipient Mail Server → Recipient Client (POP3/IMAP)

**Question 1:** Which protocol is responsible for sending an email from a client to a mail server?
**Answer:** `SMTP`

**Question 2:** Which service is used to look up the recipient domain's mail server?
**Answer:** `DNS`

**Question 3:** Bob wants to access his email from multiple devices, including his phone and laptop. Which protocol should he use?
**Answer:** `IMAP`

---

## Task 4: Email Headers

**Notes:**

- An email has two parts: **Header** (metadata) and **Body** (content).
- **Standard Headers:** From, To, Reply-To, Subject, Date.
- **Viewing Source:** In Thunderbird, use `Ctrl + U` or `View > Message Source` to see raw headers.
- **X-Originating-IP:** An optional header added by some email services that reveals the sender's actual IP address.

**Question 1:** What is the full subject line of `email11.eml`?
**Answer:** `Help protect your budget by protecting your home`

**Question 2:** View the message source of `email11.eml` using Thunderbird in your VM. What is the IP address listed as the X-Originating-IP?
**Answer:** `43.255.56.161`

---

## Task 5: Email Body

**Notes:**

- Emails can be **Plain Text** or **HTML Formatted**.
- Inspecting the raw HTML source reveals hyperlinks, images, and hidden content that might not be visible in the rendered view.
- **Attachments:** Often Base64 encoded in the raw source. Look for `Content-Type`, `Content-Disposition`, and `Content-Transfer-Encoding`.

**Question 1:** Open up the `email12.txt` file to view the source of an attachment. What is the Content-Type of the attachment?
**Answer:** `application/pdf`

**Question 2:** What is the name of the attachment from the previous question?
**Answer:** `zmgpalgh.pdf`

**Question 3:** Decode the base64 string using either a PDF converter or CyberChef. What is the hidden flag value?
**Answer:** `THM{BENIGN_PDF_ATTACHMENT}`

---

## Task 6: Types of Phishing

**Notes:**

- **Phishing:** Impersonating a trusted entity to steal info.
- **Spear Phishing:** Targeted at a specific individual.
- **Whaling:** Targets high-level executives (CEO, CFO).
- **Smishing:** Phishing via SMS.
- **Vishing:** Phishing via voice calls.
- **Defanging:** Replacing characters (like `http` → `hxxp` and `.` → `[.]`) to prevent accidental clicks during analysis.

**Question 1:** Which reputable organization is being spoofed in this phishing attempt? (Analyzing `email13.eml`)
**Answer:** `Home Depot`

**Question 2:** What is the sender's email address?
**Answer:** `support@teckbe.com`

**Question 3:** Inspect the email message source. What is the defanged X-Originating-IP?
**Answer:** `103[.]124[.]236[.]83`

**Question 4:** Continue analyzing the email message source. Which mail server generated the Authentication-Results header?
**Answer:** `atlas102.free.mail.gq1.yahoo.com`

---

## Task 7: Conclusion

**Notes:**

- Understanding email anatomy allows analysts to dissect suspicious emails confidently.
- **BEC (Business Email Compromise):** A specific type of attack where an adversary gains access to a legitimate email account to trick others into fraudulent actions.

**Question 1:** What attack, signified by the acronym BEC, uses a compromised email to trick employees into fraud?
**Answer:** `Business Email Compromise`
