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

<img width="1890" height="808" alt="image" src="https://github.com/user-attachments/assets/3f666509-fcf3-4959-99a1-16c46653ea2f" />
<img width="1892" height="778" alt="image" src="https://github.com/user-attachments/assets/c63b3e5e-5ff4-4dd0-9cea-7e3036f2f176" />

AbuseIPDB Reputation: 0% Abuse Confidence Score (Low Risk). While it has been reported 3,435 times from 519 distinct sources. 106.55.45.162 was first reported on April 19th 2021, and the most recent report was 9 months ago., indicating its abusive activity has decayed or stopped recently.

### Summary Analysis:
The IP belongs to a public cloud provider/VPS infrastructure (DigitalOcean). While threat intelligence engines currently rate it as “clean” due to a lack of recent activity (last 60 days), its classification as a hosted data center IP makes it highly suspicious when initiating inbound web attacks, as threat actors frequently rent temporary cloud servers to launch automated exploit campaigns.


|  ISP  |  Tencent cloud computing (Beijing) Co., Ltd.  |
|  :---  |  :---  |
|  Usage Type  |  Data Center/Web Hosting/Transit  |
|  ASN  |  AS45090  |
|  Domain Name  |  tencentcloud.com  |
|  Country  |  🇨🇳 China  |
|  City|  Guangzhou, Guangdong  |

