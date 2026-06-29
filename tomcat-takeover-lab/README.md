# CyberDefenders – Tomcat Takeover

> **Network Forensics Investigation using Wireshark**

![Platform](https://img.shields.io/badge/Platform-CyberDefenders-blue)
![Category](https://img.shields.io/badge/Category-Network%20Forensics-green)
![Tool](https://img.shields.io/badge/Tool-Wireshark-orange)

---

# Overview

This repository documents my investigation process while completing the **Tomcat Takeover** challenge on CyberDefenders.

Rather than publishing challenge answers, this write-up focuses on **how I approached the investigation**, **why I examined specific network artifacts**, and **what I learned** throughout the incident analysis. The objective is to demonstrate practical network forensic methodology similar to investigations performed by SOC analysts during real security incidents.

---

# Scenario

The SOC team detected suspicious activity targeting an internal Apache Tomcat web server. A packet capture (PCAP) containing the network traffic was provided for analysis.

My objective was to reconstruct the attack timeline, identify the attacker's techniques, and investigate how the compromise occurred by analysing the captured network traffic.

---

# Tools Used

* Wireshark
* HTTP Stream Analysis
* TCP Stream Analysis
* Base64 Decoding
* OSINT (IP Geolocation)
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
Identify Suspicious Host
        │
        ▼
Analyse HTTP Traffic
        │
        ▼
Investigate Authentication
        │
        ▼
Review File Upload Activity
        │
        ▼
Analyse Post-Exploitation Traffic
        │
        ▼
Correlate Evidence
```

Instead of searching directly for challenge answers, I followed the attack lifecycle by analysing each stage of the intrusion and validating every finding through packet evidence.

---

# Investigation Walkthrough

---

## Objective 1 – Detect Reconnaissance Activity

### My Approach

I began by reviewing the captured network conversations to identify hosts generating unusual traffic patterns. Systems making repeated connections across multiple ports often indicate reconnaissance or scanning behaviour.

Rather than focusing on individual packets, I analysed the overall communication flow to determine which host initiated the activity.

### Why I Looked There

Network conversations provide an excellent starting point because they quickly reveal abnormal communication patterns and identify potential attacker systems.

### Skills Practiced

* Wireshark navigation
* Packet filtering
* Network reconnaissance detection

### What I Learned

Before investigating an attack, understanding the communication pattern helps establish where the investigation should begin.

---

## Objective 2 – Investigate the Suspicious Host

### My Approach

After identifying the suspicious source, I enriched the investigation using publicly available threat intelligence and IP geolocation resources.

This helped provide additional context about the external host involved in the incident.

### Why I Looked There

Threat intelligence adds valuable context that complements packet analysis during an investigation.

### Skills Practiced

* Threat Intelligence
* OSINT
* IP Investigation

### What I Learned

External intelligence should support an investigation but never replace evidence found inside the packet capture.

---

## Objective 3 – Identify the Target Service

### My Approach

To determine which service was targeted, I examined successful TCP communications and reviewed application-layer protocols associated with those sessions.

I focused on services that consistently responded to client requests rather than assuming which application had been compromised.

### Why I Looked There

Successful connections usually indicate active services and provide a starting point for analysing attacker interaction.

### Skills Practiced

* TCP Analysis
* Protocol Identification
* Service Enumeration

### What I Learned

Understanding TCP communication makes it easier to distinguish successful connections from reconnaissance attempts.

---

## Objective 4 – Analyse Enumeration Activity

### My Approach

Once the attacker reached the web application, I analysed HTTP requests to understand how the server was being explored.

I reviewed request headers, URLs, and complete HTTP conversations to identify evidence of directory enumeration.

### Why I Looked There

Enumeration tools often generate distinctive HTTP request patterns that can be recognised through traffic analysis.

### Skills Practiced

* HTTP Analysis
* Web Enumeration
* HTTP Stream Reconstruction

### What I Learned

Following complete HTTP conversations provides much better context than analysing packets individually.

---

## Objective 5 – Investigate Administrative Access

### My Approach

After identifying enumeration activity, I continued following the HTTP sessions to determine how the attacker interacted with administrative resources.

Rather than searching randomly, I reconstructed the complete communication to understand the attack progression.

### Why I Looked There

Administrative interfaces are common targets during web server compromises and often represent the next stage after enumeration.

### Skills Practiced

* Web Application Investigation
* HTTP Stream Analysis
* Evidence Correlation

### What I Learned

Understanding the sequence of HTTP requests helps reconstruct attacker behaviour more accurately.

---

## Objective 6 – Analyse Authentication Activity

### My Approach

I reviewed authentication-related HTTP requests and examined the Authorization headers exchanged between the client and server.

When encoded information appeared within the requests, I decoded it to understand how authentication was performed.

### Why I Looked There

Authentication traffic frequently contains valuable evidence explaining how attackers successfully access systems.

### Skills Practiced

* Authentication Analysis
* Base64 Decoding
* HTTP Header Investigation

### What I Learned

Many authentication mechanisms rely on standard encoding rather than encryption, making it important to understand common encoding formats during investigations.

---

## Objective 7 – Investigate File Upload Activity

### My Approach

Following successful authentication, I examined HTTP POST requests to understand what content was transferred to the server.

Instead of relying on filenames alone, I analysed both the request and the server response to understand the upload process.

### Why I Looked There

POST requests often represent the transition between initial access and exploitation.

### Skills Practiced

* HTTP POST Analysis
* Web Shell Investigation
* Traffic Correlation

### What I Learned

Reviewing server responses alongside upload requests provides confidence that an action was completed successfully.

---

## Objective 8 – Investigate Post-Exploitation Activity

### My Approach

To understand how the attacker maintained access, I analysed the TCP streams established after exploitation.

Following complete streams allowed me to reconstruct attacker activity without relying on assumptions.

### Why I Looked There

Post-exploitation traffic often contains the strongest evidence regarding persistence and command execution.

### Skills Practiced

* TCP Stream Analysis
* Reverse Shell Investigation
* Post-Exploitation Analysis

### What I Learned

Following the attack beyond initial compromise provides a complete understanding of the attack lifecycle.

---

# Network Artifacts Explored

| Artifact              | Purpose                                  |
| --------------------- | ---------------------------------------- |
| IPv4 Conversations    | Identify communicating hosts             |
| TCP Conversations     | Analyse active sessions                  |
| HTTP Requests         | Investigate attacker activity            |
| HTTP Streams          | Reconstruct complete web sessions        |
| TCP Streams           | Analyse post-exploitation communication  |
| Authorization Headers | Investigate authentication               |
| HTTP POST Requests    | Review uploads and user actions          |
| Packet Statistics     | Identify abnormal communication patterns |

---

# MITRE ATT&CK Mapping

| Attack Phase      | Technique                         |
| ----------------- | --------------------------------- |
| Reconnaissance    | Active Scanning                   |
| Initial Access    | Exploit Public-Facing Application |
| Credential Access | Valid Accounts                    |
| Persistence       | Server Software Component         |
| Persistence       | Scheduled Task / Cron             |

---

# Skills Gained

* Network Forensics
* Wireshark Analysis
* HTTP Protocol Analysis
* TCP Stream Reconstruction
* Web Application Investigation
* Authentication Analysis
* Incident Response Methodology
* Threat Intelligence
* MITRE ATT&CK Mapping
* Evidence Correlation
* Critical Thinking

---

# Defensive Recommendations

* Restrict administrative interfaces to trusted networks.
* Disable default or weak credentials.
* Monitor for unusual scanning behaviour.
* Log and review authentication attempts regularly.
* Inspect file upload activity on web servers.
* Detect abnormal outbound connections that may indicate reverse shells.
* Continuously monitor network traffic for signs of post-exploitation activity.

---

# Key Takeaways

* Begin investigations by understanding overall network communication before analysing individual packets.
* Reconstructing complete HTTP and TCP streams provides significantly more context than isolated packets.
* Authentication traffic should always be examined during web application investigations.
* Correlating multiple network artifacts leads to stronger investigative conclusions.
* A structured methodology improves both investigation speed and accuracy.

---

# Reflection

This challenge strengthened my understanding of network forensics by demonstrating how an attacker’s actions can be reconstructed entirely from packet captures.

Instead of focusing on discovering challenge answers, I concentrated on understanding each phase of the attack—from reconnaissance and enumeration to authentication, exploitation, and post-exploitation. The investigation improved my confidence in analysing HTTP traffic, reconstructing communication streams, correlating evidence, and documenting findings using a structured incident response methodology.

The biggest lesson from this investigation was that successful analysts don't search for answers—they follow the evidence and allow the network traffic to tell the story.

---

> **Note:** This repository intentionally excludes challenge answers to respect the CyberDefenders platform. Its purpose is to document the investigation methodology, forensic reasoning, and practical skills developed while completing the lab.
