# PsExec Hunt

> **Network Forensics Investigation using Wireshark**

![Platform](https://img.shields.io/badge/Platform-CyberDefenders-blue)
![Category](https://img.shields.io/badge/Category-Network%20Forensics-green)
![Tool](https://img.shields.io/badge/Tool-Wireshark-orange)

---

# Overview

This repository documents my investigation process while completing the **PsExec Hunt** challenge on CyberDefenders.

Rather than publishing challenge answers, this write-up focuses on **how I investigated the network traffic**, **which artifacts helped reconstruct the attack**, and **what I learned** throughout the investigation. The objective is to demonstrate practical network forensic techniques commonly used by SOC analysts when investigating lateral movement within enterprise environments.

---

# Scenario

An Intrusion Detection System (IDS) generated an alert indicating suspicious lateral movement involving **PsExec**, a legitimate Windows administration tool frequently abused by attackers.

A packet capture (PCAP) was provided for analysis. My objective was to determine how the attacker moved through the network, identify compromised systems, reconstruct the attack timeline, and understand the techniques used during the intrusion.

---

# Tools Used

* Wireshark
* SMB Protocol Analysis
* NTLM Authentication Analysis
* TCP Stream Analysis
* Windows Networking Knowledge
* MITRE ATT&CK Framework

---

# Investigation Workflow

```text
Load PCAP File
        │
        ▼
Review Network Conversations
        │
        ▼
Identify Initial Compromise
        │
        ▼
Analyse SMB Authentication
        │
        ▼
Investigate PsExec Activity
        │
        ▼
Track Lateral Movement
        │
        ▼
Correlate Network Evidence
        │
        ▼
Reconstruct Attack Timeline
```

Instead of searching directly for challenge answers, I followed the attacker's activity chronologically and validated each finding using multiple pieces of network evidence.

---

# Investigation Walkthrough

---

## Objective 1 – Identify the Initial Compromised System

### My Approach

I began by analysing the overall network conversations to identify systems communicating abnormally. I reviewed traffic statistics, filtered suspicious SMB communications, and determined which host appeared to initiate the attack.

### Why I Looked There

Network conversations provide a high-level overview of communication patterns and quickly reveal hosts involved in suspicious activity.

### Skills Practiced

* Packet Analysis
* Conversation Analysis
* Traffic Filtering

### What I Learned

Understanding who initiated communication provides the foundation for reconstructing an attack timeline.

---

## Objective 2 – Investigate the First Lateral Movement

### My Approach

After identifying the suspected attacker, I narrowed the investigation to SMB traffic between the communicating systems. I reconstructed authentication exchanges and inspected protocol details to identify the first destination host.

### Why I Looked There

SMB authentication often reveals workstation information and helps determine where attackers first moved after compromising an endpoint.

### Skills Practiced

* SMB Analysis
* NTLM Investigation
* TCP Stream Reconstruction

### What I Learned

Authentication protocols often contain valuable contextual information beyond simple login events.

---

## Objective 3 – Analyse Authentication Activity

### My Approach

I examined NTLM authentication messages exchanged during SMB session establishment to understand how access was obtained.

Instead of focusing only on successful sessions, I analysed authentication packets to identify user-related information contained within the protocol.

### Why I Looked There

Authentication artifacts provide insight into the identities used during lateral movement.

### Skills Practiced

* NTLM Authentication Analysis
* SMB Session Investigation
* Identity Analysis

### What I Learned

Protocol-level authentication data can reveal important investigation details even without endpoint logs.

---

## Objective 4 – Investigate Remote Service Deployment

### My Approach

Once authentication had been established, I reviewed SMB Create and Write operations to understand what files were transferred between systems.

Rather than inspecting every SMB packet individually, I focused on file creation activity associated with remote execution.

### Why I Looked There

Remote administration tools commonly transfer executables before executing commands on the target system.

### Skills Practiced

* SMB File Analysis
* Remote Execution Investigation
* Windows Administrative Activity

### What I Learned

File creation events often indicate the transition from authentication to active remote execution.

---

## Objective 5 – Analyse Administrative Share Usage

### My Approach

After identifying evidence of file transfer, I examined the SMB paths used during the upload process to understand how the attacker deployed remote services.

### Why I Looked There

Administrative shares are frequently abused during lateral movement and provide valuable indicators of attacker behaviour.

### Skills Practiced

* Windows Administrative Shares
* SMB Path Analysis
* Lateral Movement Investigation

### What I Learned

Understanding default Windows administrative shares helps investigators recognize malicious remote administration activity.

---

## Objective 6 – Investigate Inter-System Communication

### My Approach

Following the service deployment, I analysed SMB communication channels established between the two systems to understand how commands were exchanged.

I reconstructed the communication rather than relying on isolated packets.

### Why I Looked There

Communication channels reveal how attackers maintain interaction with compromised systems during remote execution.

### Skills Practiced

* SMB Communication Analysis
* Named Pipe Investigation
* Windows Networking

### What I Learned

Legitimate Windows communication mechanisms are commonly abused during post-exploitation activities.

---

## Objective 7 – Track Additional Lateral Movement

### My Approach

Finally, I expanded the investigation to identify communication with additional hosts across the network.

I reviewed name resolution traffic alongside SMB activity to determine whether the attacker attempted to move further within the environment.

### Why I Looked There

Attackers rarely stop after compromising a single endpoint. Identifying additional movement helps determine the overall impact of the incident.

### Skills Practiced

* Lateral Movement Analysis
* LLMNR Investigation
* Network Enumeration Detection
* Evidence Correlation

### What I Learned

Combining multiple protocols provides a more complete understanding of attacker behaviour than analysing SMB traffic alone.

---

# Network Artifacts Explored

| Artifact            | Purpose                              |
| ------------------- | ------------------------------------ |
| IPv4 Conversations  | Identify communicating hosts         |
| SMB Sessions        | Investigate file sharing activity    |
| SMB Create Requests | Detect remote file deployment        |
| SMB Write Requests  | Analyse transferred files            |
| NTLM Authentication | Investigate user authentication      |
| TCP Streams         | Reconstruct complete communication   |
| LLMNR Traffic       | Identify host discovery activity     |
| Named Pipes         | Analyse remote service communication |

---

# MITRE ATT&CK Mapping

| Attack Phase      | Technique                    |
| ----------------- | ---------------------------- |
| Discovery         | Network Service Discovery    |
| Credential Access | Valid Accounts               |
| Execution         | Windows Service Execution    |
| Lateral Movement  | Remote Services (SMB/PsExec) |
| Defense Evasion   | Living Off the Land          |

---

# Skills Gained

* Network Forensics
* Wireshark Analysis
* SMB Protocol Investigation
* NTLM Authentication Analysis
* Windows Network Internals
* Lateral Movement Detection
* PsExec Investigation
* TCP Stream Reconstruction
* Threat Hunting
* Evidence Correlation
* MITRE ATT&CK Mapping
* Incident Response Methodology

---

# Defensive Recommendations

* Monitor PsExec usage across the environment.
* Restrict administrative shares to authorized users only.
* Enable logging for remote service creation events.
* Detect abnormal SMB authentication between endpoints.
* Monitor lateral movement using endpoint and network telemetry.
* Restrict privileged account usage through least-privilege principles.
* Enable alerting for unusual administrative tool execution.

---

# Key Takeaways

* SMB traffic provides valuable evidence when investigating lateral movement.
* Authentication artifacts help reconstruct attacker activity across multiple hosts.
* Administrative shares are common targets during Windows-based intrusions.
* Combining SMB, NTLM, and name resolution traffic produces a clearer investigation timeline.
* A structured methodology enables investigators to reconstruct complex attacks from network evidence alone.

---

# Reflection

This challenge strengthened my understanding of Windows network forensics by demonstrating how attacker lateral movement can be reconstructed entirely from packet captures.

Rather than focusing on challenge answers, I concentrated on understanding how attackers authenticate, transfer files, establish remote execution, and pivot between systems using legitimate Windows administration protocols.

The investigation improved my confidence in analysing SMB traffic, interpreting NTLM authentication exchanges, reconstructing TCP streams, and documenting findings using a structured SOC investigation methodology.

The biggest lesson from this lab was that legitimate administrative tools can become powerful attacker utilities, making behavioural analysis essential for distinguishing normal administration from malicious activity.

---

> **Note:** This repository intentionally excludes challenge answers to respect the CyberDefenders platform. Its purpose is to document the investigation methodology, forensic reasoning, and practical skills gained while completing the lab.
