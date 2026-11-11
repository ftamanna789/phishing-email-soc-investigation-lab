# Sample 001 — Detailed Email Header Analysis

**Case:** PHISH-LAB-001 | **Analyst:** Fouzia Tamanna | **Date:** 11 November 2026  
**Source:** [Synthetic sample email](../samples/sample-001-synthetic-phishing.md)  
**Scope:** Offline interpretation of fabricated header text; no real mail-server validation or external lookups.

## Header excerpt
```text
From: "IT Helpdesk" <support@account-alert.invalid>
Reply-To: reset@identity-check.invalid
To: employee@example.invalid
Subject: Urgent: Verify your account today
Date: Wed, 11 Nov 2026 09:14:00 +0000
Message-ID: <sample-001@account-alert.invalid>
Authentication-Results: mail.example.invalid;
  spf=fail smtp.mailfrom=account-alert.invalid;
  dkim=none;
  dmarc=fail header.from=account-alert.invalid
```

## Field-by-field interpretation

| Field | Observed value | SOC interpretation |
|---|---|---|
| From display name | `IT Helpdesk` | Claimed identity; display names are easily imitated |
| From address | `support@account-alert.invalid` | Claimed sender; does not itself establish an official IT organisation |
| Reply-To | `reset@identity-check.invalid` | Reply destination differs from From domain; warrants investigation but can be legitimate |
| To | `employee@example.invalid` | Fictional recipient; no actual recipient evidence |
| Subject | `Urgent: Verify your account today` | Urgency and verification pretext |
| Date | `Wed, 11 Nov 2026 09:14:00 +0000` | Plausible timestamp, but sender-supplied and not independently trustworthy |
| Message-ID | `<sample-001@account-alert.invalid>` | Identifier format; domain matches From but may be chosen by sender |
| Authentication-Results authserv-id | `mail.example.invalid` | Fabricated receiver identity; result is not attributable to a trusted receiving service |
| SPF | `fail` for `smtp.mailfrom=account-alert.invalid` | Sample claims the connecting sending IP was not authorised by SPF; cannot verify without sending IP, receiver result and domain DNS |
| DKIM | `none` | Sample claims no DKIM signature was found; **none is not fail** |
| DMARC | `fail` for `header.from=account-alert.invalid` | Sample claims no aligned passing SPF or DKIM; cannot independently recalculate |
| Received | **Not provided** | Cannot reconstruct hop path or connecting IP |
| Return-Path | **Not provided** | Envelope sender only appears as `smtp.mailfrom` in the fabricated authentication field |
| DKIM-Signature | **Not provided** | Consistent with stated `dkim=none`, but the full original message is unavailable |

## Authentication logic

- **SPF:** An authorised mail server is determined using the sending IP and the envelope MAIL FROM (or HELO identity in applicable cases), not simply the visible display name. The sample explicitly says `spf=fail`, but is not a live SPF test.
- **DKIM:** `dkim=none` indicates no usable DKIM signature was reported. It must not be described as `dkim=fail`.
- **DMARC:** Requires a passing SPF **or** DKIM result aligned with the RFC5322 From domain. With the sample's claimed SPF failure and no DKIM signature, the claimed `dmarc=fail` is internally consistent; DMARC alignment has **not** been independently tested.
- **Different From and Reply-To domains:** This is a contextual warning, not DMARC alignment proof. Reply-To is not the domain directly checked for DMARC alignment.

## Missing evidence / next checks for a real authorised email

1. Obtain the original `.eml` or full **Show original / View source** output, preserving headers and custody.
2. Identify trusted receiving-server `Authentication-Results` and examine the full `Received` chain for hops and source IP.
3. Verify SPF/DKIM/DMARC using trusted receiving results and associated DNS records; check From alignment.
4. Assess sender domain context, message intent, defanged URL and any attachments with approved tooling.
5. Determine whether the user clicked or entered credentials; review identity/endpoint logs if warranted.
6. Record and escalate evidence-backed findings according to local SOC procedures.

## Conclusion

**Verdict for this synthetic exercise:** Highly suspicious **simulated** credential-phishing example based on account-verification pressure, a different Reply-To domain, a login-themed defanged link, and *claimed* authentication problems. **No real email authentication, sender IP, delivery path, DNS, link reputation or compromise has been verified.**

This is a documented header interpretation exercise, not proof of a real attack.
