# Sample 001 — SOC Incident Response Summary

**Scenario:** Synthetic phishing-email investigation for SOC Level 1 training  
**Status:** Proposed response playbook; no real incident occurred and no containment actions were performed.

## Scenario and Initial Assessment

The sample email claims to be from an IT Helpdesk and pressures the recipient to verify an account using a defanged, fictional URL: `hxxps://account-verify[.]invalid/signin`. Its fabricated headers show `spf=fail`, `dkim=none`, and `dmarc=fail`. These are **simulated indicators**, not independently verified authentication results.

**Training assessment:** Highly suspicious phishing scenario, possibly designed for credential harvesting. Actual user interaction and account compromise have **not** been observed.

## Hypothetical User Report

Assume an employee reports having clicked the link **and entered their password**. As a SOC Level 1 analyst, respond as follows:

### 1. Assess
- Confirm the message, approximate click time, destination, whether credentials or MFA codes were entered, and whether a file was downloaded or opened.
- Record the affected account, device, and other available incident details without asking the employee to disclose their password.
- Treat disclosed credentials as a **potential account compromise**, not proof of a successful attacker sign-in.

### 2. Contain
- Immediately escalate the suspected credential compromise through the organisation's incident-response process.
- Coordinate an urgent password reset, active-session/token revocation, and any required account safeguards with authorised identity administrators.
- If malicious downloads or execution are suspected, follow the approved endpoint isolation/EDR procedure. Do not automatically isolate a device solely because a page was clicked.

### 3. Investigate
- Review identity-provider sign-in logs, MFA events, device activity, and unusual geolocation/IP patterns.
- Check whether the message was delivered to other recipients and whether any other users interacted with it.
- Record defanged URL/domain indicators; assess with approved tools. Do not visit a suspicious URL or execute untrusted attachments.
- Preserve email headers, relevant logs, timeline, analyst notes, and case references.

### 4. Escalate
- Notify the relevant SOC L2, incident-response, and identity teams as required by severity and playbooks.
- Recommend phishing-message quarantine, indicator blocking, further hunting, or user outreach when supported by evidence and organisational policy.

### 5. Document
- Capture initial alert/report, evidence sources, observed versus hypothetical facts, actions requested and completed, timestamps, owners, and outstanding questions.
- Close or transfer the ticket only under the local incident-handling process.

## Sample SOC Ticket Summary (Illustrative, Not a Real Incident)

**Title:** Suspected phishing — user reports credential submission (training simulation)  
**Initial priority:** High for prompt triage; final priority depends on local matrix and confirmed impact  
**Evidence:** Fictional sender/Reply-To mismatch, simulated authentication failures, pressure-based content, defanged fictional link  
**Risk:** Potential account takeover if a password were entered on an attacker-controlled site  
**Recommended next steps:** Escalate immediately; coordinate credentials/session protection; inspect sign-in and endpoint logs; determine scope; document all findings  
**Outcome:** Pending — no actual account, device, link, or log was investigated

## Interview Answer

> First, I would confirm exactly what the employee clicked and whether they entered any credentials or downloaded anything. Because they entered their password, I would treat the situation as a potential account compromise and immediately escalate it. Following company procedures, I would coordinate a password reset and revocation of active sessions, investigate sign-in logs and possible user impact, check whether others received the same message, and document all findings and actions.

**Remember:** Assess → Contain → Investigate → Escalate → Document.

## Limitations

This lab uses reserved `.invalid` domains and synthetic headers. No real phishing campaign, authentication test, URL reputation result, account compromise, or remediation outcome should be inferred from this case.
