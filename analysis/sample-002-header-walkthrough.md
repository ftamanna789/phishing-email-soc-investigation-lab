# Sample 002 — Worked Email Header Analysis

**Case:** PHISH-LAB-002  
**Evidence source:** [Synthetic training message](../samples/sample-002-full-headers.md)  
**Method:** Manual, offline interpretation of invented headers; no live authentication, DNS, email delivery, or reputation checks.

## Key findings

| Field | Synthetic value | Analytical meaning |
|---|---|---|
| From | `helpdesk@company.invalid` | Claimed visible identity: `company.invalid` |
| Return-Path | `bounce@notices.attacker.invalid` | Different SMTP envelope-sender domain |
| Reply-To | `helpdesk@notices.attacker.invalid` | Responses would go to the other domain |
| Received | `mail.notices.attacker.invalid [192.0.2.44]` | Illustrative sending hop only; address is reserved TEST-NET |
| SPF | `pass` for `notices.attacker.invalid` | In this scenario SPF passes for envelope-sender domain, **not** the displayed From domain |
| DKIM | `pass`, `header.d=notices.attacker.invalid` | In this scenario signing domain passes DKIM, but is different from visible From |
| DMARC | `fail`, `header.from=company.invalid` | Neither claimed passing SPF domain nor claimed passing DKIM domain aligns with visible From domain |
| Subject / URL | Urgent mailbox revalidation and `hxxps://mailbox-check[.]invalid/login` | Account-verification pressure and login lure; URL is non-operational |

### Why SPF and DKIM can pass while DMARC fails
SPF verifies whether a sending IP is authorised for the **SMTP envelope** domain. DKIM verifies a signature from the **signing** domain. DMARC requires a passing SPF or DKIM result **aligned** with the visible RFC5322 From domain. Here, both simulated passes are for `notices.attacker.invalid`, while visible From is `company.invalid`; neither aligns, so the simulated DMARC failure is logically consistent.

**Important:** SPF/DKIM passes do not automatically mean a message is safe, and a From-versus-Reply-To mismatch alone is not definitive evidence. Header results are only hypothetical because the sample and DKIM signature are fabricated.

### SOC triage outcome
- **Scenario classification:** Suspicious simulated impersonation / credential-phishing attempt
- **Observed user impact:** None (no real recipient or interaction)
- **Actual validation performed:** Text comparison and reasoned alignment analysis only
- **Recommended next steps for a real incident:** Obtain original received message and trusted authentication results; verify routing/DNS, assess defanged URLs with approved tooling, investigate user interaction, and escalate as warranted

### Interview talking point
> “SPF and DKIM can both pass while DMARC fails if they authenticate domains that are not aligned with the visible From address. I would investigate the actual sender identity, delivery path, message content, URL and potential user impact before reaching a final classification.”

## Limitations
The domains use the reserved `.invalid` suffix and `192.0.2.44` is reserved for documentation. No real MX, SPF DNS policy, DKIM public key, signed body, receiving server, sign-in logs or IOC intelligence is available, so no live verification or compromise claim is made.
