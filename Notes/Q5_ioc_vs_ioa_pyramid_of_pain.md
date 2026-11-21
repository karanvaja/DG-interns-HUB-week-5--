## Q5: IOC vs IOA and the Pyramid of Pain

### This document explains the difference between Indicators of Compromise (IOCs) and Indicators of Attack (IOAs), and breaks down David Bianco's Pyramid of Pain — a model showing how much "pain" (cost/effort) it causes an attacker when a defender detects and blocks each indicator type.

## 1. IOC vs IOA

| **Aspect** | **IOC (Indicator of Compromise)** | **IOA (Indicator of Attack)** |
|---|---|---|
| **Definition** | **Artifacts** left behind **after** a compromise has occurred — evidence that something bad already happened | **Behaviors and actions** an attacker performs **during** an attack — evidence of intent and method in progress |
| **Nature** | **Static / reactive** — forensic leftovers | **Dynamic / proactive** — behavioral patterns |
| **Examples** | File hashes (MD5/SHA256), malicious IPs/domains, URLs, registry keys, file paths, email addresses | Process injection, credential dumping (LSASS access), suspicious PowerShell, lateral movement via SMB, persistence via scheduled tasks, unusual parent-child process relationships |
| **When detected** | **Post-compromise** (after the fact) | **During the attack** (can enable early blocking) |
| **Lifespan** | **Short** — attacker can change hashes/IPs easily | **Longer** — behaviors are tied to how the attacker must operate |
| **Ease for attacker to evade** | **Easy** — recompile, re-host, change domain | **Hard** — changing core TTPs requires retooling and retraining |
| **Detection value** | High volume, low durability | Lower volume, high durability |
| **Typical sources** | Threat intel feeds, sandbox reports, AV, forensic analysis | EDR, SIEM behavior rules, MITRE ATT&CK mapping, UEBA |
| **Best use** | **Blocking** known-bad (firewall, DNS sinkhole, AV signatures) | **Hunting** and **detection engineering** (behavioral rules) |


* Simple analogy: An IOC is the fingerprint left at a crime scene (found after the fact). An IOA is the modus operandi — the way the criminal operates (noticed during the act).

* Key point: IOCs are easy to collect but easy for attackers to change. IOAs are harder to detect but far more resilient — this is exactly what the Pyramid of Pain formalizes.

## 2. The Pyramid of Pain

* The Pyramid of Pain (David J. Bianco, 2013) ranks indicator types by how much pain it causes an attacker when a defender blocks/detects them. Bottom = easy for attacker to change (low pain). Top = very hard (high pain).

| **Level** | **Indicator Type** | **What It Is** | **Example** | **Attacker's Cost to Change** | **Pain to Attacker** |
|---|---|---|---|---|---|
| **6 (Top)** | **TTPs** (Tactics, Techniques, Procedures) | The attacker's **methodology** and behavior | Credential dumping via LSASS; Pass-the-Hash; spear-phishing with macro → Cobalt Strike | **Very High** — must redesign tooling, retrain, re-plan | 🔴 **Tough!** |
| **5** | **Tools** | The **software/utilities** the attacker uses | Mimikatz, Cobalt Strike, PsExec, Rubeus | **High** — must switch to a new tool, learn it, possibly rebuild infrastructure | 🟠 **Challenging** |
| **4** | **Network/Host Artifacts** | Distinctive **traces** left by tools on the network or host | Named pipes (`\\.\pipe\msagent_12`), registry keys, user-agent strings, mutexes | **Moderate–High** — requires modifying tool config or source | 🟡 **Annoying** |
| **3** | **Domain Names** | Malicious **domains** used for C2, phishing, or payload hosting | `evil-c2[.]com`, lookalike `paypa1[.]com` | **Moderate** — register a new domain (cheap, but requires re-setup + rep for new domain) | 🟡 **Simple** |
| **2** | **IP Addresses** | **IPs** of C2 servers, payload hosts, or phishing infrastructure | `198.51.100.77`, `203.0.113.5` | **Low–Moderate** — spin up a new VPS/cloud instance quickly | 🟢 **Easy** |
| **1** | **Hash Values** | **MD5/SHA1/SHA256** of malicious files | `d41d8cd98f00b204e9800998ecf8427e` | **Trivial** — recompile/repack, change one byte, hash changes completely | 🟢 **Trivial** |


## Visual (bottom = low pain, top = high pain)

                  ▲
                 / \
                /   \        TTPs            ← Tough! (hardest to change)
               /-----\
              /       \      Tools           ← Challenging
             /---------\
            /           \    Network/Host Artifacts ← Annoying
           /-------------\
          /               \  Domain Names    ← Simple
         /-----------------\
        /                   \ IP Addresses   ← Easy
       /---------------------\
      /                       \ Hash Values  ← Trivial
     /-------------------------\
    ▼ (easiest to change, lowest pain)


## 3. How Hard Is Each Level for the Attacker to Change?

| **Pyramid Level** | **Difficulty to Change** | **Why** | **Detection Durability** |
|---|---|---|---|
| **Hash Values** | **Trivial** | Change one byte → new hash; recompile malware | Very low — blocklists go stale fast |
| **IP Addresses** | **Easy** | Buy new VPS/proxy; rotate C2 | Low — IPs change frequently |
| **Domain Names** | **Moderate** | Must register, configure DNS, build reputation; some cost/time | Medium — domain blocklists last longer |
| **Network/Host Artifacts** | **Moderate–High** | Must modify tool code/config (pipes, mutexes, user-agents) | Medium–High — requires attacker effort |
| **Tools** | **High** | Must abandon familiar tool, learn new one, possibly rebuild | High — forces retooling |
| **TTPs** | **Very High** | Must change **how they operate** — retrain, redesign playbooks, re-plan | **Highest** — behavioral detection is hardest to evade |


* Rule of thumb: The higher up the pyramid you detect, the more long-term value your detection has — but the harder it is to build the detection in the first place.



## 4. Practical Implications for Analysts
* Don't stop at hashes and IPs. They are the easiest to collect but also the easiest for attackers to evade. Use them for quick blocking, but don't rely on them as your only detection.

* Pivot upward. When you get a hash, also extract:

* the domain/IP it connected to,

* the artifacts it created (pipes, registry keys),

* the tool family,

* the TTP (map to MITRE ATT&CK).

* Map detections to MITRE ATT&CK — that's how you operationalize TTP-level detection (e.g., T1003 OS Credential Dumping, T1059 Command and Scripting Interpreter, T1021 Remote Services).

* Combine IOC + IOA detection. IOC blocklists catch known-bad fast; IOA behavioral rules catch novel/evasive variants.

* Feed threat intel both ways. Consume IOCs from feeds (fast blocking) and use TTP intel to build hunts (durable detection).

## 5. Key Takeaways
* IOC = static evidence after compromise; IOA = behavioral evidence during attack.

* IOCs are cheap to collect, cheap for the attacker to change; IOAs are harder to build but much more durable.

* The Pyramid of Pain ranks indicators by attacker cost to change: Hashes (trivial) → IPs (easy) → Domains (moderate) → Host/Network Artifacts (high) → Tools (high) → TTPs (very high).

* Detect as high on the pyramid as you can — TTP-level detection forces the attacker to change their entire approach.

* Best practice: block at the bottom (hashes/IPs) for speed, hunt at the top (TTPs/ATT&CK) for durability.


