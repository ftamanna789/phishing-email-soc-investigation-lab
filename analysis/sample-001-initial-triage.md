# Sample 001 — Email Triage and Header Investigation

**Case type:** Synthetic training scenario  
**Status:** Initial analysis complete; independent authentication and infrastructure checks not performed  
**Analyst focus:** SOC Level 1 phishing triage

## 1. Reported Message
- **Display name:** IT Helpdesk
- **From:** `support@account-alert.invalid`
- **Reply-To:** `reset@identity-check.invalid`
- **Subject:** Urgent: Verify your account today
- **Defanged URL:** `hxxps://account-verify[.]invalid/signin`
- **Pretext:** Account access will allegedly be disabled unless the recipient verifies details.

This sample is fictional. `.invalid` is a reserved, non-resolving domain used for demonstrations.

## 2. Header Observations

| Indicator | Supplied value | Interpretation |
|---|---|---|
| From / Reply-To | Different domains | Mismatch merits investigation; not conclusive on its own |
| SPF | `fail` | Synthetic header claims SPF validation failed |
| DKIM | `none` | Synthetic header claims no DKIM signature was available |
| DMARC | `fail` | Synthetic header claims DMARC evaluation failed |
| Content | Urgent verification request | Pressure-based social engineering cue |
| Link | Defanged sign-in URL | Possible credential-harvesting pretext, not tested |

**Evidence limitation:** These are text fields in a fabricated example, not authentication checks performed against a genuine received email. In a real incident, the analyst should identify trusted receiving-server authentication results and inspect the relevant header chain before relying on them.

## 3. Initial Assessment
**Classification:** Highly suspicious simulated phishing scenario (training-only).  
**Confidence:** High for the *intended scenario*, not a claim about any real-world infrastructure.

A failed or missing SPF/DKIM/DMARC result alone does **not** prove phishing: misconfiguration and mail forwarding can affect authentication. An analyst should corroborate header alignment, sender context, email content, URL characteristics, and user interaction before a final real-world classification.

## 4. Recommended SOC L1 Actions (Hypothetical)
1. Preserve the original message with full headers and record the report source.
2. Verify the trusted authentication-results header and examine From/Reply-To and routing.
3. Analyse URLs as defanged indicators using approved tools; avoid visiting links or opening attachments.
4. Determine whether the recipient clicked, entered credentials, or downloaded anything.
5. Escalate for quarantine, blocking, password reset, or additional response only when supported by evidence and local procedures.
6. Document findings, uncertainty, and escalation decisions in the incident ticket.

## 5. Interview-Ready Explanation
> “I would not classify an email as phishing solely because SPF, DKIM, or DMARC failed. I would treat the authentication failures as strong warning signs, then investigate header alignment, URLs, message content, and potential user impact before making a final classification.”

## Next Exercise
Review the URL and the message’s urgency/credential-verification language; create an IOC assessment and response summary. No active investigation of a real malicious URL is required.
