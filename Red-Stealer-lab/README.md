# CyberDefenders – Red Stealer

> **Threat Intelligence Investigation using VirusTotal, MalwareBazaar & ThreatFox**

![Platform](https://img.shields.io/badge/Platform-CyberDefenders-blue)
![Category](https://img.shields.io/badge/Category-Threat%20Intelligence-green)
![Tool](https://img.shields.io/badge/Tool-VirusTotal%20%7C%20MalwareBazaar%20%7C%20ThreatFox-orange)

---

# Overview

This repository documents my investigation process while completing the **Red Stealer** challenge on CyberDefenders.

Instead of publishing challenge answers, this write-up explains **how I investigated a malware sample using threat intelligence platforms**, **how I gathered Indicators of Compromise (IOCs)**, and **what I learned** throughout the investigation.

The primary objective was to profile the malware, identify its infrastructure, understand its capabilities, map its behaviour to the MITRE ATT&CK framework, and enrich the investigation using multiple intelligence sources.

---

# Scenario

A suspicious executable was identified within the environment, and only its file hash was available for investigation.

My objective was to leverage public threat intelligence platforms to identify the malware family, understand its behavior, collect actionable IOCs, investigate command-and-control infrastructure, and document the techniques used by the malware.

---

# Tools Used

* VirusTotal
* MalwareBazaar
* ThreatFox
* WHOIS
* ANY.RUN
* MITRE ATT&CK Framework

---

# Investigation Workflow

```text
Start with Malware Hash
        │
        ▼
Identify Malware Family
        │
        ▼
Review Sample Metadata
        │
        ▼
Analyse Behaviour Report
        │
        ▼
Collect Network IOCs
        │
        ▼
Investigate Threat Intelligence
        │
        ▼
Map MITRE ATT&CK Techniques
        │
        ▼
Document Findings
```

Rather than searching directly for challenge answers, I followed the same workflow that a SOC analyst or Threat Intelligence analyst would use when profiling an unknown malware sample.

---

# Investigation Walkthrough

---

## Objective 1 – Identify the Malware

### My Approach

I began by searching the provided file hash on VirusTotal to determine whether the sample had already been analysed by the security community.

Rather than relying on a single antivirus detection, I reviewed the overall detection ratio, malware classification, and available intelligence associated with the sample.

### Why I Looked There

VirusTotal aggregates results from multiple security vendors, making it one of the fastest ways to identify suspicious files.

### Skills Practiced

* Malware Identification
* Threat Intelligence
* IOC Validation

### What I Learned

Hash-based reputation lookups are often the first step in malware triage during incident response.

---

## Objective 2 – Review Malware Metadata

### My Approach

After identifying the malware family, I explored the sample metadata to understand the characteristics of the executable.

I reviewed information such as filenames, submission history, timestamps, and file properties to build context around the sample.

### Why I Looked There

Metadata provides valuable intelligence about malware evolution, distribution, and detection history.

### Skills Practiced

* Malware Profiling
* File Metadata Analysis
* Threat Hunting

### What I Learned

File metadata often reveals useful investigative context before analysing malware behaviour.

---

## Objective 3 – Analyse Malware Behaviour

### My Approach

Next, I reviewed the Behaviour section to understand what the malware attempted to do after execution.

Rather than focusing on individual events, I examined the complete execution chain, including file access, system interactions, and network activity.

### Why I Looked There

Behaviour analysis explains what the malware actually does after compromising a system.

### Skills Practiced

* Malware Behaviour Analysis
* Dynamic Analysis
* Threat Investigation

### What I Learned

Behaviour reports provide significantly more context than static detection alone.

---

## Objective 4 – Investigate Network Communication

### My Approach

I examined network-related artifacts generated during dynamic analysis to identify external infrastructure contacted by the malware.

I reviewed domains, IP addresses, ports, and communication patterns to understand how the malware interacted with attacker-controlled systems.

### Why I Looked There

Network indicators are critical for threat hunting, detection engineering, and incident response.

### Skills Practiced

* IOC Collection
* C2 Investigation
* Network Intelligence

### What I Learned

Malware often exposes valuable infrastructure indicators during sandbox execution.

---

## Objective 5 – Map MITRE ATT&CK Techniques

### My Approach

Using behavioural information, I reviewed the mapped MITRE ATT&CK techniques provided by VirusTotal.

Rather than memorising technique IDs, I focused on understanding why specific attacker behaviours were associated with each tactic.

### Why I Looked There

MITRE ATT&CK provides a standardized framework for describing adversary behaviour.

### Skills Practiced

* MITRE ATT&CK Analysis
* Threat Modelling
* Adversary Behaviour Analysis

### What I Learned

MITRE ATT&CK helps translate technical malware activity into standardized defensive knowledge.

---

## Objective 6 – Enrich Intelligence with MalwareBazaar

### My Approach

I searched the malware hash on MalwareBazaar to collect additional intelligence not available through VirusTotal.

This included community-submitted malware information, detection signatures, and related indicators.

### Why I Looked There

Different threat intelligence platforms provide complementary information that improves investigation quality.

### Skills Practiced

* Threat Intelligence Correlation
* IOC Enrichment
* Malware Research

### What I Learned

Cross-referencing multiple intelligence sources increases confidence in investigation findings.

---

## Objective 7 – Investigate ThreatFox Intelligence

### My Approach

Finally, I searched associated indicators in ThreatFox to identify related malware aliases and infrastructure.

I correlated these findings with previous observations to better understand the malware ecosystem.

### Why I Looked There

ThreatFox provides community-driven intelligence that links indicators to known malware campaigns.

### Skills Practiced

* IOC Correlation
* Malware Attribution
* Threat Intelligence Research

### What I Learned

Multiple intelligence sources often reveal relationships that would otherwise remain hidden.

---

# Intelligence Sources Used

| Platform      | Purpose                                |
| ------------- | -------------------------------------- |
| VirusTotal    | Malware reputation & behaviour         |
| MalwareBazaar | Sample intelligence & YARA information |
| ThreatFox     | IOC correlation & malware aliases      |
| WHOIS         | Infrastructure investigation           |
| ANY.RUN       | Dynamic malware analysis               |

---

# MITRE ATT&CK Focus

During this investigation I explored how the malware mapped to several MITRE ATT&CK tactics, including:

* Execution
* Persistence
* Privilege Escalation
* Defense Evasion
* Discovery
* Collection
* Impact

Understanding these tactics helped explain the malware's complete attack lifecycle rather than viewing it as a single malicious file.

---

# Skills Gained

* Threat Intelligence
* Malware Profiling
* VirusTotal Investigation
* MalwareBazaar Analysis
* ThreatFox Investigation
* IOC Collection
* IOC Enrichment
* Dynamic Malware Analysis
* MITRE ATT&CK Mapping
* Threat Hunting
* Malware Attribution
* OSINT Investigation

---

# Defensive Recommendations

* Continuously monitor file hashes against trusted threat intelligence feeds.
* Block known malicious domains and IP addresses at network boundaries.
* Integrate IOC feeds into SIEM and EDR platforms.
* Monitor unusual outbound network connections initiated by user processes.
* Use YARA rules to detect known malware families during endpoint scans.
* Regularly enrich alerts with external threat intelligence before triage.
* Develop detection rules based on attacker behavior rather than file hashes alone.

---

# Key Takeaways

* Threat intelligence platforms significantly reduce investigation time during malware analysis.
* A single malware hash can reveal extensive intelligence across multiple platforms.
* Behaviour analysis provides deeper insight than antivirus detections alone.
* Combining VirusTotal, MalwareBazaar, and ThreatFox produces richer investigation results.
* MITRE ATT&CK mapping improves understanding of adversary objectives and techniques.

---

# Reflection

This challenge strengthened my understanding of **Threat Intelligence workflows** by demonstrating how multiple public intelligence platforms can be used together to profile malware without executing it locally.

Instead of simply identifying a malware family, I learned how to investigate malware metadata, analyse behavioural reports, collect indicators of compromise, correlate findings across multiple intelligence sources, and map adversary behaviour using the MITRE ATT&CK framework.

The investigation improved my confidence in using **VirusTotal**, **MalwareBazaar**, **ThreatFox**, and other OSINT resources to enrich malware investigations and produce actionable intelligence for SOC operations.

The biggest lesson from this lab was that **effective threat intelligence comes from correlation**—combining information from multiple trusted sources provides a much clearer understanding of malware capabilities, infrastructure, and attacker behavior.

---

> **Note:** This repository intentionally excludes challenge answers to respect the CyberDefenders platform. Its purpose is to document the investigation methodology, threat intelligence techniques, and practical skills gained while completing the lab.
