# 🏠 SOC Home Lab – Detection, Investigation & Incident Response

![Wazuh](https://img.shields.io/badge/Wazuh-005DAC?style=for-the-badge&logo=wazuh&logoColor=white)
![Splunk](https://img.shields.io/badge/Splunk-000000?style=for-the-badge&logo=splunk&logoColor=white)
![Sysmon](https://img.shields.io/badge/Sysmon-E65100?style=for-the-badge)
![Wireshark](https://img.shields.io/badge/Wireshark-1679A7?style=for-the-badge&logo=wireshark&logoColor=white)
![Kali Linux](https://img.shields.io/badge/Kali_Linux-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE_ATT%26CK-FF0000?style=for-the-badge)

A hands-on SOC home lab built across three virtual machines (Windows 10, Ubuntu, Kali Linux) to simulate real blue team workflows. Every project here involves actual attack simulation, live detection, and documented investigation the way a Tier 1 SOC analyst would approach it.

---

<img width="1671" height="2376" alt="Home-Lab-Structure" src="https://github.com/user-attachments/assets/80c96319-bf7a-4d15-8c63-2d11e3205f48" />

---

## 🖥️ Lab Environment

| Machine | Role |
|---|---|
| Windows 10 | Target endpoint, Sysmon + Wazuh agent, event log analysis |
| Ubuntu Server | Wazuh manager, log collection, SSH attack target |
| Kali Linux | Attacker machine, Hydra, Nmap, traffic generation |

All VMs run in an isolated NAT network on a single laptop using VirtualBox.

---

## 📂 Projects

---

### 🔴 Wazuh + VirusTotal Active Response Pipeline

Configured Wazuh to automatically detect and respond to malware using the VirusTotal API.

- Dropped a test malware file onto the Windows machine. Sysmon Event ID 11 caught the file creation, VirusTotal API scanned the hash and returned a positive verdict, and remove-threat.sh automatically deleted the file within 60 seconds
- Microsoft Edge was triggering T1105 false positive alerts. Wrote a custom suppression rule in local_rules.xml to eliminate the noise without reducing actual detection coverage
- Configured active response blocks so the pipeline triggers only on confirmed malicious verdicts, not on low-confidence scores
- 📌 MITRE: `T1105` Ingress Tool Transfer · `T1070.004` File Deletion · `T1565.001` Stored Data Manipulation

→ [View Lab](https://github.com/rohithbaggu56-dot/Wazuh-SIEM-SOC-Hands-On-Lab/blob/main/README.md)

---

### 🔴 SSH & RDP Brute Force Detection

Simulated brute force attacks from Kali Linux against Ubuntu and Windows targets and verified end-to-end detection and blocking.

- Ran Hydra from Kali against Ubuntu SSH. Wazuh triggered on repeated authentication failures and active response blocked the attacker IP automatically
- Ran Hydra against Windows RDP. Correlated Event IDs 4625 (failed logon) and 4740 (account lockout) in Wazuh to confirm the attack pattern
- Verified the blocked IP in Wazuh active response logs and confirmed no further connections were accepted from that source
- 📌 MITRE: `T1110` Brute Force · `T1110.001` Password Guessing · `T1078` Valid Accounts

→ [View Lab](https://github.com/rohithbaggu56-dot/Incident-Investigation-Report)

---

### 🔴 Sysmon Integration & False Positive Tuning

Deployed Sysmon on Windows 10 with a custom configuration and tuned detection rules to reduce noise while keeping real detections intact.

- Installed Sysmon with a custom XML config to capture process creation (Event ID 1), network connections (Event ID 3), and file drops (Event ID 11)
- Wazuh was generating false positive T1105 alerts from Microsoft Edge downloading filter list updates. Identified the pattern, wrote a local_rules.xml override to suppress it
- Validated the fix by confirming Edge no longer triggered alerts while a real file drop still fired correctly
- 📌 MITRE: `T1105` Ingress Tool Transfer · `T1036` Masquerading. 

→ [View Sysmon + Wazuh Lab](https://github.com/rohithbaggu56-dot/Wazuh-SIEM-SOC-Hands-On-Lab/blob/main/README.md) *(Sysmon is integrated within the Wazuh lab – detection rules and false positive tuning documented there)*

---

### 🔴 ModSecurity WAF + DVWA Web Attack Simulation

Set up ModSecurity WAF in front of DVWA and simulated web application attacks to verify WAF blocking behavior.

- Ran SQL injection and XSS payloads against DVWA. ModSecurity blocked each attack and logged the triggered rule ID, payload, and source IP
- Reviewed WAF logs to confirm which OWASP Core Rule Set rules fired for each attack type
- 📌 MITRE: `T1190` Exploit Public-Facing Application · `T1059` Command & Scripting Interpreter

*(ModSecurity WAF is part of the core SOC lab environment – findings documented in the SOC Home Lab repo)*

---

### 🔴 Phishing Analysis

Worked through phishing triage from alert intake to escalation decision using simulated email samples.

- Identified a spoofed sender domain by analyzing email headers. Reply-To and Return-Path did not match the claimed sender address
- Extracted the embedded URL, confirmed it redirected to a credential harvesting page via VirusTotal and urlscan.io
- Checked sender IP reputation on AbuseIPDB and confirmed it was flagged as a known malicious source
- Ran headers through MXToolbox and confirmed SPF and DKIM both failed, indicating a spoofed origin
- 📌 MITRE: `T1566.001` Spearphishing Attachment · `T1566.002` Spearphishing Link

→ [View Lab](https://github.com/rohithbaggu56-dot/Phishing-Analysis-SOC-Simulation-Lab)

---

### 🔴 Splunk Log Analysis & Detection

Ingested Wazuh alert logs into Splunk manually and wrote SPL queries to detect attack patterns across SSH, DNS, and HTTP log sources.

- Wrote SPL to detect SSH brute force: `index=main sourcetype=linux_secure "Failed password" | stats count by src_ip | where count > 10`
- Identified a source IP generating abnormally high DNS query volume and flagged it as a potential C2 beaconing pattern
- Built a dashboard tracking failed authentication events across multiple log sources
- 📌 MITRE: `T1110` Brute Force · `T1071.004` DNS · `T1046` Network Service Scanning

→ [View Lab](https://github.com/rohithbaggu56-dot/Splunk-SIEM-Practice-Notes/blob/main/README.md)

---

### 🔴 pfSense Firewall – Network Segmentation & Traffic Control

Deployed pfSense as the network gateway controlling all traffic between lab VMs. Configured firewall rules, verified blocking behavior, and analyzed logs showing real blocked connection attempts.

- Configured LAN firewall rules and applied a block rule for the Kali attacker machine. Ping test confirmed 100% packet loss after rule was applied
- Reviewed firewall logs showing 170 blocked attempts from 192.168.1.101 targeting both external DNS and Wazuh manager port 1514
- Identified the blocked TCP traffic was targeting port 1514, the Wazuh agent communication port
- 📌 MITRE: `T1046` Network Service Scanning · `T1562.004` Disable or Modify System Firewall

→ [View Lab](https://github.com/rohithbaggu56-dot/pfsense-firewall-lab)

---

### 🔴 Log Analysis & Raw Event Investigation

Windows and Linux log analysis focused on reading raw event data and identifying suspicious activity without relying on SIEM alerts.

- Identified repeated Event ID 4625 failures followed by a 4740 account lockout and flagged the sequence as a brute force indicator
- Went through Linux auth.log manually and identified sudo escalation attempts alongside abnormal SSH login patterns
- Documented a personal IOC extraction workflow: event ID to log field to indicator to classification
- 📌 MITRE: `T1110.001` Password Guessing · `T1078` Valid Accounts

→ [View Lab](https://github.com/rohithbaggu56-dot/Log-Analysis-Detection-Notes)

---

### 🔴 AI-Assisted SOC Triage Pipeline

Followed and implemented a Python automation pipeline simulating a basic SOAR-style workflow — capturing live traffic, detecting suspicious IPs, generating structured JSON alerts, and routing them to a published AI agent for automated triage.

- Implemented tshark packet capture, CSV conversion, IP threshold analysis, and JSON alert generation in a five-stage Python pipeline
- Configured and published an Airia AI agent trained on a custom SOC playbook with risk scoring, MITRE mapping, and escalation logic
- Pipeline successfully detected 70 ICMP packets from attacker IP, generated alert SOC-CC95AA8A, and received structured triage response with HTTP 200

→ [View Lab](https://github.com/rohithbaggu56-dot/AIRIA-AI-Log-Triage-Lab)

---

## 📁 Repository Structure

```
SOC-Home-Lab/
├── incidents/
│   ├── IR-001-brute-force.md
│   ├── IR-002-web-attacks.md
│   ├── IR-003-phishing.md
│   ├── IR-004-splunk-detection.md
│   └── IR-005-log-analysis.md
├── detection-rules/
│   ├── virustotal-active-response-rule.xml
│   └── sysmon-false-positive-suppression.xml
├── scripts/
│   └── remove-threat.sh
└── dashboards/
    └── (coming soon — Wazuh dashboard screenshots)
```

---

⬅️ [Back to Portfolio](https://github.com/rohithbaggu56-dot)
