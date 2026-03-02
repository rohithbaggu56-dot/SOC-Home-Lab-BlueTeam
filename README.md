# 🏠 Home SOC Lab – Detection, Log Analysis & Network Investigation
![Splunk](https://img.shields.io/badge/Splunk-SIEM-000000?style=for-the-badge&logo=splunk&logoColor=white)
![Wazuh](https://img.shields.io/badge/Wazuh-EDR%20%2F%20HIDS-005571?style=for-the-badge&logo=wazuh&logoColor=white)
![pfSense](https://img.shields.io/badge/pfSense-Firewall-212121?style=for-the-badge&logo=pfsense&logoColor=white)
![Wireshark](https://img.shields.io/badge/Wireshark-Network_Analysis-1679A7?style=for-the-badge&logo=wireshark&logoColor=white)
![Windows](https://img.shields.io/badge/Windows_Event_Logs-0078D6?style=for-the-badge&logo=windows&logoColor=white)
![Linux](https://img.shields.io/badge/Linux_Log_Analysis-333333?style=for-the-badge&logo=linux&logoColor=white)
![AI Log Analysis](https://img.shields.io/badge/AI-Agent%20Log%20Triage-6A5ACD?style=for-the-badge&logo=openai&logoColor=white)

A multi-VM Security Operations Center (SOC) home lab built to simulate real-world blue team workflows including log monitoring, alert investigation, network analysis, and threat detection.

This lab focuses on understanding **how attacks appear in logs**, how analysts investigate alerts, and how security tools work together inside a monitored environment.

---

## 🎯 Project Summary

This project demonstrates a self-built SOC environment created using virtual machines and open-source security tools.  
The lab simulates enterprise-style monitoring where system logs, network traffic, and security events are analyzed to identify suspicious activity.

The goal was not penetration testing, but **defensive security and SOC analyst skill development**.


## 🎯 Project Scope

This lab focuses on:

✅ Detection & monitoring  
✅ Log investigation  
✅ Network analysis  
✅ SOC workflow understanding  

This project does **not** simulate production infrastructure but serves as a controlled learning environment.


## 🎯 Objectives

- Build an isolated cybersecurity lab using virtualization
- Practice Windows and Linux log investigation
- Perform SOC-style alert triage and analysis
- Understand attacker behavior through logs and traffic
- Gain hands-on experience with SIEM and monitoring tools
- Develop investigation and detection thinking

---

## 🏗️ Lab Architecture
<img width="2816" height="1536" alt="Gemini_Generated_Image_9zlyo09zlyo09zly" src="https://github.com/user-attachments/assets/16442680-488c-46d7-84b9-a7e51915e88e" />

The environment consists of multiple virtual machines connected within an isolated network.

### Virtual Machines

- **Ubuntu Server**
  - Log analysis
  - Security monitoring
  - SSH authentication investigation

- **Windows 10**
  - Event Viewer analysis
  - Security log monitoring
  - User activity investigation

- **Kali Linux**
  - Traffic generation
  - Network testing scenarios
  - Security analysis tools


## 🛠️ Technologies & Tools Used

### SIEM & Monitoring
- Splunk (Log ingestion & dashboards)
- Wazuh (Host-based monitoring – explored separately)

### Network & Traffic Analysis
- Wireshark
- TCPDump
- DNS traffic inspection

### Operating Systems
- Windows 10
- Ubuntu Linux
- Kali Linux

### Network Security
- pfSense Firewall (network segmentation – dedicated lab)

### AI Security Experimentation
- AIRIA AI Agent (log triage experimentation – separate project)


## 🔎 Skills Practiced

- Log Analysis & Alert Investigation
- SIEM Monitoring Concepts
- Network Traffic Analysis
- Windows Event Log Investigation
- Linux Authentication Log Analysis
- Incident Investigation Workflow
- IOC Identification
- Security Event Correlation


## 🧠 Investigation Workflow Practiced

Typical analysis approach followed in the lab:

1. Generate activity inside lab environment
2. Collect logs from systems
3. Search and filter events
4. Identify suspicious patterns
5. Extract Indicators of Compromise (IOCs)
6. Validate findings using multiple data sources
7. Document investigation results

This workflow mirrors entry-level SOC analyst processes.


## 📊 Log Analysis Performed

### Windows Investigation
- Security Event Log review
- Login activity monitoring
- Failed authentication tracking
- Event correlation using Event IDs

### Linux Investigation
- SSH authentication logs analysis
- Failed login detection
- Brute-force behavior identification
- Suspicious IP investigation

Example log sources:
- /var/log/auth.log
- OpenSSH authentication logs
- windows Security Logs
  

## 🌐 Network Traffic Analysis

Network activity was analyzed to understand communication patterns and detect anomalies.

Activities included:

- DNS request/response inspection
- Packet capture analysis
- Traffic filtering using Wireshark
- Identifying unusual connections
- Understanding attacker footprints in traffic


## 🧩 Extended Lab Components

As the lab evolved, additional security technologies were explored in dedicated repositories:

- 🔥 **pfSense Firewall Lab**  
  Network segmentation, firewall rules, and traffic control  
  👉 → [View pfSense Lab Repository](https://github.com/rohithbaggu56-dot/pfsense-firewall-lab)


- 🛡 **Wazuh SIEM Monitoring Lab**  
  Host-based monitoring and alert visibility  
  → [View Wazuh Lab Repository](https://github.com/rohithbaggu56-dot/Wazuh-SIEM-SOC-Hands-On-Lab/blob/main/README.md)


- 🤖 **AIRIA AI Log Triage Lab**  
  Experimenting with AI-assisted investigation workflows  
   → [View AIRIA AI Lab Repository](https://github.com/rohithbaggu56-dot/AIRIA-AI-Log-Triage-Lab))

These components expand the SOC environment but are documented separately for clarity.

## 🔎 Analyst Perspective

This lab was approached from a SOC analyst viewpoint rather than a penetration testing perspective.

Focus areas included:
- Understanding attacker behavior through logs
- Investigating alerts step-by-step
- Validating suspicious activity using multiple data sources
- Building investigation reasoning instead of tool memorization

---
## 📸 Investigation & Lab Evidence

**1. Virtualized Home SOC Lab Environment (local VMs, NAT networking)**
<img width="1920" height="1080" alt="Screenshot 2026-03-02 111835" src="https://github.com/user-attachments/assets/0c801d9a-ac58-430b-a56f-3a5adf110e37" />


**2. Windows Event Viewer – Security Event Logs (Windows 10 VM)**
<img width="1897" height="689" alt="Windows-Event-Viewer" src="https://github.com/user-attachments/assets/dc5c4cb2-2582-453b-aece-2482591ab5b2" />


**3. Linux authentication log analysis (OpenSSH)**
<img width="1910" height="922" alt="Ubuntu-SSH-log analysis" src="https://github.com/user-attachments/assets/decf839d-d7b9-46de-9258-ac9d1bc41660" />
OpenSSH log file analyzed for practice and investigation purposes.



**4. Splunk – DNS Log Analysis**
<img width="1920" height="961" alt="Splunk-Dns log-Search" src="https://github.com/user-attachments/assets/61901e89-5de8-48bc-8273-ee437e07fa6a" />


**5. Wireshark – DNS Response Analysis**
<img width="1903" height="975" alt="Wireshark-Dsn analysis" src="https://github.com/user-attachments/assets/e5ff993d-f406-45d2-92b5-ca0830d61c57" />

---
## 📈 Key Learning Outcomes

- Understood how attacker behavior appears in logs
- Learned differences between normal vs suspicious activity
- Practiced SOC investigation methodology
- Built dashboards for log visibility
- Improved detection-focused mindset
- Gained practical blue team experience


## 🚀 Future Improvements

- Integrate Wazuh alerts into Splunk
- Automate alert correlation
- Expand detection use cases
- Centralized log pipeline
- AI-assisted investigation workflows

---

## 📌 Key Takeaway

Security monitoring is not about tools alone, it is about understanding behavior, patterns, and investigation logic.

This lab represents practical steps toward becoming a SOC Analyst by learning **how defenders observe and respond to threats**.
