# Introduction to EDR & Initial Access Scenario

## Goal / Objective
Understand the fundamentals of **Endpoint Detection and Response (EDR)** and how SOC analysts leverage it to detect, investigate, and respond to threats at the endpoint level.

---

## Key Terms / Concepts
- **EDR (Endpoint Detection and Response):** A host-based security solution for detecting and responding to endpoint threats  
- **Endpoint:** Any device connected to the network (laptop, server, workstation)  
- **Telemetry:** Detailed data collected from endpoints (processes, registry, files, user activity)  
- **Detection:** Identifying suspicious or malicious behavior using signatures and behavior analysis  
- **Containment:** Preventing the spread of a threat (e.g., endpoint isolation)  
- **Investigation:** Analyzing endpoint activity to validate alerts  
- **IOC:** Indicator of Compromise (hashes, IPs, domains)  
- **IOA:** Indicator of Attack (malicious behaviors)

---

## EDR Overview
Endpoint Detection and Response (EDR) solutions deploy lightweight agents (sensors) on endpoints to continuously collect telemetry such as process execution, registry modifications, file changes, and user actions. This data is correlated and analyzed using signature-based and behavior-based detection techniques, often enhanced with machine learning, to identify malicious activity and advanced threats.

### Core Features of EDR
- **Visibility:** Deep, real-time visibility into endpoint activities and system changes  
- **Detection:** Identification of threats using signatures, behavioral analysis, and IOAs  
- **Response:** Actions such as isolating endpoints, terminating processes, and quarantining files

### Threats Detected by EDR
- Malware and suspicious executable files  
- Abnormal process behavior and persistence mechanisms  
- Command and Control (C2) communications over common protocols such as HTTP, HTTPS, and DNS

### Tips / Notes
- EDR is primarily focused on endpoint-level visibility and does not replace network-based security solutions such as NDR or IDS  
- An EDR agent is also known as a **Sensor**  
- Configuration settings in Windows systems are primarily stored in the **Windows Registry**

---

## Scenario: Initial Access via Malicious Office Document

**Summary:**  
An EDR alert was triggered after a macro-enabled Microsoft Office document (**invoice.docm**) was opened by **alice.thomas** on **DESKTOP-HR01**. The document spawned CMD.exe, which used cURL to download a payload. The payload was dropped to disk but quarantined by the EDR, preventing execution. The activity maps to **MITRE ATT&CK Initial Access – T1566.001 (Spearphishing Attachment)**.

---

## Evidence

### Evidence 1 – Malicious Document Execution
The user opened a macro-enabled Office document (**invoice.docm**) using WINWORD.EXE. The document spawned CMD, initiating the first step of the malicious activity chain.  



---

### Evidence 2 – Command Execution via Macro
The Office macro triggered CMD.EXE, an abnormal child process for Word, indicating potential malware execution.  



---

### Evidence 3 – Payload Download via cURL
CMD.EXE launched cURL to download a payload from an external domain, consistent with staging behavior rather than immediate execution.  



---

### Evidence 4 – Dropped Payload (install.exe)
The downloaded file (**install.exe**) was saved to disk in the Public folder. The payload was suspicious, unsigned, and known in malware campaigns. EDR quarantined the file before execution.  



---

### Evidence 5 – MITRE ATT&CK Mapping
The activity was mapped to MITRE ATT&CK Initial Access, specifically T1566.001 – Spearphishing Attachment, confirming phishing as the initial infection vector.  



