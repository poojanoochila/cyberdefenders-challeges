# GrabThePhisher

> **Threat Intelligence Investigation of a Cryptocurrency Phishing Kit**

![Platform](https://img.shields.io/badge/Platform-CyberDefenders-blue)
![Category](https://img.shields.io/badge/Category-Threat%20Intelligence-green)
![Tool](https://img.shields.io/badge/Tool-Source%20Code%20Analysis-orange)

---

# Overview

This repository documents my investigation process while completing the **GrabThePhisher** challenge on CyberDefenders.

Rather than publishing challenge answers, this write-up focuses on **how I analysed the phishing kit**, **which artifacts revealed the attacker's infrastructure**, and **what I learned** throughout the investigation. The objective is to demonstrate practical threat intelligence techniques used to investigate phishing campaigns, analyse malicious source code, and attribute attacker infrastructure.

---

# Scenario

A compromised server was hosting a phishing kit impersonating a legitimate cryptocurrency exchange website. The phishing kit was distributed as an open directory containing the complete source code used to steal cryptocurrency wallet recovery phrases.

As a SOC Analyst, my objective was to analyse the phishing kit, understand how it operated, identify its infrastructure, investigate its data exfiltration methods, and gather threat intelligence about the actor behind the campaign.

---

# Tools Used

* Source Code Analysis
* PHP Code Review
* HTML Analysis
* Telegram Bot API Documentation
* Google Search (OSINT)
* cURL
* jq
* MITRE ATT&CK Framework

---

# Investigation Workflow

```text
Obtain Phishing Kit
        │
        ▼
Review File Structure
        │
        ▼
Identify Credential Collection Logic
        │
        ▼
Analyse Source Code
        │
        ▼
Investigate Data Exfiltration
        │
        ▼
Pivot Using OSINT
        │
        ▼
Analyse Attacker Infrastructure
        │
        ▼
Correlate Threat Intelligence
```

Instead of searching directly for challenge answers, I investigated the phishing kit as if analysing malware during a real-world phishing incident, following the attack chain from credential harvesting to attacker infrastructure.

---

# Investigation Walkthrough

---

## Objective 1 – Identify the Targeted Wallet

### My Approach

I began by extracting the phishing kit and reviewing its directory structure to understand how the fake website was organised.

After identifying the landing page, I analysed the linked resources and examined individual wallet-related components to determine which wallet contained the credential harvesting functionality.

### Why I Looked There

The website structure often reveals which components perform the actual credential collection instead of simply displaying the user interface.

### Skills Practiced

* HTML Analysis
* Directory Structure Analysis
* Phishing Kit Investigation

### What I Learned

Separating presentation files from backend processing files is essential when analysing phishing kits.

---

## Objective 2 – Analyse the Phishing Logic

### My Approach

After locating the primary phishing component, I reviewed the source code to understand how user input was processed.

Instead of searching only for credential fields, I examined the application's workflow to determine where sensitive information was collected and handled.

### Why I Looked There

Backend application logic usually contains the complete credential harvesting workflow.

### Skills Practiced

* PHP Analysis
* Source Code Review
* Web Application Investigation

### What I Learned

Reading source code provides significantly more context than interacting with the phishing website itself.

---

## Objective 3 – Identify Supporting Services

### My Approach

While analysing the code, I reviewed external API requests and third-party services referenced by the application.

Whenever an unfamiliar service appeared, I researched its purpose using publicly available documentation to understand why it was included in the phishing kit.

### Why I Looked There

External services often provide attackers with geolocation, victim profiling, or infrastructure support.

### Skills Practiced

* OSINT
* API Investigation
* Threat Intelligence

### What I Learned

Threat intelligence investigations frequently require pivoting between source code analysis and external research.

---

## Objective 4 – Investigate Data Exfiltration

### My Approach

After understanding how credentials were collected, I followed the application's processing functions to determine where harvested information was stored or transmitted.

I analysed logging mechanisms alongside outbound communication functions to reconstruct the attacker's data exfiltration workflow.

### Why I Looked There

Understanding where stolen information is sent is one of the most important objectives during phishing investigations.

### Skills Practiced

* Data Flow Analysis
* Code Tracing
* Exfiltration Investigation

### What I Learned

Many phishing kits include both local logging and remote exfiltration to ensure stolen credentials are preserved.

---

## Objective 5 – Analyse Attacker Infrastructure

### My Approach

After identifying outbound communication methods, I investigated the services used by the phishing kit.

Rather than stopping at the exposed configuration values, I researched the associated platform documentation to understand how attackers interacted with their infrastructure.

### Why I Looked There

Infrastructure analysis provides opportunities to gather additional intelligence beyond the phishing kit itself.

### Skills Practiced

* Infrastructure Analysis
* API Documentation Research
* Threat Intelligence Pivoting

### What I Learned

Exposed configuration data can often reveal valuable intelligence about attacker-controlled infrastructure.

---

## Objective 6 – Threat Intelligence Pivoting

### My Approach

Using information discovered during source code analysis, I pivoted to publicly available resources to gather additional intelligence regarding the phishing campaign.

I combined evidence from the phishing kit with external documentation to build a broader understanding of the attack.

### Why I Looked There

Threat intelligence investigations extend beyond malware analysis by correlating technical artifacts with publicly available information.

### Skills Practiced

* Threat Intelligence
* OSINT
* Infrastructure Attribution
* Intelligence Correlation

### What I Learned

Small pieces of exposed information can become valuable intelligence when combined with external data sources.

---

# Artifacts Explored

| Artifact                | Purpose                                 |
| ----------------------- | --------------------------------------- |
| HTML Files              | Analyse phishing interface              |
| PHP Source Code         | Investigate credential harvesting logic |
| Directory Structure     | Understand application workflow         |
| Configuration Variables | Identify attacker infrastructure        |
| Log Files               | Review harvested data                   |
| Telegram API References | Investigate data exfiltration           |
| External API Calls      | Analyse victim profiling                |
| Source Code Comments    | Gather developer intelligence           |

---

# MITRE ATT&CK Mapping

| Attack Phase         | Technique                          |
| -------------------- | ---------------------------------- |
| Resource Development | Phishing Infrastructure            |
| Credential Access    | Input Capture                      |
| Collection           | Data from Information Repositories |
| Exfiltration         | Exfiltration Over Web Service      |
| Reconnaissance       | Gather Victim Identity Information |

---

# Skills Gained

* Threat Intelligence
* Phishing Kit Analysis
* PHP Source Code Review
* HTML Analysis
* Web Application Investigation
* Data Flow Analysis
* API Investigation
* Telegram Bot Analysis
* OSINT
* Infrastructure Attribution
* Intelligence Correlation
* MITRE ATT&CK Mapping

---

# Defensive Recommendations

* Educate users to verify website URLs before entering sensitive information.
* Enable multi-factor authentication for cryptocurrency wallets whenever supported.
* Monitor for phishing domains impersonating legitimate services.
* Inspect phishing kits for exposed attacker infrastructure to aid threat intelligence.
* Block known malicious domains and communication endpoints.
* Continuously monitor threat intelligence feeds for emerging phishing campaigns.
* Report phishing infrastructure to hosting providers and relevant security communities.

---

# Key Takeaways

* Source code analysis provides deep visibility into phishing kit behaviour.
* Understanding application logic is more valuable than simply identifying stolen data.
* Threat intelligence investigations often require combining code analysis with OSINT.
* Public API documentation can reveal valuable investigative opportunities.
* Small configuration artifacts can lead to meaningful attribution intelligence.

---

# Reflection

This challenge strengthened my understanding of phishing kit analysis and threat intelligence investigations.

Instead of focusing solely on identifying indicators of compromise, I learned how to examine the complete phishing workflow—from credential collection and data handling to attacker infrastructure and intelligence gathering.

The investigation improved my confidence in reviewing PHP source code, tracing application logic, performing OSINT pivots, and documenting technical findings using a structured investigative methodology.

The biggest lesson from this lab was that effective threat intelligence often comes from connecting small technical artifacts with publicly available information to build a complete picture of the attacker's infrastructure and operations.

---

> **Note:** This repository intentionally excludes challenge answers to respect the CyberDefenders platform. Its purpose is to document the investigation methodology, threat intelligence techniques, and practical skills gained while completing the lab.
