# LetsDefend-WebAttack-Lab-Detecting-RFI-LFI-Attacks

## How to Detect and prevent different types of Web Attacks: SQL Injection,  Cross Site Scripting,  Command Injection,  IDOR,  RFI & LFI and File Upload (Web Shell)

## Practice with SOC Alerts
---
### 🔗120 - SOC170 - Passwd Found in Requested URL - Possible LFI Attack
---

<img width="1919" height="596" alt="image" src="https://github.com/user-attachments/assets/175abe05-11e9-4586-981d-36a6f52dd687" />

Here is my Ticket located in the **Investigation Channel** waiting to be investigated

---

* Click **Details** to view more information of the Ticket
<img width="1912" height="852" alt="image" src="https://github.com/user-attachments/assets/16490ac2-b526-4074-808c-4912fbc38d8c" />

---

* Click >> Create Ticket to Create ticket for EventID: 120
<img width="1906" height="756" alt="image" src="https://github.com/user-attachments/assets/830ffe84-262a-4364-9a9c-01c62e94c90e" />

Click the blue Continue button to create a ticket

---

Click OK when the window pops up “Ticket Created” indicating my “The ticket has been created successfully.”
<img width="783" height="554" alt="image" src="https://github.com/user-attachments/assets/bf52e2e8-fedb-41df-8b60-48cd3cb325f3" />

---

### Play Book Opens

(Which is used to begin the guided incident response investigation for this specific - Passwd Found in Requested URL - Possible LFI Attack alert.)
<img width="1902" height="557" alt="image" src="https://github.com/user-attachments/assets/3cea9c61-3075-42c4-bb11-a876a448c22b" />

This screen highlights a critical security alert:

• Incident Name: SOC170 — Passwd Found in Requested URL - Possible LFI Attack

• Incident Type: Web Attack

• Created Date: 2026-10-10 14:29:11

The dashboard indicates that I am currently navigating within the Case Management section (highlighted on the left panel).

Click blue Start Playbook! button.

---

<img width="979" height="569" alt="image" src="https://github.com/user-attachments/assets/4d3b09f5-28c8-4982-b3ac-4cacee64d71c" />

This step outlines the fundamental methodology required before analyzing logs directly to determine if the alert is a false positive or a true positive:

• Examining the rule name: SOC170 — Passwd Found in Requested URL - Possible LFI Attack

• Detected traffic communication: The source 106.55.45.162 and destination devices 172.16.17.13 (Host Name: Webserver1006)

This helps map out the direction of the traffic, the communication flow, and the specific network protocols used.

---

* Click Log Management
* Click Basic
* Type in One of the IoC”s eg. Source IP Address: 106.55.45.162

<img width="1902" height="754" alt="image" src="https://github.com/user-attachments/assets/93714fdd-0990-4a4e-aaa3-f85233421750" />

Result: It displays only the traffic between the source 106.55.45.162 and destination devices 172.16.17.13 (Host Name: Webserver1006)

### Protocols

|  Source Port  |  Destination Port  |
|  :---  |  :---  |
|  Port: 49028  |  Port: 443  |
|   This strongly indicates it is functioning as an ephemeral (temporary) client port, which is typical and standard behavior for outbound network traffic.  |  This is a globally trusted reputation as the industry standard for HTTPS (Hypertext Transfer Protocol Secure).  |

---

<img width="981" height="661" alt="image" src="https://github.com/user-attachments/assets/0c017063-3f16-4b40-aa36-00ad1da07cfc" />

<img width="1919" height="830" alt="image" src="https://github.com/user-attachments/assets/1f451c37-0355-462a-bcdc-eaf54d955f51" />
• VirusTotal Reputation: 0 / 92 Malicious Flags (Completely clean according to security vendors, though it holds a community score of -7).

---

<img width="1890" height="808" alt="image" src="https://github.com/user-attachments/assets/3f666509-fcf3-4959-99a1-16c46653ea2f" />
<img width="1892" height="778" alt="image" src="https://github.com/user-attachments/assets/c63b3e5e-5ff4-4dd0-9cea-7e3036f2f176" />

AbuseIPDB Reputation: 0% Abuse Confidence Score (Low Risk). While it has been reported 3,435 times from 519 distinct sources. 106.55.45.162 was first reported on April 19th 2021, and the most recent report was 9 months ago., indicating its abusive activity has decayed or stopped recently.

### Summary Analysis:
While threat intelligence engines currently rate it as “clean” due to a lack of recent activity (9 months ago), its classification as a hosted data center IP makes it highly suspicious when initiating inbound web attacks, as threat actors frequently rent temporary cloud servers to launch automated exploit campaigns.


|  ISP  |  Tencent cloud computing (Beijing) Co., Ltd.  |
|  :---  |  :---  |
|  Usage Type  |  Data Center/Web Hosting/Transit  |
|  ASN  |  AS45090  |
|  Domain Name  |  tencentcloud.com  |
|  Country  |  🇨🇳 China  |
|  City|  Guangzhou, Guangdong  |

---

<img width="979" height="730" alt="image" src="https://github.com/user-attachments/assets/213cfffa-adee-46a4-b4e2-138f1f013876" />

<img width="1905" height="828" alt="image" src="https://github.com/user-attachments/assets/c01a3080-7dfc-4098-bdb1-392826b623d2" />

* Reveiwing the provided raw log details, the traffic is not successful.

The HTTP Response Status code is 500 (Internal Server Error) and the HTTP Response Size is 0 bytes. This indicates that while the malicious Request URL: ```https://172.16.17.13/?file=../../../../etc/passwd``` reached the web application, the server encountered an error processing it and did not leak or return any sensitive data payload back to the attacker.

### Key Analytical Findings

• Suspicious User-Agent: The request uses an ancient User-Agent string corresponding to Internet Explorer 6.0 on Windows XP. This is a massive red flag in a modern production environment, strongly suggesting an automated scanner, exploit tool, or manual script spoofing the browser identity.

• Failed Response: The HTTP Response Status is 500 (Internal Server Error), the HTTP Response Size is 0 bytes and the Device Action is Permitted. Although Request URL: ```https://172.16.17.13/?file=../../../../etc/passwd``` reached the web application, the server encountered an error processing it and did not leak or return any sensitive data payload back to the attacker.

Evidence of Passwd Found in Requested URL - Possible LFI Attack: The parameters ```https://172.16.17.13/?file=../../../../etc/passwd``` endpoint.

---

* Click **Malicious**
<img width="1000" height="495" alt="image" src="https://github.com/user-attachments/assets/7133c5e0-e468-4b34-a0f9-3a63b3f7ea72" />

The traffic contains a blatant directory traversal attempt (../../../../etc/passwd) seeking access to a sensitive Linux system file. Even though the server blocked it with an internal error code, the intent and request payload itself are strictly hostile and malicious.

---

* Click **LFI/RFI**
<img width="993" height="418" alt="image" src="https://github.com/user-attachments/assets/83d1d13d-8de9-465e-84b8-c5868903247f" />

The payload ?file=../../../../etc/passwd uses directory traversal characters (../) to include a local configuration file from the operating system, which is a classic Local File Inclusion (LFI) technique.

---

* Click **Not Planned**
<img width="989" height="596" alt="image" src="https://github.com/user-attachments/assets/2ec84bdb-fd86-45ad-9cc6-712c564e8d77" />

### Reasons
The source IP address (106.55.45.162) belongs to an external hosting infrastructure (Tencent Cloud) rather than an internal security scanner, authorized testing company, or integrated attack simulation vendor platform.

---

* Select Traffic: **Internet --> Company Network**
<img width="995" height="435" alt="image" src="https://github.com/user-attachments/assets/e2f3705e-c913-4edf-86c7-85a405ffea15" />

Because SOC170 is a web-based Passwd Found in Requested URL - Possible LFI Attack attack executing HTTP GET requests directly against a web server.

---

<img width="979" height="787" alt="image" src="https://github.com/user-attachments/assets/9af5cfd6-81dd-47af-9d8e-c7617411921c" />

<img width="1905" height="828" alt="image" src="https://github.com/user-attachments/assets/159b0b79-cf08-484f-86f4-b3b9e961bb8b" />
• The raw HTTP server log shows an HTTP Response Status of 500 and an HTTP Response Size of 0.

---

<img width="1910" height="651" alt="image" src="https://github.com/user-attachments/assets/c8ff7d97-ae20-492d-8520-6e5dbb940b8b" />
• The terminal history shows no anomalous, attacker-driven commands executed around the time of the event (only standard docker-compose deployment commands from days prior).

---

* Click **NO**
<img width="984" height="389" alt="image" src="https://github.com/user-attachments/assets/8f4bcfd7-c976-4843-bb91-61237371c539" />

---

### Artifact:
• Value: 106.55.45.162

• Comment: Malicious source IP conducting Local File Inclusion (LFI) attack / directory traversal attempts.

• Type: Select IP from the dropdown menu.

<img width="994" height="503" alt="image" src="https://github.com/user-attachments/assets/1ff4d6c1-d789-4f91-99fb-28d0ccf85655" />

* Click **Next**

---

* Select **No.**
The instructions clearly state that Tier 2 escalation is not required in cases where attacks from the internet do not succeed. Because the web server blocked the directory traversal request with an HTTP 500 error code and returned a 0-byte response payload, the attack was completely unsuccessful.

<img width="977" height="651" alt="image" src="https://github.com/user-attachments/assets/bfb440fb-f786-4be4-8df6-6dd854f5d860" />

---

<img width="976" height="564" alt="image" src="https://github.com/user-attachments/assets/86e25dc3-6674-456f-9382-7561d72814bf" />

### My Anaylst Note:

```
The alert triggered due to an inbound Local File Inclusion (LFI) and directory traversal attack attempt from an external IP address (106.55.45.162) targeting the internal web server (172.16.17.13). The attack payload specifically attempted to read the sensitive Linux configuration file '/etc/passwd' via a modified URL parameter ('?file=../../../../etc/passwd'). 

Log analysis shows that the attack was unsuccessful. The web server responded with an HTTP status code 500 (Internal Server Error) and returned a response payload size of 0 bytes, confirming no system data or sensitive files were leaked to the attacker. Furthermore, investigation into the endpoint's terminal history revealed no anomalous post-exploitation activity or malicious code execution. 

The threat intelligence reputation check reveals that the source IP address is hosted on a Tencent Cloud infrastructure and has a history of high abuse, scanning, and exploit attempts. Because this was an internet-facing exploit attempt that failed to execute or penetrate the web application, this alert is being classified as a True Positive (unsuccessful attack attempt). No Tier 2 escalation or immediate host isolation is required. The malicious source IP has been documented as an Indicator of Compromise (IoC).
```

---

### Click Confirm & Close
To officially submit and close out this case (Ticket)

<img width="997" height="469" alt="image" src="https://github.com/user-attachments/assets/f038ec2f-bc8c-4f01-b4fb-1b534f3a87fb" />

---

<img width="1901" height="823" alt="image" src="https://github.com/user-attachments/assets/50657e9a-21f0-4a7c-816c-4543552b9e62" />

---

### **Final Results**

<img width="1897" height="824" alt="image" src="https://github.com/user-attachments/assets/c06a3324-b0c2-4a27-8749-dd8a657eb77a" />

---
