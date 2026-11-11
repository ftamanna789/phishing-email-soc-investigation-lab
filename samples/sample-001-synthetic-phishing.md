# Synthetic Phishing Email Sample 001

> Training-only fictional sample. Domains ending in `.invalid` are deliberately non-resolving. Authentication headers below are fabricated for analysis practice, not real verification results.

## Scenario
An employee reports an unexpected request to verify their Microsoft 365 account.

## Email (synthetic, redacted)
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

Your account will be disabled today unless you verify your details.
Visit: hxxps://account-verify[.]invalid/signin
Regards,
IT Helpdesk
```

## Analyst Tasks
1. Identify sender display-name and domain inconsistencies.
2. Interpret the *claimed* SPF, DKIM and DMARC results; explain why copied headers alone cannot independently prove them.
3. Defang and record the URL as an indicator without visiting it.
4. Assess urgency, credential-request pretext, and whether the message was expected.
5. Draft an evidence-based preliminary classification and recommended escalation.

**Do not submit this synthetic domain or URL to public reputation services as though it were a live threat.**
