# Ramnit

> **Endpoint Memory Forensics Investigation using Volatility 3 & Threat Intelligence**

![Platform](https://img.shields.io/badge/Platform-CyberDefenders-blue)
![Category](https://img.shields.io/badge/Category-Endpoint%20Forensics-green)
![Tool](https://img.shields.io/badge/Tool-Volatility%203%20%7C%20VirusTotal-orange)

---

# Overview

This repository documents my investigation process while completing the **Ramnit** challenge on CyberDefenders.

Rather than publishing challenge answers, this write-up focuses on **how I investigated a Windows memory dump**, **how I identified malware artifacts using Volatility 3**, and **what I learned** throughout the investigation.

The objective was to perform memory forensics, identify the malicious process, recover useful indicators of compromise (IOCs), and enrich the findings using external threat intelligence.

---

# Scenario

An Intrusion Detection System (IDS) generated an alert indicating suspicious activity on a Windows workstation. A memory dump was collected from the compromised machine for forensic investigation.

My objective was to examine the memory image, identify malicious processes, recover executable artifacts, investigate network activity, and correlate the findings with external intelligence sources to understand the malware's behavior.

---

# Tools Used

* Volatility 3
* VirusTotal
* SHA1 Hash Utilities
* Threat Intelligence Platforms
* Linux Terminal

---

# Investigation Workflow

```text
Acquire Memory Dump
        │
        ▼
Enumerate Running Processes
        │
        ▼
Identify Suspicious Process
        │
        ▼
Recover Process Information
        │
        ▼
Investigate Network Connections
        │
        ▼
Extract Malware from Memory
        │
        ▼
Generate File Hashes
        │
        ▼
Correlate with Threat Intelligence
        │
        ▼
Document Indicators of Compromise
```

Instead of searching directly for challenge answers, I followed a standard DFIR workflow commonly used during memory forensic investigations.

---

# Investigation Walkthrough

---

## Objective 1 – Identify the Suspicious Process

### My Approach

I began by listing every running process present in the memory image using Volatility.

Instead of assuming a process was malicious based solely on its name, I reviewed the complete process list and looked for unusual executables, suspicious parent-child relationships, and processes executing from unexpected locations.

### Why I Looked There

Running processes provide one of the quickest ways to identify malware that was active when the memory capture was taken.

### Skills Practiced

* Memory Forensics
* Process Enumeration
* Suspicious Process Identification

### What I Learned

Memory analysis provides a snapshot of system activity that may no longer exist on disk after malware removes itself.

---

## Objective 2 – Investigate the Executable

### My Approach

After identifying the suspicious process, I examined its command-line arguments and executable path.

Rather than relying only on the process name, I validated where the executable originated on the victim system.

### Why I Looked There

Malware often executes from temporary or user-accessible directories instead of legitimate system locations.

### Skills Practiced

* Process Investigation
* Command-Line Analysis
* Windows Artifact Analysis

### What I Learned

Executable paths frequently provide valuable context regarding how malware was introduced onto a system.

---

## Objective 3 – Analyse Network Activity

### My Approach

Next, I investigated active and recently established network connections associated with the suspicious process.

I correlated process identifiers with network artifacts to determine whether the malware attempted to communicate externally.

### Why I Looked There

Network connections reveal potential command-and-control infrastructure and attacker communication channels.

### Skills Practiced

* Network Forensics
* Volatility Network Analysis
* IOC Identification

### What I Learned

Memory images preserve network artifacts that may not be available after a compromised system is shut down.

---

## Objective 4 – Correlate Threat Intelligence

### My Approach

After identifying suspicious network indicators, I pivoted to external threat intelligence platforms to gather additional context about the observed infrastructure.

Rather than relying solely on forensic evidence, I enriched my findings using publicly available intelligence.

### Why I Looked There

Threat intelligence helps determine whether observed infrastructure has been associated with previous malicious activity.

### Skills Practiced

* Threat Intelligence
* IOC Enrichment
* OSINT Investigation

### What I Learned

External intelligence transforms isolated indicators into actionable security information.

---

## Objective 5 – Recover the Malware

### My Approach

Once the malicious process had been identified, I extracted the executable directly from the memory image using Volatility.

Recovering the executable allowed me to generate cryptographic hashes and perform additional malware validation.

### Why I Looked There

Recovered malware samples can be analysed independently and compared against known malware databases.

### Skills Practiced

* Memory Artifact Recovery
* Malware Extraction
* File Recovery

### What I Learned

Memory dumps often contain recoverable malware even when files are no longer available on disk.

---

## Objective 6 – Generate File Hashes

### My Approach

After extracting the executable, I generated its cryptographic hash to uniquely identify the malware sample.

The resulting hash was then used for reputation checks and malware intelligence.

### Why I Looked There

File hashes provide reliable indicators for malware identification, detection, and threat hunting.

### Skills Practiced

* Hash Generation
* Malware Identification
* IOC Collection

### What I Learned

Cryptographic hashes are fundamental indicators used across DFIR and SOC investigations.

---

## Objective 7 – Investigate Malware Intelligence

### My Approach

Using the recovered hash, I searched threat intelligence platforms to collect additional malware metadata, including compilation information and associated infrastructure.

Rather than treating the recovered executable as an isolated artifact, I enriched the investigation using external malware intelligence.

### Why I Looked There

Threat intelligence platforms provide historical context unavailable through memory analysis alone.

### Skills Practiced

* Malware Intelligence
* IOC Correlation
* Threat Research

### What I Learned

Combining forensic artifacts with external intelligence provides a much clearer picture of malware behaviour.

---

# Volatility Plugins Explored

| Plugin              | Purpose                                          |
| ------------------- | ------------------------------------------------ |
| `windows.pslist`    | Enumerate running processes                      |
| `windows.cmdline`   | View executable paths and command-line arguments |
| `windows.netscan`   | Identify network connections                     |
| `windows.dumpfiles` | Recover files from memory                        |

---

# MITRE ATT&CK Mapping

| Attack Phase        | Technique                    |
| ------------------- | ---------------------------- |
| Execution           | User Execution               |
| Defense Evasion     | Masquerading                 |
| Command and Control | Application Layer Protocol   |
| Discovery           | System Information Discovery |

---

# Skills Gained

* Memory Forensics
* Windows Memory Analysis
* Volatility 3
* Process Investigation
* Command-Line Analysis
* Network Artifact Analysis
* Malware Extraction
* IOC Collection
* Threat Intelligence
* VirusTotal Analysis
* Malware Attribution
* DFIR Investigation Methodology

---

# Defensive Recommendations

* Monitor unusual process execution from user directories.
* Collect memory images during incident response whenever possible.
* Correlate process activity with network connections.
* Integrate threat intelligence into SOC investigations.
* Monitor outbound communications to suspicious infrastructure.
* Validate executable hashes against malware intelligence feeds.
* Deploy endpoint monitoring capable of detecting abnormal process behaviour.

---

# Key Takeaways

* Memory forensics captures valuable evidence unavailable through disk analysis alone.
* Volatility provides powerful capabilities for analysing running processes and memory artifacts.
* Process paths and command-line arguments provide important investigation context.
* Network artifacts recovered from memory help identify command-and-control activity.
* Threat intelligence significantly improves the value of forensic investigations by enriching recovered indicators.

---

# Reflection

This challenge strengthened my understanding of endpoint memory forensics by demonstrating how malware investigations can be performed using a Windows memory image.

Instead of relying solely on antivirus detections, I learned how to enumerate running processes, investigate suspicious executables, analyse network activity, recover malware directly from memory, generate indicators of compromise, and enrich findings using external threat intelligence.

The investigation improved my confidence in using **Volatility 3** during DFIR investigations and reinforced the importance of correlating **memory artifacts, network evidence, and threat intelligence** to understand the complete scope of an incident.

The biggest lesson from this lab was that **memory is one of the richest sources of forensic evidence**, often containing processes, network connections, and malware artifacts that may no longer exist on disk.

---

> **Note:** This repository intentionally excludes challenge answers to respect the CyberDefenders platform. Its purpose is to document the investigation methodology, memory forensic techniques, and practical skills gained while completing the lab.
