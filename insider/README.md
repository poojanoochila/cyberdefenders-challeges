# CyberDefenders – Insider

> **Linux Digital Forensics & Incident Response (DFIR) Investigation using FTK Imager**

![Platform](https://img.shields.io/badge/Platform-CyberDefenders-blue)
![Category](https://img.shields.io/badge/Category-Linux%20DFIR-green)
![Tool](https://img.shields.io/badge/Tool-FTK%20Imager-orange)

---

# Overview

This repository documents my investigation process while completing the **Insider** challenge on CyberDefenders.

Rather than publishing challenge answers, this write-up focuses on **how I approached the investigation**, **why I examined specific artifacts**, and **what I learned** during the analysis. The goal is to demonstrate practical DFIR methodology and investigative thinking similar to real-world SOC and Digital Forensics investigations.

---

# Scenario

A Linux forensic disk image belonging to an employee suspected of insider activity was provided for analysis. My objective was to examine the available evidence, reconstruct user activity, and answer the investigation objectives using forensic techniques while maintaining evidence integrity.

---

# Tools Used

- FTK Imager
- Linux File System Analysis
- Log Analysis
- File Hash Verification
- Digital Forensics Methodology

---

# Investigation Workflow

```
Evidence Acquisition
        │
        ▼
Explore Linux File System
        │
        ▼
Identify Important Artifacts
        │
        ▼
Analyse System Logs
        │
        ▼
Investigate User Activity
        │
        ▼
Correlate Evidence
        │
        ▼
Validate Findings
```

Instead of searching randomly, I followed a structured investigation methodology by analysing one artifact at a time and correlating evidence from multiple sources before reaching conclusions.

---

# Investigation Walkthrough

---

## Objective 1 – Identify the Operating System

### My Approach

The first step in any forensic investigation is understanding the operating system because it determines where important forensic artifacts are stored.

I began by exploring the **/var/log** directory and focused on kernel-related log files since they typically contain system boot information and operating system details.

### Why I Looked There

Kernel logs record information generated during system startup and provide valuable environmental details for investigators.

### Skills Practiced

- Linux filesystem navigation
- System log analysis
- Evidence discovery

### What I Learned

Understanding the operating system early makes the rest of the investigation significantly easier because artifact locations become predictable.

---

## Objective 2 – Verify Evidence Integrity

### My Approach

Rather than manually calculating hashes, I used FTK Imager's hashing functionality to verify evidence files.

This follows standard forensic practices by validating files without modifying the original evidence.

### Why I Looked There

Hash values are commonly used throughout DFIR investigations to ensure evidence remains unchanged during analysis.

### Skills Practiced

- Evidence preservation
- MD5 hashing
- Forensic validation

### What I Learned

Hash verification is one of the first steps in maintaining evidence integrity throughout an investigation.

---

## Objective 3 – Investigate Downloaded Files

### My Approach

To determine whether suspicious tools had been downloaded, I inspected common user directories such as Downloads.

Instead of searching the entire image, I prioritised locations where users typically save downloaded files.

### Why I Looked There

Downloaded archives and executables often reveal attacker tooling or preparation activities.

### Skills Practiced

- User artifact analysis
- Directory investigation
- Suspicious file identification

### What I Learned

Simple user directories can contain valuable evidence and should never be overlooked during investigations.

---

## Objective 4 – Investigate User-Created Files

### My Approach

Instead of browsing every folder manually, I examined shell history to identify commands executed by the user.

Command history often reveals file creation, deletion, movement, and execution.

### Why I Looked There

User command history provides direct insight into user behaviour and frequently reduces investigation time.

### Skills Practiced

- Bash history analysis
- User behaviour investigation
- Timeline reconstruction

### What I Learned

Shell history is one of the most valuable Linux forensic artifacts because it records actual user interactions with the system.

---

## Objective 5 – Identify Executed Programs

### My Approach

While reviewing shell history, I paid attention to commands executed alongside filenames and utilities.

Rather than guessing which application interacted with a file, I relied on command history as supporting evidence.

### Why I Looked There

Executed commands provide context about how files were used instead of simply showing that they existed.

### Skills Practiced

- Process investigation
- Command analysis
- Artifact correlation

### What I Learned

Understanding user intent requires analysing both files and the commands that interacted with them.

---

## Objective 6 – Analyse User Documents

### My Approach

I examined common user directories including Desktop and Documents because they frequently contain notes, scripts, checklists, and other user-generated artifacts.

### Why I Looked There

Personal files often provide context that system logs alone cannot.

### Skills Practiced

- User artifact discovery
- Manual evidence collection
- Context analysis

### What I Learned

User-generated documents can provide valuable context when reconstructing attacker behaviour.

---

## Objective 7 – Analyse Service Logs

### My Approach

To determine application activity, I inspected relevant service logs instead of relying on assumptions.

I reviewed available logs to verify whether services had actually been used during the investigation period.

### Why I Looked There

Service logs provide objective evidence about application execution.

### Skills Practiced

- Log analysis
- Service investigation
- Evidence validation

### What I Learned

The absence of log entries can be just as valuable as the presence of activity.

---

## Objective 8 – Correlate Multiple Artifacts

### My Approach

Rather than relying on a single piece of evidence, I correlated information from shell history, user files, screenshots, and system artifacts to understand overall activity.

### Why I Looked There

Real-world investigations depend on evidence correlation rather than isolated findings.

### Skills Practiced

- Evidence correlation
- Timeline analysis
- Investigation methodology

### What I Learned

Multiple independent artifacts create stronger forensic conclusions than any single source.

---

## Objective 9 – Analyse Scripts

### My Approach

I reviewed scripts stored inside user directories to understand their purpose and identify behavioural clues.

Instead of executing scripts, I inspected their contents statically.

### Why I Looked There

Scripts often reveal automation, testing activity, or attacker intent.

### Skills Practiced

- Script analysis
- Static inspection
- Behaviour analysis

### What I Learned

Even simple scripts can provide important contextual evidence during investigations.

---

## Objective 10 – Authentication Investigation

### My Approach

Authentication logs were reviewed to understand privilege escalation events and user authentication activity.

I searched for authentication-related entries matching the investigation objectives.

### Why I Looked There

Authentication logs provide reliable evidence of login activity and privilege changes.

### Skills Practiced

- Authentication log analysis
- Privilege escalation investigation
- Event filtering

### What I Learned

Authentication logs are among the most valuable artifacts when investigating user activity on Linux systems.

---

## Objective 11 – Reconstruct User Activity

### My Approach

The final step was correlating shell history, log files, and filesystem artifacts to understand the user's working environment and sequence of actions.

### Why I Looked There

Timeline reconstruction helps transform isolated findings into a complete investigation story.

### Skills Practiced

- Timeline reconstruction
- Evidence correlation
- Digital investigation methodology

### What I Learned

Successful investigations rely on connecting multiple artifacts rather than analysing them independently.

---

# Linux Artifacts Explored

| Artifact | Purpose |
|----------|---------|
| `/var/log/` | System and application logs |
| `.bash_history` | User command history |
| User Directories | Desktop, Documents, Downloads, Pictures |
| Authentication Logs | Login and privilege events |
| Apache Logs | Service activity |
| File Hashes | Evidence integrity verification |

---

# Skills Gained

- Linux Digital Forensics
- Incident Response
- FTK Imager
- Linux Log Analysis
- Bash History Analysis
- Authentication Analysis
- File Integrity Verification
- Timeline Reconstruction
- Evidence Correlation
- Critical Thinking
- Digital Investigation Methodology

---

# Key Takeaways

- Always begin by understanding the operating environment.
- Follow a structured methodology instead of searching randomly.
- Validate findings using multiple forensic artifacts.
- Preserve evidence integrity throughout the investigation.
- User activity can often be reconstructed through command history and system logs.
- Correlating evidence produces stronger and more reliable conclusions.

---

# Reflection

This challenge strengthened my understanding of Linux Digital Forensics by showing how multiple artifacts work together to reconstruct user activity.

Instead of focusing on finding answers quickly, I concentrated on understanding **why** particular artifacts were important and **how** they contributed to the investigation. I became more confident navigating Linux forensic images, analysing logs, interpreting shell history, and correlating evidence to build an accurate timeline.

The experience reinforced an important DFIR principle:

> **Good investigators don't search for answers—they follow the evidence.**

---

> **Note:** This repository intentionally excludes challenge answers to respect the CyberDefenders platform and instead focuses on the investigation methodology, learning outcomes, and practical DFIR techniques gained while completing the lab.
