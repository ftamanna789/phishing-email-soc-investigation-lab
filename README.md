# Phishing Email Detection & Investigation Lab

**SOC Level 1 | Email Security | Threat Analysis | Incident Response**

## Overview
A hands-on blue-team portfolio project focused on investigating suspicious emails using a repeatable SOC analyst workflow. The lab will assess email authentication, sender identity, links and attachments, indicators of compromise (IOCs), and appropriate incident-response actions.

**Project status:** In progress — investigation and findings will be added as the lab is completed.

## Objectives
- Triage a suspicious email and document the initial indicators.
- Examine email headers and assess SPF, DKIM, and DMARC results.
- Investigate sender domains, reply-to mismatches, suspicious URLs, and attachment metadata safely.
- Correlate relevant IOCs with reputable threat-intelligence sources.
- Classify the message based on evidence and recommend containment and escalation actions.
- Produce a concise SOC investigation case study with reproducible evidence.

## Planned Investigation Workflow
1. **Intake & triage:** Record the alert, source, subject, timestamps, and reported behaviour.
2. **Header analysis:** Examine From, Reply-To, Return-Path, Received headers, and authentication results.
3. **IOC extraction:** Defang URLs/domains and record hashes where applicable.
4. **Threat intelligence:** Check reputation and context without opening suspicious links or executing attachments.
5. **Assessment:** Document supporting and contradicting evidence; assign a justified verdict and confidence level.
6. **Response:** Recommend reporting, blocking, quarantine, user notification, or escalation as appropriate.
7. **Reporting:** Summarise the timeline, evidence, outcome, limitations, and lessons learned.

## Tools & Techniques
Planned: **CyberChef**, **VirusTotal** (public IOC checks where safe), **Python**, email header inspection, and **MITRE ATT&CK** mapping where supported by evidence.

> The tools listed above form the intended workflow; their use does not imply an investigation has been completed.

## Planned Repository Structure
```text
phishing-email-soc-investigation-lab/
├── README.md
├── samples/              # Sanitised, harmless sample emails only
├── evidence/             # Redacted screenshots and extracted indicators
├── analysis/             # Header and IOC analysis notes
└── reports/              # Final case-study report
```

Folders and reports will be added as the practical investigation progresses.

## Safety & Ethics
- Use only authorised or publicly provided, sanitised samples.
- Do not click live suspicious links, open untrusted attachments, or execute malware.
- Defang suspicious URLs and redact personal information, credentials, tokens, and private email content before publishing.
- Treat third-party reputation results as supporting evidence, not definitive proof.

## Expected Deliverables
A documented email triage, header/IOC analysis, evidence-backed classification, recommended SOC response, and a final case-study report.

## Author
**Fouzia Tamanna**  
[GitHub Profile](https://github.com/ftamanna789) · [Portfolio](https://fouziatamanna.net)
