# Dana Bot 

> **Network Forensics & Threat Intelligence Investigation using Wireshark**

![Platform](https://img.shields.io/badge/Platform-CyberDefenders-blue)
![Category](https://img.shields.io/badge/Category-Network%20Forensics-green)
![Tool](https://img.shields.io/badge/Tool-Wireshark%20%7C%20Threat%20Intelligence-orange)

---

# Overview

This repository documents my investigation process while completing the **DanaBot** challenge on CyberDefenders.

Rather than publishing challenge answers, this write-up focuses on **how I analysed network traffic**, **how I reconstructed the malware delivery chain**, and **what I learned** throughout the investigation. The objective is to demonstrate practical SOC investigation techniques by combining packet analysis with threat intelligence and basic malware analysis.

---

# Scenario

The SOC detected suspicious outbound network activity originating from an internal workstation. Initial investigation indicated that sensitive company information had been compromised.

Using a provided **PCAP** file, my objective was to identify the initial infection vector, reconstruct the malware execution chain, analyse downloaded payloads, and collect indicators of compromise that could support incident response and future threat hunting.

---

# Tools Used

* Wireshark
* VirusTotal
* JavaScript Deobfuscation Tools
* Linux Hash Utilities
* Threat Intelligence Platforms

---

# Investigation Workflow

```text
Load PCAP File
        │
        ▼
Review Network Traffic
        │
        ▼
Identify Initial Access
        │
        ▼
Extract HTTP Objects
        │
        ▼
Analyse Downloaded Files
        │
        ▼
Investigate Malware Behaviour
        │
        ▼
Collect Indicators of Compromise
        │
        ▼
Build Attack Timeline
```

Instead of searching directly for challenge answers, I followed the malware infection chronologically—from the first network connection through payload delivery and execution.

---

# Investigation Walkthrough

---

## Objective 1 – Identify Initial Access

### My Approach

I began by reviewing DNS and HTTP traffic to determine where the compromised host first communicated externally.

Rather than focusing on isolated packets, I analysed the sequence of requests to identify suspicious domains and their corresponding infrastructure.

### Why I Looked There

DNS requests often reveal the first interaction between a compromised host and attacker-controlled infrastructure.

### Skills Practiced

* DNS Analysis
* Network Traffic Investigation
* IOC Identification

### What I Learned

DNS traffic frequently provides the earliest evidence of malicious communication during an intrusion.

---

## Objective 2 – Investigate Delivered Files

### My Approach

After identifying suspicious communications, I exported HTTP objects from the PCAP and reviewed downloaded files.

I compared filenames, MIME types, and file characteristics to determine which downloads required further investigation.

### Why I Looked There

HTTP object extraction allows investigators to recover malware delivered during an attack without requiring endpoint access.

### Skills Practiced

* HTTP Object Extraction
* Malware Delivery Analysis
* File Identification

### What I Learned

File metadata and content types often reveal suspicious downloads that warrant deeper analysis.

---

## Objective 3 – Analyse the Initial Payload

### My Approach

Once I identified the suspicious file, I inspected its contents to determine whether it contained obfuscated or encoded code.

After recognising signs of obfuscation, I used a JavaScript deobfuscation tool to understand the script's behaviour and execution flow.

### Why I Looked There

Attackers commonly obfuscate scripts to evade detection and hinder manual analysis.

### Skills Practiced

* JavaScript Analysis
* Code Deobfuscation
* Malware Behaviour Analysis

### What I Learned

Deobfuscation transforms unreadable scripts into valuable sources of behavioural intelligence.

---

## Objective 4 – Investigate Malware Execution

### My Approach

After understanding the script logic, I analysed how it interacted with the operating system and what Windows components it leveraged to execute additional payloads.

Instead of focusing only on downloaded files, I examined the complete execution chain initiated by the script.

### Why I Looked There

Execution mechanisms explain how malware transitions from delivery to active compromise.

### Skills Practiced

* Windows Process Analysis
* Malware Execution Investigation
* Behaviour Analysis

### What I Learned

Attackers frequently abuse legitimate Windows components to execute malicious code while blending into normal system activity.

---

## Objective 5 – Analyse Secondary Payload Delivery

### My Approach

Next, I followed the script's download logic to identify any additional payloads retrieved during execution.

I correlated HTTP traffic with the script's behaviour to understand the complete infection chain.

### Why I Looked There

Modern malware commonly downloads secondary payloads instead of embedding all functionality in the initial infection.

### Skills Practiced

* Payload Analysis
* Network Correlation
* Multi-stage Malware Investigation

### What I Learned

Understanding secondary payload delivery is essential for determining the full scope of an infection.

---

## Objective 6 – Collect Indicators of Compromise

### My Approach

Finally, I generated cryptographic hashes and collected network indicators associated with the recovered files.

Rather than relying on a single indicator, I documented multiple artifacts that could support detection and threat hunting activities.

### Why I Looked There

Reliable indicators of compromise improve detection, incident response, and future investigations.

### Skills Practiced

* IOC Collection
* Hash Generation
* Threat Hunting

### What I Learned

Combining network indicators with file-based indicators provides stronger detection coverage.

---

# Network Artifacts Explored

| Artifact            | Purpose                           |
| ------------------- | --------------------------------- |
| DNS Queries         | Identify attacker infrastructure  |
| HTTP Requests       | Investigate malware delivery      |
| HTTP Objects        | Recover downloaded files          |
| JavaScript Files    | Analyse initial payload           |
| HTTP Headers        | Validate downloaded content       |
| File Hashes         | Generate indicators of compromise |
| Network Connections | Reconstruct attack timeline       |

---

# MITRE ATT&CK Mapping

| Attack Phase          | Technique                         |
| --------------------- | --------------------------------- |
| Initial Access        | Phishing                          |
| Execution             | Command and Scripting Interpreter |
| Defense Evasion       | Obfuscated Files or Information   |
| Command and Control   | Application Layer Protocol        |
| Ingress Tool Transfer | Transfer Additional Payloads      |

---

# Skills Gained

* Network Forensics
* Wireshark Analysis
* DNS Investigation
* HTTP Object Extraction
* JavaScript Deobfuscation
* Malware Behaviour Analysis
* IOC Collection
* Threat Intelligence
* Windows Execution Analysis
* Attack Timeline Reconstruction
* Incident Response Methodology
* MITRE ATT&CK Mapping

---

# Defensive Recommendations

* Monitor unusual DNS queries to newly observed domains.
* Inspect HTTP downloads with uncommon content types.
* Detect execution of scripts through Windows scripting engines.
* Monitor abnormal use of legitimate Windows utilities.
* Block known malicious domains and file hashes through threat intelligence feeds.
* Correlate network-based and host-based telemetry during investigations.
* Deploy endpoint detection capable of identifying script-based malware execution.

---

# Key Takeaways

* Network captures often contain the complete malware delivery chain.
* HTTP object extraction enables investigators to recover malware directly from network traffic.
* JavaScript obfuscation is a common technique used to hide malicious behaviour.
* Behaviour analysis provides more value than relying solely on antivirus detections.
* Combining network forensics with threat intelligence produces a more complete understanding of an attack.

---

# Reflection

This challenge strengthened my understanding of network forensics by demonstrating how malware infections can be reconstructed entirely from packet captures.

Instead of focusing solely on identifying malicious files, I learned how to follow the complete infection chain—from DNS resolution and payload delivery to script execution, secondary payload retrieval, and indicator collection.

The investigation improved my confidence in using Wireshark to analyse malicious traffic, extracting network-delivered malware, interpreting obfuscated JavaScript, and documenting findings using a structured SOC investigation methodology.

The biggest lesson from this lab was that effective malware investigations require combining **network evidence, malware behaviour analysis, and threat intelligence** to understand both the technical details and the broader attack lifecycle.

---

> **Note:** This repository intentionally excludes challenge answers to respect the CyberDefenders platform. Its purpose is to document the investigation methodology, network forensic techniques, and practical skills gained while completing the lab.
