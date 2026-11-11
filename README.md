# Phishing Email Detection & Investigation Lab

**SOC Level 1 | Email Security | Header Analysis | Incident Response**

**Project status: Completed — two synthetic training case studies (11 November 2026).** This is a simulated desktop investigation, not a live phishing investigation.

## Overview
This portfolio lab demonstrates how an entry-level SOC analyst can triage suspicious email, interpret email authentication, identify social-engineering indicators, assess URLs safely, and write an evidence-aware incident report. The samples and authentication results are fictional; no real sender, delivery, clicked link, endpoint or compromised account was investigated.

## Completed case studies

### Case 001 — Simulated Helpdesk Impersonation
- [Synthetic email](samples/sample-001-synthetic-phishing.md)
- [Initial triage notes](analysis/sample-001-initial-triage.md)
- [Detailed header analysis](analysis/sample-001-detailed-header-analysis.md)
- [Incident response summary](reports/sample-001-incident-response-summary.md)
- [Final case study — PHISH-LAB-001](reports/PHISH-LAB-001-final-case-study.md)

**Finding:** Sample claims SPF failure, no DKIM and DMARC failure; fake helpdesk identity, mismatched reply address and urgent login request are contextual red flags.

### Case 002 — SPF/DKIM Pass, DMARC Fail
- [Synthetic full headers](samples/sample-002-full-headers.md)
- [Header and alignment walkthrough](analysis/sample-002-header-walkthrough.md)
- [Warning signs and URL analysis](analysis/sample-002-content-url-analysis.md)
- [Final case study — PHISH-LAB-002](reports/PHISH-LAB-002-final-case-study.md)

**Finding:** In the constructed message, SPF and DKIM pass for `notices.attacker.invalid`, but neither is aligned to the displayed From domain `company.invalid`; the supplied DMARC result is fail. The urgent mailbox-revalidation message and login-themed link provide additional suspicious indicators.

## Investigation workflow
1. **Assess** — examine user report, email content, headers and potential interaction.
2. **Contain** — recommend appropriate access protections under a real organisation's playbook.
3. **Investigate** — compare From, Return-Path, Reply-To, SPF, DKIM, DMARC; inspect indicators safely and review approved logs if available.
4. **Escalate** — involve appropriate incident response or identity teams for credible exposure.
5. **Document** — record evidence, confidence, limitations, response recommendations and outcome.

## Techniques demonstrated
- Manual email-header parsing and SPF/DKIM/DMARC domain-alignment reasoning
- Sender/Reply-To and Return-Path comparison
- Phishing-content indicators: urgency, claimed authority and credential requests
- Defanged URL assessment, hypothetical SOC triage and incident documentation

**Not performed:** Live DNS or mail checks, cryptographic DKIM validation, VirusTotal lookup, link detonation, endpoint/SIEM investigation, or real account containment. These are possible future extensions, not completed work.

## Safety and ethics
All email samples are invented. The `.invalid` domains and `192.0.2.44` documentation IP are not live malicious IOCs. No untrusted link was visited, no malware executed, and no real user data was used. A simulated classification is not proof of an actual phishing incident.

## Interview takeaway
“Common warning signs include suspicious sender addresses, urgent language, unexpected links, and requests for sensitive information, such as passwords or login credentials. I would also review the email headers and authentication-domain alignment before making a classification.”

## Author
**Fouzia Tamanna**  
[GitHub Profile](https://github.com/ftamanna789) · [Portfolio](https://fouziatamanna.net)
