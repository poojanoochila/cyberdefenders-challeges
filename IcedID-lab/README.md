# IcedID Lab

> **Cyber Threat Intelligence Investigation using VirusTotal, MITRE ATT&CK, Tria.ge & OSINT**

![Platform](https://img.shields.io/badge/Platform-CyberDefenders-blue)
![Category](https://img.shields.io/badge/Category-Threat%20Intelligence-green)
![Tool](https://img.shields.io/badge/Tool-VirusTotal%20%7C%20Tria.ge%20%7C%20MITRE-orange)

---

# Overview

This repository documents my investigation process while completing the **IcedID** challenge on CyberDefenders.

Rather than publishing challenge answers, this write-up focuses on **how I investigated a malware sample using Cyber Threat Intelligence (CTI)**, **how I correlated intelligence across multiple platforms**, and **what I learned** throughout the investigation. The objective is to demonstrate practical threat intelligence methodologies used to analyse malware campaigns, identify attacker infrastructure, and understand adversary behaviour without performing reverse engineering.

---

# Scenario

A security team identified an active phishing campaign distributing the **IcedID** banking malware. Instead of providing the malware sample itself, the investigation began with only a **SHA256 hash**.

My objective was to leverage public threat intelligence platforms to identify the malware, investigate its behaviour, analyse its infrastructure, associate it with known threat actors, and collect actionable indicators that could support threat hunting and incident response.

---

# Tools Used

* VirusTotal
* MITRE ATT&CK
* Tria.ge (Recorded Future)
* Malpedia
* ANY.RUN
* OSINT Research
* SHA256 Hash Analysis

---

# Investigation Workflow

```text
Receive Malware Hash
        │
        ▼
Search VirusTotal
        │
        ▼
Identify Malware Sample
        │
        ▼
Collect Static Intelligence
        │
        ▼
Investigate Behaviour
        │
        ▼
Analyse Infrastructure
        │
        ▼
Pivot to MITRE ATT&CK
        │
        ▼
Correlate Threat Intelligence
        │
        ▼
Build Threat Profile
```

Rather than attempting malware reverse engineering, I conducted an intelligence-driven investigation by correlating findings across multiple malware analysis platforms.

---

# Investigation Walkthrough

---

## Objective 1 – Identify the Malware Sample

### My Approach

I started the investigation using the provided SHA256 hash as the primary indicator of compromise.

The hash was searched across public malware intelligence repositories to determine whether the sample had been previously analysed and documented.

### Why I Looked There

Hash-based investigations are one of the fastest ways to identify known malware and obtain historical intelligence.

### Skills Practiced

* IOC Investigation
* Hash Analysis
* Threat Intelligence
* Malware Identification

### What I Learned

Even without possessing the malware itself, a file hash can reveal extensive intelligence when queried against reputable CTI platforms.

---

## Objective 2 – Investigate Static Malware Information

### My Approach

After identifying the malware sample, I reviewed its static metadata to understand its characteristics.

Rather than relying solely on detection results, I explored the file metadata, associated filenames, and sample properties that could support future threat hunting.

### Why I Looked There

Static indicators provide valuable hunting artifacts without executing malicious code.

### Skills Practiced

* Static Malware Analysis
* Metadata Investigation
* Threat Hunting

### What I Learned

Static analysis often provides enough information to identify related malware activity across multiple environments.

---

## Objective 3 – Analyse Malware Behaviour

### My Approach

Next, I examined behavioural analysis reports to understand how the malware interacted with external systems after execution.

I focused on observed network activity, contacted resources, and payload delivery mechanisms rather than individual antivirus detections.

### Why I Looked There

Behavioural analysis provides visibility into how malware actually operates inside a compromised environment.

### Skills Practiced

* Behavioural Malware Analysis
* Network Behaviour Investigation
* Threat Intelligence

### What I Learned

Behaviour-based indicators are often more resilient than signatures when tracking evolving malware families.

---

## Objective 4 – Investigate Infrastructure

### My Approach

After identifying outbound communications, I analysed the infrastructure contacted by the malware.

Instead of investigating only one indicator, I reviewed multiple related domains and infrastructure artifacts to understand how additional payloads were delivered.

### Why I Looked There

Infrastructure analysis helps defenders identify malicious hosting patterns and improve detection capabilities.

### Skills Practiced

* Infrastructure Analysis
* IOC Correlation
* Threat Intelligence

### What I Learned

Examining infrastructure rather than isolated indicators provides a broader understanding of malware campaigns.

---

## Objective 5 – Attribute Threat Activity

### My Approach

Using the identified malware family, I pivoted into MITRE ATT&CK and malware intelligence resources to investigate adversaries known to deploy this malware.

Rather than attributing based solely on one report, I correlated intelligence across multiple trusted sources.

### Why I Looked There

Threat actor attribution provides valuable context regarding attacker objectives, capabilities, and historical campaigns.

### Skills Practiced

* Threat Attribution
* MITRE ATT&CK Research
* Intelligence Correlation

### What I Learned

Threat intelligence becomes significantly more valuable when malware analysis is combined with adversary knowledge.

---

## Objective 6 – Investigate Malware Execution

### My Approach

Finally, I reviewed malware execution behaviour using sandbox reports from multiple intelligence platforms.

I compared execution-related observations across different analysis environments to understand how the malware retrieved additional payloads during execution.

### Why I Looked There

Execution behaviour provides valuable insight into how malware establishes itself and continues the infection chain.

### Skills Practiced

* Sandbox Analysis
* Malware Execution Analysis
* Behaviour Correlation

### What I Learned

Comparing multiple sandbox reports increases confidence in behavioural observations while reducing reliance on a single intelligence source.

---

# Threat Intelligence Sources Used

| Source         | Purpose                                 |
| -------------- | --------------------------------------- |
| VirusTotal     | Malware intelligence and IOC collection |
| Tria.ge        | Sandbox behavioural analysis            |
| MITRE ATT&CK   | Threat actor and technique research     |
| Malpedia       | Malware family intelligence             |
| ANY.RUN        | Behaviour validation                    |
| OSINT Research | Intelligence correlation                |

---

# Artifacts Explored

| Artifact                    | Purpose                      |
| --------------------------- | ---------------------------- |
| SHA256 Hash                 | Malware identification       |
| File Metadata               | Static analysis              |
| Associated Filenames        | Threat hunting               |
| Contacted URLs              | Infrastructure investigation |
| Contacted Domains           | IOC collection               |
| Sandbox Behaviour           | Execution analysis           |
| Threat Intelligence Reports | Campaign analysis            |
| MITRE ATT&CK References     | Adversary research           |

---

# MITRE ATT&CK Mapping

| Attack Phase        | Technique                       |
| ------------------- | ------------------------------- |
| Initial Access      | Phishing                        |
| Execution           | User Execution                  |
| Defense Evasion     | Obfuscated Files or Information |
| Command and Control | Application Layer Protocol      |
| Discovery           | System Information Discovery    |
| Collection          | Data from Local System          |

---

# Skills Gained

* Cyber Threat Intelligence (CTI)
* Malware Intelligence
* VirusTotal Investigation
* Tria.ge Analysis
* Malware Infrastructure Analysis
* IOC Collection
* Threat Actor Attribution
* MITRE ATT&CK Research
* OSINT
* Threat Hunting
* Behaviour Correlation
* Intelligence Validation

---

# Defensive Recommendations

* Continuously monitor known malware hashes and infrastructure.
* Enrich security alerts with external threat intelligence feeds.
* Hunt for malware using multiple indicators rather than hashes alone.
* Monitor outbound connections to newly observed infrastructure.
* Block malicious domains and URLs identified during investigations.
* Correlate sandbox reports from multiple vendors before making attribution decisions.
* Regularly review MITRE ATT&CK mappings to improve detection coverage.

---

# Key Takeaways

* A single SHA256 hash can initiate a complete threat intelligence investigation.
* Effective CTI relies on correlating information from multiple intelligence sources.
* Behavioural analysis complements static malware intelligence.
* Threat actor attribution provides valuable operational context.
* Infrastructure analysis strengthens both detection and threat hunting capabilities.

---

# Reflection

This challenge strengthened my understanding of Cyber Threat Intelligence by demonstrating how malware investigations can be conducted using publicly available intelligence platforms instead of reverse engineering.

Throughout the investigation, I learned how to pivot between VirusTotal, Tria.ge, MITRE ATT&CK, Malpedia, and other intelligence sources to build a comprehensive threat profile. Correlating findings across these platforms helped me better understand malware behaviour, infrastructure, and adversary activity.

The investigation improved my confidence in analysing malware using CTI methodologies, validating indicators across multiple sources, and documenting findings using a structured investigative workflow suitable for SOC operations.

The biggest lesson from this lab was that strong threat intelligence comes from **correlation**, not a single report. Each platform contributes a different perspective, and combining them produces a much more complete understanding of the threat.

---

> **Note:** This repository intentionally excludes challenge answers to respect the CyberDefenders platform. Its purpose is to document the investigation methodology, threat intelligence techniques, and practical skills gained while completing the lab.

