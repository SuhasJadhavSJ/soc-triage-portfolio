# SOC Alert Triage & Incident Investigation Portfolio

**Independent Blue Team Practice | SOC Analyst L1 | October 15-31, 2026**

## Overview

This repository documents my hands-on practice in Security Operations Center (SOC) alert triage, incident investigation, evidence correlation, and incident reporting.

The objective is to strengthen my practical SOC Analyst L1 skills by investigating a minimum of five alerts per day, documenting the evidence, determining defensible verdicts, and recommending appropriate next steps.

The sprint focuses on working with security events and investigation artifacts rather than completing guided labs alone. Each completed investigation is documented as an incident ticket that demonstrates the investigation process, supporting evidence, reasoning, and recommended actions.

**Sprint period:** October 15-31, 2026  
**Minimum target:** 85 documented alert investigations  
**Primary focus:** Alert triage, incident classification, and technical documentation

> **Scope:** This is an independent learning and simulation portfolio. Investigations are based on lab telemetry, publicly available datasets, and cybersecurity training platforms. No production SOC experience is implied.

## Objectives

- Investigate at least five alerts per day.
- Identify suspicious patterns in authentication, endpoint, network, and email telemetry.
- Correlate related events to establish an evidence-based incident timeline.
- Distinguish true positives, false positives, benign true positives, and inconclusive cases.
- Practice basic SIEM searches and endpoint investigation techniques.
- Map relevant findings to MITRE ATT&CK when supported by evidence.
- Document investigation findings and recommended containment or remediation steps.
- Track investigation time, verdicts, and completion status.
- Build a GitHub portfolio that demonstrates practical SOC investigation skills.

## Investigation Categories

| Category | Investigation focus |
|---|---|
| Authentication attacks | SSH brute force, failed logins, password spraying, suspicious successful logons |
| Phishing analysis | Sender verification, email headers, URLs, domains, and indicators of compromise |
| Account compromise | Unusual login patterns, suspicious source addresses, and authentication anomalies |
| Endpoint detection | Suspicious process execution, parent-child relationships, and command-line arguments |
| PowerShell investigation | Encoded commands, suspicious scripts, and potentially malicious execution patterns |
| Network investigation | Port scans, unusual outbound connections, and suspicious network activity |
| Malware indicators | File hashes, process behavior, network indicators, and available forensic artifacts |
| Persistence and lateral movement | Suspicious scheduled tasks, services, account activity, and related endpoint events |
| Benign activity | Legitimate administrative actions, expected system behavior, and false-positive analysis |

The investigation categories will increase in complexity throughout the sprint. Not every category will necessarily produce a confirmed malicious incident.

## Tools and Technologies

The following tools and data sources may be used depending on the investigation.

- **SIEM:** Wazuh, Splunk
- **Windows investigation:** Event Viewer, Windows Security logs, Sysmon
- **Linux investigation:** Authentication logs, SSH logs, system logs
- **Network analysis:** Wireshark, network logs, PCAP artifacts
- **Threat intelligence:** VirusTotal, URLhaus, and relevant reputation sources
- **Investigation platforms:** TryHackMe, LetsDefend, CyberDefenders, and other suitable training resources
- **Documentation:** Markdown, CSV, Git, GitHub
- **Framework:** MITRE ATT&CK

Tool usage will depend on the available telemetry and the requirements of each case.

## Investigation Methodology

Every alert follows a consistent workflow.

### 1. Alert Intake

- Record the alert name, detection source, timestamp, severity, and triggering rule.
- Identify the affected host, account, and relevant network indicators.
- Understand what behavior triggered the detection.

### 2. Evidence Collection

- Inspect the relevant raw events and associated timestamps.
- Review source and destination IP addresses, ports, protocols, and usernames.
- Examine process names, command-line arguments, parent processes, and available network events.
- Collect related events to determine whether the activity forms a broader pattern.

### 3. Correlation and Validation

- Correlate events across available log sources.
- Establish a timeline of relevant activity.
- Validate suspicious indicators using appropriate threat intelligence sources.
- Separate confirmed facts from assumptions and identify evidence gaps.

### 4. Verdict Classification

Each investigation receives a classification based on the evidence.

| Classification | Meaning |
|---|---|
| True Positive (TP) | The detection correctly identifies activity that meets the malicious or suspicious detection criteria. |
| False Positive (FP) | The detection incorrectly identifies benign activity as meeting its detection criteria. |
| Benign True Positive (BTP) | The detection correctly identifies the activity, but the activity is legitimate or authorized. |
| Inconclusive | The available evidence is insufficient to support a reliable final classification. |

### 5. Incident Documentation

Each completed ticket contains:

1. **Summary:** What triggered the investigation and which assets were involved.
2. **Evidence:** Relevant events, timestamps, indicators, queries, and correlated findings.
3. **Verdict:** Classification, confidence, and evidence-based rationale.
4. **Next Steps:** Recommended investigation, containment, remediation, or escalation.

### 6. Closure and Review

- Record the final status and time spent on triage.
- Document unresolved questions and investigation limitations.
- Record relevant MITRE ATT&CK techniques when justified.
- Add the report link to the alert tracker.
- Review the investigation for unsupported claims and missing evidence.

## Sprint Roadmap

| Period | Focus | Minimum target |
|---|---|---:|
| October 15-17 | Authentication alerts and basic event correlation | 15 |
| October 18-21 | Phishing, account security, and benign activity | 20 |
| October 22-25 | Endpoint and network investigations | 20 |
| October 26-29 | PowerShell, malware indicators, persistence, and lateral movement | 20 |
| October 30-31 | Mixed-alert investigations, quality review, and portfolio finalization | 10 |
| **Total** | **17 calendar days** | **85** |

These numbers represent planned targets, not completed investigations. Progress will be updated as cases are actually investigated and documented.

## Repository Structure

```text
soc-triage-portfolio/
├── README.md
├── tracker/
│   └── alert-tracker.csv
├── incidents/
│   ├── INC-001-ssh-brute-force.md
│   ├── INC-002-failed-logins-followed-by-success.md
│   ├── INC-003-rdp-authentication-investigation.md
│   └── ...
├── queries/
│   ├── wazuh.md
│   ├── splunk-spl.md
│   └── windows-event-logs.md
└── reports/
    └── october-2026-summary.md
```

Each incident report will use a unique ticket ID. The example filenames illustrate the intended naming convention and do not imply that these tickets have already been completed.

## Master Alert Tracker

This table is the central index for all SOC alert investigations conducted during the October 15-31, 2026 sprint. Each ticket ID links to its detailed investigation report.

### Sprint Metrics

| Metric | Target | Actual |
|---|---:|---:|
| Investigation period | 17 days | In progress |
| Total tickets | 85 minimum | 0 documented |
| Average daily volume | 5 minimum | 0 |
| True Positives | Track actual | 0 |
| False Positives | Track actual | 0 |
| Benign True Positives | Track actual | 0 |
| Inconclusive | Track actual | 0 |

*Update the actual figures only when corresponding tickets have been documented and reviewed.*

### Incident Index

| Ticket ID | Alert / Scenario | Source Platform | Log Sources Analyzed | MITRE ATT&CK | Verdict | Write-Up |
|---|---|---|---|---|---|---|
| INC-001 | Multiple authentication failures followed by a success | Wazuh |  | T1110; T1078 | True Positive (Confirmed Account Takeover)  | [View Report](incidents/INC-001.md) |
| INC-002 | To be investigated | Wazuh / Windows | To be confirmed | TBD | Pending | [View Report](incidents/INC-002.md) |
| INC-003 | To be investigated | Windows Event Logs | To be confirmed | TBD | Pending | [View Report](incidents/INC-003.md) |
| INC-004 | To be investigated | To be confirmed | To be confirmed | TBD | Pending | [View Report](incidents/INC-004.md) |
| INC-005 | To be investigated | To be confirmed | To be confirmed | TBD | Pending | [View Report](incidents/INC-005.md) |

*The rows above are placeholders for the first five investigations. Replace the scenario, platform, log sources, technique, and verdict with verified findings. Add one row for every subsequent ticket.*

### Verdict Definitions

- **True Positive (TP):** The detection correctly identified activity meeting the malicious or suspicious detection criteria.
- **False Positive (FP):** The detection incorrectly classified benign activity as suspicious.
- **Benign True Positive (BTP):** The detection correctly identified the activity, but the activity was legitimate.
- **Inconclusive:** Available evidence does not support a reliable final classification.
- **Pending:** Investigation or documentation has not been completed.

### Navigation

- [Incident Reports](incidents/)
- [Alert Tracker CSV](tracker/alert-tracker.csv)
- [SIEM Queries and Investigation Notes](queries/)
- [October Sprint Summary](reports/october-2026-summary.md)

All report links use relative GitHub paths so readers can navigate directly to the Markdown files in this repository.

## Metrics and Quality Standards

The sprint will measure both investigation volume and quality.

- **Completed investigations:** Number of documented cases.
- **Daily throughput:** Number of completed investigations per day.
- **Verdict distribution:** Number of TP, FP, BTP, and inconclusive cases.
- **Mean triage time:** Average time spent per investigation, using a consistent definition.
- **Evidence quality:** Whether conclusions are supported by recorded telemetry.
- **Documentation completeness:** Whether every ticket includes a summary, evidence, verdict, and next steps.
- **Escalation quality:** Whether unresolved or higher-risk cases are escalated appropriately.

A high number of tickets alone does not demonstrate investigation competence. Each report must be reproducible, evidence-backed, and transparent about limitations.

## MITRE ATT&CK Mapping

MITRE ATT&CK will be used to describe relevant adversary behavior where the available evidence supports a mapping.

Potential areas of investigation include:

- **T1110:** Brute Force
- **T1566:** Phishing
- **T1059.001:** PowerShell
- **T1055:** Process Injection
- **T1003.001:** LSASS Memory

These are examples of techniques that may be relevant to future investigations, not claims that every technique has been observed or confirmed in this lab. Technique mappings will be validated against the evidence for each ticket.

## Evidence and Reporting Principles

To maintain the integrity of this portfolio:

- No alert will be marked malicious solely because a detection rule fired.
- No indicator will be described as malicious without supporting evidence.
- Threat intelligence reputation will be treated as one investigative input, not conclusive proof.
- Lab simulations will be identified as simulations.
- Recommended containment actions will be distinguished from actions actually performed.
- Sensitive information, credentials, API keys, and private infrastructure details will not be published.
- Inconclusive investigations will remain inconclusive until sufficient evidence is available.

## Final Deliverables

By October 31, 2026, the intended deliverables are:

- A minimum of 85 documented alert investigations.
- A structured incident ticket collection.
- A searchable alert tracker with investigation metrics.
- SIEM query examples and relevant investigation notes.
- A sprint summary covering investigation volume, verdict distribution, recurring findings, and lessons learned.
- A selection of detailed cases suitable for technical interview discussion.

Actual completion statistics and results will be added at the end of the sprint.

## About This Project

This portfolio is part of my independent preparation for SOC Analyst L1 and Blue Team roles. It demonstrates a structured approach to security monitoring, alert validation, log analysis, incident documentation, and evidence-based decision-making.

**Author:** Suhas Jadhav  
**Focus:** SOC Operations | Blue Team | SIEM | Incident Investigation

**Portfolio status:** In progress  
**Sprint:** October 15-31, 2026
