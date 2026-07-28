# RedLine — Lab


> **Platform:** CyberDefenders
> **Category:** Digital Forensics / Memory Forensics / Malware Analysis
> **Focus:** Memory Analysis / Incident Investigation / DFIR
> **Difficulty:** Blue Team / DFIR Lab

## Overview

This repository documents my learning experience from the **RedLine Lab** on CyberDefenders.

The lab focuses on analyzing a compromised system using **memory forensics** techniques to investigate an attack, identify suspicious processes, trace attacker activity, analyze network connections, and determine the malware and artifacts associated with the compromise.

The investigation involved analyzing a memory dump using tools such as **Volatility 3** and standard forensic utilities to identify indicators of compromise and reconstruct parts of the attacker's activity.

---

## Objectives

* Analyze a memory dump from a compromised system.
* Identify suspicious and potentially malicious processes.
* Investigate process relationships and child processes.
* Analyze suspicious memory regions.
* Identify malicious memory protection characteristics.
* Investigate network connections associated with suspicious processes.
* Identify the attacker's IP address.
* Trace attacker activity through memory artifacts.
* Identify the URL accessed by the attacker.
* Locate the full path of a malicious executable.
* Develop practical memory forensics and incident investigation skills.

---

## Investigation Methodology

During this lab, I approached the investigation from the perspective of a **DFIR analyst** investigating a potentially compromised Windows system.

My investigation process included:

* Enumerating running processes from the memory image.
* Identifying processes that appeared suspicious or anomalous.
* Investigating process relationships and child processes.
* Analyzing suspicious memory regions using Volatility.
* Examining active network connections.
* Correlating suspicious processes with network activity.
* Searching memory for attacker-related artifacts.
* Identifying malicious files and their locations.
* Connecting multiple indicators to reconstruct the attack activity.

This approach helped me understand how memory forensics can be used to investigate an incident even when traditional filesystem-based evidence may be incomplete or unavailable.

---

## Tools Used

### Volatility 3

Used for memory analysis and investigation of:

* Running processes
* Process relationships
* Network connections
* Suspicious memory regions
* In-memory file objects

### Strings

Used to extract readable strings from the memory dump and search for potential indicators such as:

* IP addresses
* URLs
* File paths
* Other textual artifacts

---

## Investigation Areas

### Process Analysis

The first stage of the investigation involved enumerating processes present in the memory dump.

The goal was to identify:

* Unusual process names
* Suspicious executables
* Unexpected process relationships
* Potentially malicious processes

A suspicious executable was identified during the process investigation and was used as a starting point for further analysis.

---

### Process Relationship Analysis

After identifying the suspicious process, I investigated its process relationships to determine whether it had spawned any child processes.

Understanding parent-child process relationships can help identify suspicious execution chains and provide additional context about how malware operates within a compromised system.

---

### Memory Analysis

The suspicious process was further analyzed to identify potentially injected or malicious memory regions.

The investigation focused on memory protection characteristics associated with the process.

A memory region with **PAGE_EXECUTE_READWRITE** permissions was identified.

This type of memory protection allows a memory region to be:

* Read
* Written
* Executed

The combination of write and execute permissions can be suspicious in a forensic investigation because it may indicate techniques such as code injection or shellcode execution.

However, memory protection alone should be treated as an indicator requiring further investigation rather than definitive proof of malicious activity.

---

### Network Investigation

The next stage involved investigating network connections associated with the suspicious process.

The objective was to identify:

* Remote IP addresses
* Local and remote ports
* Connection states
* Processes associated with network activity

By correlating network connections with the suspicious process, I was able to identify a potentially attacker-controlled IP address associated with the incident.

---

### Attacker Activity Analysis

The identified network indicator was then used to search the memory dump for additional artifacts.

This investigation revealed evidence of a URL associated with the attacker infrastructure.

This demonstrated how network indicators can be used as pivot points during forensic investigations to uncover additional evidence.

---

### Malicious File Analysis

The investigation also involved locating the malicious executable within the memory image.

File scanning was used to identify the full path associated with the suspicious executable.

This provided additional context about where the malicious file was located on the compromised system and helped establish another Indicator of Compromise (IOC).

---

## Investigation Workflow

```text
Memory Dump
     │
     ▼
Process Enumeration
     │
     ▼
Identify Suspicious Process
     │
     ▼
Analyze Process Relationships
     │
     ▼
Investigate Suspicious Memory
     │
     ▼
Analyze Network Connections
     │
     ▼
Identify Attacker Infrastructure
     │
     ▼
Search Memory for Additional Artifacts
     │
     ▼
Locate Malicious File
     │
     ▼
Correlate Indicators of Compromise
     │
     ▼
Reconstruct Attacker Activity
```

---

## Key Findings

During the investigation, the following categories of evidence were identified:

| Evidence Type       | Finding                                    |
| ------------------- | ------------------------------------------ |
| Suspicious Process  | Malicious executable identified            |
| Child Process       | Suspicious process relationship identified |
| Memory Protection   | PAGE_EXECUTE_READWRITE                     |
| VPN-Related Process | VPN connection process identified          |
| Network Indicator   | Attacker-associated IP address identified  |
| Web Artifact        | Attacker-accessed PHP resource identified  |
| Malicious File      | Full executable path identified            |

> Specific challenge answers and indicators are intentionally not included in this section to keep the write-up focused on investigation methodology and learning.

---

## Skills Gained

After completing this lab, I became more confident in:

* Memory forensics
* Windows memory analysis
* Volatility 3
* Process analysis
* Process tree investigation
* Malware investigation
* Network connection analysis
* IOC identification
* Artifact correlation
* Incident investigation
* DFIR methodology

---

## SOC Analyst Relevance

This lab is highly relevant to my goal of becoming a **SOC Analyst** because it demonstrates how analysts can investigate a compromised endpoint using forensic evidence.

The investigation process helped me understand how different artifacts can be correlated during an incident:

```text
Suspicious Process
        │
        ▼
Process Relationship
        │
        ▼
Memory Artifact
        │
        ▼
Network Connection
        │
        ▼
Attacker IP
        │
        ▼
URL / Infrastructure
        │
        ▼
Malicious File
        │
        ▼
Incident Reconstruction
```

The ability to correlate these indicators is important for SOC and DFIR teams when determining:

* What happened?
* How did the attacker gain access?
* What processes were involved?
* What systems or resources were accessed?
* What infrastructure did the attacker communicate with?
* What artifacts remain on the compromised system?

This investigation also strengthened my understanding of how **memory forensics complements SIEM and endpoint monitoring** during incident response.

---

## Key Takeaways

The RedLine Lab demonstrated the importance of memory forensics in incident investigation. A memory image can contain valuable evidence about running processes, network connections, suspicious memory regions, and other artifacts that may help reconstruct attacker activity.

One of the key lessons from this lab was the importance of **correlating multiple pieces of evidence** rather than relying on a single indicator. A suspicious process becomes more significant when it can be correlated with unusual memory permissions, network connections, attacker infrastructure, and malicious files.

The lab also reinforced the importance of tools such as **Volatility 3** for extracting forensic evidence from memory dumps and supporting investigations into compromised systems.

---

## Conclusion

The **RedLine Lab** provided practical experience in **memory forensics, malware investigation, and digital incident response**.

By analyzing a memory dump and correlating process information, memory artifacts, network activity, and malicious file evidence, I gained a better understanding of how DFIR analysts investigate compromised systems and reconstruct attacker activity.

This lab strengthened my knowledge of **Volatility 3, Windows memory analysis, IOC identification, and forensic investigation**, which are valuable skills for pursuing a career in **SOC Analysis, Incident Response, Digital Forensics, and Threat Hunting**.

---

## Disclaimer

This write-up is created for educational and cybersecurity learning purposes.

All investigation activities were performed within an authorized CyberDefenders training environment. The techniques and tools documented here should only be used for legitimate security investigations and authorized forensic analysis.
