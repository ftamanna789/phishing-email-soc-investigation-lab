# Sample 002 — Email Content and URL Analysis

**Case ID:** PHISH-LAB-002  
**Source:** [Synthetic training email](../samples/sample-002-full-headers.md)  
**Method:** Manual analysis of fictional content; no URL visit, DNS lookup or live reputation check.

## Warning signs

| Indicator | Evidence in sample | Assessment |
|---|---|---|
| Sender impersonation | Display name “Company IT Helpdesk” with `helpdesk@company.invalid` | Claimed corporate authority; requires independent verification in a real case |
| Domain mismatch | From: `company.invalid`; Reply-To: `notices.attacker.invalid` | Replies are directed to a different domain; suspicious in context, not proof alone |
| Urgent language | “Your mailbox needs revalidation today to prevent disruption.” | Creates time pressure to bypass normal scrutiny |
| Account verification pretext | Mailbox revalidation requested | Induces recipient to take action on account access |
| Unexpected login-themed link | `hxxps://mailbox-check[.]invalid/login` | Simulated credential-entry lure; reserved `.invalid` domain, non-operational |
| Authentication domain alignment | Simulated SPF pass and DKIM pass for `notices.attacker.invalid`; DMARC fail for visible From `company.invalid` | Neither passing mechanism aligns with visible From |

## Analyst finding

**Training verdict:** Suspicious simulated phishing / impersonation attempt. Multiple contextual indicators collectively justify suspicion in this fictional scenario. **No real sender, phishing site, user compromise or malicious infrastructure was verified.**

## SOC Level 1 response recommendations

1. Preserve the original message and trusted headers, record the user report and delivery context.
2. Verify sender identity and authentication using actual receiving-server evidence.
3. Analyse the destination safely with approved tools and defanged indicators, without visiting untrusted links.
4. Determine whether the user clicked, entered credentials or downloaded a file; review relevant SIEM/identity/EDR evidence when authorised.
5. Follow the incident playbook to contain and escalate credible compromise, then document the timeline and outcome.

## Interview-ready answer

> “Common warning signs include suspicious sender addresses, urgent language, unexpected links, and requests for sensitive information, such as passwords or login credentials. I would examine these indicators together with email authentication and domain alignment before making a classification.”

## Limitations

This is an educational synthetic email. All header authentication results are invented. No live investigation, URL reputation check, account containment or real incident response occurred.
