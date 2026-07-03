# Yellow RAT

> **Cyber Threat Intelligence Investigation using VirusTotal, Hybrid Analysis & OSINT**

![Platform](https://img.shields.io/badge/Platform-CyberDefenders-blue)
![Category](https://img.shields.io/badge/Category-Cyber%20Threat%20Intelligence-green)
![Tool](https://img.shields.io/badge/Tool-VirusTotal%20%7C%20Hybrid%20Analysis-orange)

---

# Overview

This repository documents my investigation process while completing the **Yellow RAT** challenge on CyberDefenders.

Rather than publishing challenge answers, this write-up focuses on **how I investigated a malware sample using Cyber Threat Intelligence (CTI)**, **which intelligence sources provided valuable context**, and **what I learned** throughout the investigation. The objective is to demonstrate practical CTI techniques used to investigate malware without requiring reverse engineering.

---

# Scenario

During a routine security assessment, an organization detected abnormal network traffic originating from multiple employee workstations. Users also reported that web searches were being redirected to unfamiliar websites, indicating a possible malware infection.

Instead of receiving the malware sample itself, the investigation began with only its **SHA256 file hash**. My objective was to leverage public threat intelligence platforms to identify the malware, understand its capabilities, investigate its infrastructure, and gather intelligence that could support incident response efforts.

---

# Tools Used

* VirusTotal
* Hybrid Analysis
* Red Canary Intelligence
* Google Search (OSINT)
* SHA256 Hash Analysis
* MITRE ATT&CK Framework

---

# Investigation Workflow

```text
Obtain Malware Hash
        │
        ▼
Search Threat Intelligence Platforms
        │
        ▼
Identify Malware Family
        │
        ▼
Collect Static Intelligence
        │
        ▼
Investigate Malware Behaviour
        │
        ▼
Identify Infrastructure
        │
        ▼
Correlate Intelligence Sources
        │
        ▼
Build Threat Profile
```

Rather than attempting to reverse engineer the malware, I performed an intelligence-driven investigation by correlating findings across multiple trusted malware analysis platforms.

---

# Investigation Walkthrough

---

## Objective 1 – Identify the Malware Family

### My Approach

I began the investigation using the provided SHA256 hash as the primary indicator of compromise.

Instead of searching randomly, I queried malware intelligence platforms that maintain historical analysis reports. These reports provided contextual information about previously analysed malware samples.

### Why I Looked There

Threat intelligence platforms aggregate behavioural analysis, malware classifications, and community research, making them ideal starting points when only a file hash is available.

### Skills Practiced

* Hash Investigation
* Threat Intelligence
* Malware Identification
* OSINT

### What I Learned

A single file hash can provide extensive intelligence when correlated with trusted malware repositories.

---

## Objective 2 – Analyse Static Malware Information

### My Approach

After identifying the malware family, I reviewed the static metadata associated with the sample, including executable properties and embedded file information.

Rather than focusing on detections alone, I examined metadata that could help identify similar malware across other systems.

### Why I Looked There

Static analysis provides valuable indicators without requiring malware execution.

### Skills Practiced

* Static Malware Analysis
* File Metadata Investigation
* Threat Hunting

### What I Learned

Metadata can reveal valuable hunting indicators that assist in identifying additional infections.

---

## Objective 3 – Investigate Malware Timeline

### My Approach

I continued reviewing malware metadata to understand when the sample was compiled and when it first appeared in public intelligence databases.

This helped place the malware within a broader timeline of known malicious activity.

### Why I Looked There

Timeline information helps analysts determine malware age and estimate potential exposure windows.

### Skills Practiced

* Timeline Analysis
* Threat Intelligence Correlation
* Malware Research

### What I Learned

Compilation dates and public submission history provide important context during incident investigations.

---

## Objective 4 – Investigate Malware Behaviour

### My Approach

After gathering static intelligence, I pivoted to behavioural analysis reports to understand how the malware interacted with the operating system.

I reviewed behavioural summaries and technical reports instead of relying solely on antivirus detections.

### Why I Looked There

Behavioural analysis reveals what malware actually does once executed.

### Skills Practiced

* Behavioural Analysis
* Malware Investigation
* Threat Intelligence

### What I Learned

Behaviour-based indicators are often more valuable than signatures when detecting future variants.

---

## Objective 5 – Analyse Dropped Artifacts

### My Approach

I reviewed malware research reports to determine what additional files were created during execution.

Instead of relying on a single intelligence source, I compared findings across multiple reports to validate the observed behaviour.

### Why I Looked There

Dropped files frequently become valuable indicators during endpoint investigations.

### Skills Practiced

* Malware Behaviour Analysis
* Artifact Identification
* Intelligence Validation

### What I Learned

Correlating multiple intelligence sources improves confidence in investigative findings.

---

## Objective 6 – Investigate Network Infrastructure

### My Approach

Finally, I analysed the malware's observed network communications to understand how it interacted with external infrastructure.

I compared network indicators across multiple intelligence platforms to verify consistency before drawing conclusions.

### Why I Looked There

Understanding attacker infrastructure supports incident response by enabling defenders to identify, monitor, and block malicious communications.

### Skills Practiced

* Infrastructure Analysis
* Network Intelligence
* IOC Validation
* Threat Correlation

### What I Learned

Cross-validating indicators from multiple intelligence sources produces stronger and more reliable threat intelligence.

---

# Threat Intelligence Sources Used

| Source                  | Purpose                                 |
| ----------------------- | --------------------------------------- |
| VirusTotal              | Static malware intelligence             |
| Hybrid Analysis         | Sandbox behavioural analysis            |
| Red Canary Intelligence | Malware research and technical analysis |
| Google Search           | Intelligence pivoting                   |
| SHA256 Hash             | Primary indicator of compromise         |

---

# Artifacts Explored

| Artifact                 | Purpose                      |
| ------------------------ | ---------------------------- |
| SHA256 Hash              | Malware identification       |
| Executable Metadata      | Static analysis              |
| File Version Information | Sample profiling             |
| Compilation Information  | Timeline reconstruction      |
| Behaviour Reports        | Malware capability analysis  |
| Network Indicators       | Infrastructure investigation |
| File Artifacts           | Host-based indicators        |
| Intelligence Reports     | Threat context               |

---

# MITRE ATT&CK Mapping

| Attack Phase        | Technique                         |
| ------------------- | --------------------------------- |
| Initial Access      | Phishing                          |
| Execution           | User Execution                    |
| Persistence         | Registry Run Keys / Startup Items |
| Command and Control | Application Layer Protocol        |
| Collection          | Input Capture                     |
| Defense Evasion     | Obfuscated Files or Information   |

---

# Skills Gained

* Cyber Threat Intelligence (CTI)
* Malware Intelligence
* Static Malware Analysis
* Behavioural Malware Analysis
* Hash Investigation
* VirusTotal Analysis
* Hybrid Analysis
* IOC Collection
* Infrastructure Analysis
* Threat Hunting
* OSINT
* MITRE ATT&CK Mapping

---

# Defensive Recommendations

* Continuously monitor threat intelligence feeds for emerging malware.
* Block known malicious domains and IP addresses identified during investigations.
* Deploy endpoint protection capable of detecting behavioural indicators.
* Hunt for malware using file hashes and additional IOCs.
* Monitor unusual outbound network traffic from endpoints.
* Educate users to identify phishing attempts and suspicious downloads.
* Validate threat intelligence using multiple reputable sources before acting.

---

# Key Takeaways

* Threat intelligence investigations often begin with only a single indicator of compromise.
* Multiple intelligence platforms provide complementary information that strengthens investigations.
* Behavioural reports provide valuable insight beyond antivirus detections.
* Correlating intelligence from several trusted sources improves confidence in findings.
* Effective CTI investigations support faster incident response and threat hunting.

---

# Reflection

This challenge strengthened my understanding of Cyber Threat Intelligence by demonstrating how a complete malware investigation can be performed using publicly available intelligence sources.

Rather than reverse engineering the malware, I learned how to leverage VirusTotal, Hybrid Analysis, and industry research to identify malware characteristics, investigate behaviour, analyse infrastructure, and collect actionable indicators of compromise.

The investigation improved my confidence in using intelligence platforms, validating information across multiple sources, and documenting findings using a structured CTI investigation methodology.

The biggest lesson from this lab was that effective threat intelligence is built by correlating evidence from multiple trusted sources rather than relying on a single report or detection.

---

> **Note:** This repository intentionally excludes challenge answers to respect the CyberDefenders platform. Its purpose is to document the investigation methodology, threat intelligence techniques, and practical skills gained while completing the lab.
