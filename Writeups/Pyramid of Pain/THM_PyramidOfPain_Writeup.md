TryHackMe: Pyramid Of Pain — Writeup
Room Link: https://tryhackme.com/room/pyramidofpain
Difficulty: Easy
Estimated Time: 30 mins
Tags: Cyber Defence Frameworks, Threat Intelligence, MITRE ATT&CK

Overview
The Pyramid of Pain, created by David J. Bianco, is a concept that illustrates the relationship between the types of indicators of compromise (IOCs) and the amount of "pain" or difficulty it causes an adversary when a defender blocks or detects those indicators. The higher you go up the pyramid, the harder it is for the attacker to change their behavior, making detection much more valuable.

Task 1: Introduction
Notes:

Understanding the Pyramid of Pain concept is crucial for Threat Hunters, Incident Responders, and SOC Analysts.

It is used to improve the effectiveness of CTI (Cyber Threat Intelligence) and threat hunting.

Question 1: Read the above.
Answer: No answer needed

Task 2: Hash Values (Trivial)
Notes:

Hash values (MD5, SHA-1, SHA-256) uniquely identify data.

Trivial: An attacker can easily change a file's hash by modifying even a single bit (e.g., appending a string), rendering hash-based blocklists useless for new variants.

Fuzzy Hashing (like SSDEEP) helps detect similar files even if the hash changes.

Question 1: Analyse the report associated with the hash "b8ef959a9176aef07fdca8705254a163b50b49a17217a4ff0107487f59d4a35d" here. What is the filename of the sample?
Answer: Sales_Receipt 5606.xls

Task 3: IP Address (Easy)
Notes:

Blocking IP addresses at the firewall is a common defense.

Easy: Attackers can easily change IPs using proxies, VPNs, or by renting new cloud instances. They also use Fast Flux (constantly changing the IPs associated with a domain name) to evade IP blocking.

Question 1: Read the following report to answer this question. What is the first IP address the malicious process (PID 1632) attempts to communicate with?
Answer: 50.87.136.52

Question 2: Read the following report to answer this question. What is the first domain name the malicious process ((PID 1632) attempts to communicate with?
Answer: craftingalegacy.com

Task 4: Domain Names (Simple)
Notes:

Domains are harder to change than IPs; attackers must purchase them, register them, and set up DNS. However, it's still relatively Simple for them.

Punycode Attack: Uses Unicode characters that look like legitimate letters (e.g., adidas.de vs adidạs.de) to trick users (Homograph attack).

URL Shorteners: Attackers use services like bit.ly, tinyurl, etc., to hide malicious domains. Appending a + to the shortened URL reveals the destination.

Question 1: Go to this report on app.any.run and provide the first suspicious domain request you are seeing, you will be using this report to answer the remaining questions of this task.
Answer: craftingalegacy.com

Question 2: What term refers to an address used to access websites?
Answer: Domain Name

Question 3: What type of attack uses Unicode characters in the domain name to imitate a known domain?
Answer: Punycode attack

Question 4: Provide the redirected website for the shortened URL using a preview: https://tinyurl.com/bw7t8p4u
Answer: https://tryhackme.com/

Task 5: Host Artifacts (Annoying)
Notes:

Host artifacts are traces left on the system (registry keys, suspicious processes, files dropped).

Annoying: Detecting at this level forces the attacker to go back and change their tools or methodologies, which is time-consuming.

Question 1: A security vendor has analysed the malicious sample for us. Review the report here to answer the following questions.
Answer: No answer needed

Question 2: A process named regidle.exe makes a POST request to an IP address based in the United States (US) on port 8080. What is the IP address?
Answer: 96.126.101.6

Question 3: The actor drops a malicious executable (EXE). What is the name of this executable?
Answer: G_jugk.exe

Question 4: Look at this report by VirusTotal. How many vendors determine this host to be malicious?
Answer: 9

Task 6: Network Artifacts (Annoying)
Notes:

Network artifacts include User-Agent strings, C2 information, or URI patterns.

Detecting these requires analyzing network traffic (PCAPs) using tools like Wireshark or TShark.

Example: A malware using a specific User-Agent string can be blocked easily.

Question 1: Which network indicator helped us identify the malware type (Emotet)?
Answer: User-Agent

Question 2: How many POST requests are in the screenshot from the PCAP file?
Answer: 6

Task 7: Tools (Challenging)
Notes:

Challenging: Detecting the specific tools an attacker uses (e.g., Mimikatz, Cobalt Strike) forces them to build or buy new tools, which takes time and money.

Fuzzy Hashing (SSDeep): Helps perform similarity analysis to match files with minor differences.

YARA rules: Great for detecting specific tools based on their characteristics.

Question 1: Provide the method used to determine similarity between the files.
Answer: Fuzzy Hashing

Question 2: Provide the alternative name for fuzzy hashes without the abbreviation.
Answer: context triggered piecewise hashes

Task 8: TTPs (Tough)
Notes:

TTPs (Tactics, Techniques & Procedures) is the apex of the Pyramid.

Tough: Detecting behavior (e.g., Pass-the-Hash) forces the attacker to completely change their methodology, retrain, or give up. This maps directly to the MITRE ATT&CK Matrix.

Detecting TTPs gives defenders the ultimate advantage.

Question 1: Navigate to ATT&CK Matrix webpage. How many techniques fall under the Exfiltration category?
Answer: 9

Question 2: Chimera is a China-based hacking group that has been active since 2018. What is the name of the commercial, remote access tool they use for C2 beacons and data exfiltration?
Answer: Cobalt Strike

Task 9: Practical: The Pyramid of Pain
Notes:

Deploy the static site and place the prompts into the correct tiers of the pyramid.

Mapping Logic:

Hash Values: MD5, SHA-1, SHA-256

IP Address: 192.168.1.1

Domain Names: google.com

Host Artifacts: File paths, Registry keys

Network Artifacts: User-Agent strings, URI patterns

Tools: Mimikatz, Cobalt Strike

TTPs: Pass-the-Hash, Spearphishing

Question 1: Complete the static site. What is the flag?
Answer: THM{PYRAMIDS_COMPLETE}
