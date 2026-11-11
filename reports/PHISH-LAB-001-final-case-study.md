# Phishing Email Investigation — Final Case Study (Synthetic Lab)

**Analyst:** Fouzia Tamanna  
**Role focus:** SOC Analyst Level 1  
**Case ID:** PHISH-LAB-001  
**Report date:** 11 November 2026  
**Case status:** Completed *desktop review of a fictional sample*; real-world validation not applicable  
**Scope:** Email triage, header interpretation, IOC extraction, hypothetical response and escalation

> **Training simulation only.** No real phishing email, active malicious domain, recipient account, sign-in logs or endpoint were investigated. The email authentication results and employee-click scenario are fabricated. All findings below are derived solely from the synthetic example.

## 1. Executive Summary
A fictional employee received a message impersonating an IT helpdesk and demanding urgent account verification. The sample's `From` and `Reply-To` addresses use different domains, its supplied `Authentication-Results` text states SPF failure, no DKIM signature, and DMARC failure, and its body uses an account-disabling pretext with a defanged sign-in URL.

**Outcome:** Classified as a **simulated phishing / credential-harvesting scenario** with strong suspicious indicators for training purposes. No actual account compromise or malware activity can be concluded. Proposed SOC actions are documented, but **none was executed on a live system**.

## 2. Source Evidence and Scope
Reviewed repository files:
- [Synthetic email sample](../samples/sample-001-synthetic-phishing.md)
- [Initial triage notes](../analysis/sample-001-initial-triage.md)
- [Proposed incident response](sample-001-incident-response-summary.md)

No original `.eml` from a live message, verified receiving-server headers, screenshots, delivered-message metadata, clicked-link telemetry, threat-intelligence results, DNS records, authentication logs, or EDR telemetry were supplied.

## 3. Evidence Register

| ID | Evidence from fictional sample | Interpretation | Confidence / limitation |
|---|---|---|---|
| E01 | Display name: `IT Helpdesk`; From: `support@account-alert.invalid` | Impersonates an IT support function | Training text, not attributable to a real sender |
| E02 | Reply-To: `reset@identity-check.invalid` | Different domain from From; merits scrutiny | Mismatch alone is not proof of phishing |
| E03 | `spf=fail` | Supplied text claims SPF check failed | Synthetic; not independently verified |
| E04 | `dkim=none` | Supplied text claims no DKIM signature | Synthetic; not independently verified |
| E05 | `dmarc=fail` | Supplied text claims DMARC failure | Synthetic; not independently verified |
| E06 | Subject: `Urgent: Verify your account today` | Creates time pressure | Contextual indicator |
| E07 | Body warns the account will be disabled | Coercive account-verification pretext | Consistent with credential-phishing scenario |
| E08 | `hxxps://account-verify[.]invalid/signin` | Login-themed link and possible credential-harvesting lure | Reserved, intentionally non-resolving test domain; never visited |

**Analyst caution:** Authentication failures alone do not establish malicious intent. Legitimate messages can fail checks because of configuration or forwarding; authentic receiving-server results and sender context are needed for real-world classification.

## 4. IOC and URL Assessment

| Type | Indicator | Assessment |
|---|---|---|
| Sender domain | `account-alert.invalid` | Fictional domain; no reputation conclusion |
| Reply-To domain | `identity-check.invalid` | Fictional and different from sender |
| URL domain | `account-verify.invalid` | Fictional sign-in-themed domain |
| URL path | `/signin` | Supports simulated login lure |
| URL | `hxxps://account-verify[.]invalid/signin` | Already defanged; do not visit |
| File hash | Not available | No attachment or executable supplied |
| Source IP | Not available | No trusted routing/server details supplied |

**No VirusTotal result, DNS resolution, link detonation or live threat-intelligence verdict was obtained.** The domain suffix `.invalid` is reserved for non-resolving examples; do not submit these indicators as genuine malicious IOCs.

## 5. Analyst Decision
- **Type:** Simulated phishing / credential-harvesting exercise.
- **Suspicion:** High *within the fictional scenario* based on combined sender, content, authentication-text, and link indicators.
- **Confirmed compromise:** None.
- **Real-world classification:** Not applicable; evidence is synthetic.
- **Rationale:** The message combines IT-helpdesk impersonation, domain mismatch, account-loss urgency and a login-themed destination. The copied authentication header claims failure, but is not independent proof.

## 6. Hypothetical Incident Response
**Assumed scenario for this section only:** A user says they clicked a link and entered their password. This is not an observed event.

1. **Assess:** Establish what was clicked, when, whether a password/MFA code was submitted and whether anything was downloaded; preserve the reported email.
2. **Contain:** Escalate immediately as possible credential compromise; coordinate password reset, session revocation and identity safeguards with authorised teams following playbooks.
3. **Investigate:** Review sign-in/MFA logs and relevant endpoint telemetry; look for unusual sign-ins, post-click activity and additional targeted recipients.
4. **Escalate:** Notify SOC L2, incident response and identity administrators as required; propose quarantine or blocking actions when justified.
5. **Document:** Record source evidence, timestamps, impacts, decisions, action owners, unresolved questions and handover notes.

**Priority:** Prompt/high-priority triage would be reasonable for reported credential disclosure, but organisational severity depends on its incident matrix and confirmed impact.

## 7. Illustrative SOC Ticket
- **Ticket:** PHISH-LAB-001 (training only)
- **Reported event:** Suspicious IT-helpdesk account-verification email
- **Possible impact:** Credential disclosure and account takeover (hypothetical)
- **Evidence collected:** Sample message text and analyst notes only
- **Recommended action:** Escalate, verify reported user interaction and sign-in activity, coordinate access protection, investigate scope
- **Actions actually performed:** Review and documentation of synthetic material
- **Resolution:** Training case-study review complete; live incident resolution not applicable

## 8. Lessons Learned
- Use multiple corroborating indicators rather than treating authentication failure as automatic proof.
- Distinguish header values quoted in a sample from trusted, verified receiving-server results.
- Treat possible credential submission urgently, while documenting whether compromise is suspected or confirmed.
- Never claim containment, detection-tool execution or real-world threat intelligence without evidence.
- Preserve a clear trail from source material to observation, analysis, response recommendation and limitation.

## 9. Next Extension
To turn this into a stronger hands-on portfolio demonstration, obtain an **authorised, sanitised** real email sample with full headers, conduct tool-assisted header/IOC checks, capture redacted evidence, and update the case with clearly attributed observations. Do not publish private messages, credentials, or live malicious links.

---
**Repository:** [Phishing Email SOC Investigation Lab](../README.md)  
**Author portfolio:** [Fouzia Tamanna](https://fouziatamanna.net)
