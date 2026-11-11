# PHISH-LAB-002 — Final SOC Phishing Investigation Case Study

**Date:** 11 November 2026  
**Focus:** SOC Level 1 email triage, authentication domain alignment, content/URL assessment  
**Status:** Complete simulated desktop investigation — **not a real incident**

## Executive summary
A synthetic email impersonates a company IT helpdesk and requests urgent mailbox revalidation through a fictional login link. The visible From domain (`company.invalid`) differs from the envelope sender and DKIM signing domain (`notices.attacker.invalid`). The **fabricated** header declares SPF=pass and DKIM=pass but DMARC=fail. This is internally consistent because neither passing authentication domain aligns with the visible From domain. Other suspicious indicators are a different Reply-To domain, urgency, and a login-themed lure.

**Training finding:** Suspicious simulated impersonation / credential-phishing attempt; no real-world phishing activity or compromise established.

## Evidence and investigation
| Evidence | Finding | Interpretation |
|---|---|---|
| Visible From | `helpdesk@company.invalid` | Claims corporate IT identity |
| Return-Path | `bounce@notices.attacker.invalid` | Separate envelope domain |
| Reply-To | `helpdesk@notices.attacker.invalid` | Replies routed to another domain |
| Authentication-Results | SPF pass: `notices.attacker.invalid` | Only synthetic envelope-domain authorisation |
| DKIM | Pass: `d=notices.attacker.invalid` | Synthetic signing-domain authentication |
| DMARC | Fail: `header.from=company.invalid` | Neither SPF nor DKIM pass aligns with visible From |
| Received | `192.0.2.44` | Reserved documentation IP, not a verified sender |
| Message body | “Your mailbox needs revalidation today to prevent disruption.” | Urgency / account-verification pressure |
| Link | `hxxps://mailbox-check[.]invalid/login` | Fictional defanged login-themed URL |

**Authentication explanation:** DMARC can pass if **either** SPF or DKIM passes with proper alignment to the RFC5322 From domain. In this example, both passes concern a different organizational domain, so the stated DMARC failure is consistent.

## SOC workflow (recommended, not executed)
1. **Assess:** Preserve message and headers, interview recipient to establish click, credential submission or download.
2. **Contain:** Where credible exposure exists, coordinate account safeguards, password reset and session revocation under approved procedures.
3. **Investigate:** Check trusted mail gateway headers, identity logs, SIEM and EDR data, and safe URL reputation intelligence for a *real* incident.
4. **Escalate:** Notify L2 / IR team according to severity and playbook.
5. **Document:** Record indicators, timestamps, confidence, decisions, owner and outcome.

## Interview takeaway
> “Common warning signs include suspicious sender addresses, urgent language, unexpected links, and requests for sensitive information, such as passwords or login credentials. I would also verify authentication results and domain alignment before concluding whether the email is phishing.”

## Outcome and limitations
- **Simulated verdict:** Suspicious phishing-themed email.
- **Confirmed compromise / affected users:** None; this is not a real delivery or click.
- **Checks actually performed:** Manual interpretation and comparison of constructed text.
- **Checks not performed:** No DNS, cryptographic DKIM verification, VirusTotal, link detonation, EDR, SIEM, or live-response action.
- **Lesson learned:** SPF and DKIM pass do not mean a message is safe; DMARC requires alignment of at least one passing mechanism.

## Reproducible source
- [Training sample](../samples/sample-002-full-headers.md)
- [Header walkthrough](../analysis/sample-002-header-walkthrough.md)
- [Content and URL analysis](../analysis/sample-002-content-url-analysis.md)

**Safety:** Domains ending in `.invalid` and IP `192.0.2.44` are documentation-only values. Do not submit them as real malicious IOCs.
