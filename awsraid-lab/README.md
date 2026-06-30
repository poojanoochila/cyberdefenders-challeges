# CyberDefenders – AWSRaid

> **Cloud Forensics Investigation using AWS CloudTrail & Splunk**

![Platform](https://img.shields.io/badge/Platform-CyberDefenders-blue)
![Category](https://img.shields.io/badge/Category-Cloud%20Forensics-green)
![Tool](https://img.shields.io/badge/Tool-Splunk-orange)

---

# Overvie


This repository documents my investigation process while completing the **AWSRaid** challenge on CyberDefenders.

Instead of publishing challenge answers, this write-up focuses on **how I investigated the incident**, **which CloudTrail artifacts were analysed**, and **what I learned** during the investigation. The objective is to demonstrate practical cloud forensic techniques and incident response methodologies commonly used by SOC analysts and cloud security engineers.

---

# Scenario

An organization reported unauthorized access to its AWS environment after suspicious activity was detected involving IAM accounts and Amazon S3 resources.

A collection of **AWS CloudTrail logs** was indexed into **Splunk**, and my objective was to reconstruct the attack timeline, determine the attacker's actions, identify persistence mechanisms, and understand the overall impact of the compromise.

---

# Tools Used

* Splunk
* AWS CloudTrail Logs
* Splunk Processing Language (SPL)
* AWS IAM Knowledge
* Amazon S3 Security Concepts
* MITRE ATT&CK Framework

---

# Investigation Workflow

```text
CloudTrail Log Collection
          │
          ▼
Authentication Investigation
          │
          ▼
User Activity Analysis
          │
          ▼
S3 Access Investigation
          │
          ▼
Configuration Change Detection
          │
          ▼
IAM Persistence Analysis
          │
          ▼
Evidence Correlation
          │
          ▼
Attack Timeline Reconstruction
```

Rather than searching directly for challenge answers, I followed the attacker's progression from initial access through persistence by correlating CloudTrail events inside Splunk.

---

# Investigation Walkthrough

---

## Objective 1 – Investigate Initial Access

### My Approach

I began by analysing AWS Management Console sign-in events to identify abnormal authentication behaviour. Instead of looking only for successful logins, I reviewed failed authentication attempts followed by successful access originating from the same source.

### Why I Looked There

Authentication events are usually the first indicator of account compromise and provide valuable information about attacker entry points.

### Skills Practiced

* CloudTrail Analysis
* Authentication Investigation
* Splunk Searching
* Incident Triage

### What I Learned

A successful login immediately following multiple failed attempts may indicate brute-force activity or credential guessing and should always be investigated.

---

## Objective 2 – Analyse User Activity

### My Approach

After identifying the compromised account, I filtered CloudTrail events associated with that identity and reconstructed the user's actions in chronological order.

Rather than reviewing every log entry manually, I narrowed the investigation using event types and timestamps.

### Why I Looked There

Following activity performed by a compromised identity helps reconstruct the attacker's objectives and movement within the environment.

### Skills Practiced

* Timeline Analysis
* Splunk Filtering
* Event Correlation

### What I Learned

Building an event timeline makes it easier to understand attacker behaviour and reduces unnecessary investigation effort.

---

## Objective 3 – Investigate Amazon S3 Access

### My Approach

I examined CloudTrail events related to Amazon S3 to determine how storage resources were accessed after the compromise.

I reviewed bucket operations and associated resources to understand what information the attacker attempted to discover.

### Why I Looked There

Sensitive information is frequently stored inside S3 buckets, making them common targets during cloud compromises.

### Skills Practiced

* AWS CloudTrail Analysis
* Amazon S3 Investigation
* Resource Identification

### What I Learned

CloudTrail provides detailed visibility into interactions with cloud resources, allowing investigators to reconstruct attacker activity without directly accessing the affected infrastructure.

---

## Objective 4 – Investigate Configuration Changes

### My Approach

After identifying access to cloud storage, I investigated configuration-related API calls to determine whether security controls had been modified.

I specifically looked for administrative actions affecting resource permissions rather than only data access events.

### Why I Looked There

Changes to security configurations often indicate attacker attempts to weaken protections or prepare for data exposure.

### Skills Practiced

* Cloud Configuration Analysis
* Security Control Monitoring
* Cloud Forensics

### What I Learned

Monitoring configuration changes is just as important as monitoring authentication events because attackers often modify security settings after gaining access.

---

## Objective 5 – Investigate Persistence

### My Approach

To determine whether persistence had been established, I searched for IAM management events related to account administration.

Rather than focusing only on authentication logs, I reviewed identity management actions that could create long-term access.

### Why I Looked There

Creating additional identities is a common persistence technique used in compromised cloud environments.

### Skills Practiced

* IAM Investigation
* Persistence Detection
* AWS Identity Analysis

### What I Learned

Attackers frequently create new identities instead of relying on compromised credentials, making IAM monitoring essential during incident response.

---

## Objective 6 – Investigate Privilege Escalation

### My Approach

Once new identity management activity was identified, I analysed subsequent IAM events to understand how permissions changed over time.

I correlated related API calls to determine whether additional privileges had been granted after account creation.

### Why I Looked There

Privilege changes often indicate an attempt to establish stronger or more persistent access within the environment.

### Skills Practiced

* Privilege Escalation Investigation
* IAM Analysis
* Event Correlation

### What I Learned

CloudTrail records permission changes with enough detail to reconstruct privilege escalation without requiring direct access to the AWS account.

---

# Cloud Artifacts Explored

| Artifact                | Purpose                                |
| ----------------------- | -------------------------------------- |
| AWS CloudTrail Logs     | Record AWS API activity                |
| Console Sign-In Events  | Authentication monitoring              |
| IAM Events              | Identity and access management changes |
| Amazon S3 Events        | Storage access investigation           |
| Configuration Changes   | Security control modifications         |
| User Management Events  | Persistence detection                  |
| Group Membership Events | Privilege escalation analysis          |

---

# Splunk Techniques Used

* Event Filtering
* Time-based Analysis
* Field Extraction
* Event Correlation
* Statistical Aggregation
* Timeline Reconstruction
* CloudTrail Log Investigation

---

# MITRE ATT&CK Mapping

| Attack Phase         | Technique                      |
| -------------------- | ------------------------------ |
| Initial Access       | Brute Force                    |
| Credential Access    | Valid Accounts                 |
| Discovery            | Cloud Service Discovery        |
| Persistence          | Create Account                 |
| Privilege Escalation | Account Manipulation           |
| Defense Evasion      | Modify Cloud Security Controls |

---

# Skills Gained

* Cloud Forensics
* AWS CloudTrail Analysis
* Splunk Investigation
* SPL Querying
* IAM Security
* Amazon S3 Investigation
* Authentication Analysis
* Timeline Reconstruction
* Threat Hunting
* Cloud Incident Response
* Evidence Correlation
* MITRE ATT&CK Mapping

---

# Defensive Recommendations

* Enable MFA for privileged IAM users.
* Monitor repeated authentication failures.
* Generate alerts for IAM user creation events.
* Continuously monitor IAM privilege modifications.
* Detect changes to Amazon S3 security configurations.
* Apply the principle of least privilege across IAM roles and users.
* Continuously review CloudTrail logs for abnormal administrative activity.

---

# Key Takeaways

* CloudTrail provides comprehensive visibility into AWS administrative activity.
* Authentication events should always be correlated with subsequent API calls.
* IAM modifications are high-value indicators during cloud investigations.
* Configuration changes may reveal attacker objectives beyond initial compromise.
* Structured log analysis allows investigators to reconstruct complex cloud attacks efficiently.

---

# Reflection

This challenge significantly improved my understanding of cloud incident response and AWS forensic investigations.

Instead of focusing solely on authentication events, I learned how to correlate CloudTrail logs to reconstruct an entire attack lifecycle—from initial access and resource discovery to configuration changes, persistence, and privilege escalation.

The investigation strengthened my confidence in using Splunk to analyse cloud logs, build investigation timelines, and identify attacker behaviour using evidence rather than assumptions.

The biggest takeaway from this lab was that effective cloud investigations rely on understanding the relationships between authentication events, API activity, IAM modifications, and resource configuration changes rather than analysing each event independently.

---

> **Note:** This repository intentionally excludes challenge answers to respect the CyberDefenders platform. Its purpose is to document the investigation methodology, cloud forensic techniques, and practical skills gained while completing the lab.
