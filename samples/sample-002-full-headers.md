# Sample 002 — Full Header Analysis Training Email

**FICTIONAL TRAINING DATA ONLY.** Every domain ends in reserved `.invalid`, and the IP `192.0.2.44` is a documentation-only TEST-NET address. These headers, SPF/DKIM results, and timestamps were invented; they were **not** received by a real mail server or cryptographically verified.

## Scenario
A message claims to be from a corporate IT helpdesk, but its sending infrastructure authenticates a different domain. The recipient is asked to verify an account using a fictional, defanged link.

```text
Return-Path: <bounce@notices.attacker.invalid>
Delivered-To: employee@company.invalid
Received: from mail.notices.attacker.invalid (mail.notices.attacker.invalid [192.0.2.44])
    by mx.company.invalid with ESMTP id LAB002;
    Wed, 11 Nov 2026 10:05:04 +0000
Authentication-Results: mx.company.invalid;
    spf=pass smtp.mailfrom=notices.attacker.invalid;
    dkim=pass header.d=notices.attacker.invalid;
    dmarc=fail header.from=company.invalid
Received-SPF: pass (simulated) client-ip=192.0.2.44;
    envelope-from=bounce@notices.attacker.invalid
DKIM-Signature: v=1; a=rsa-sha256; d=notices.attacker.invalid;
    s=training; h=from:to:subject:date; bh=SIMULATED-NOT-REAL;
    b=SIMULATED-NOT-REAL
From: "Company IT Helpdesk" <helpdesk@company.invalid>
Reply-To: helpdesk@notices.attacker.invalid
To: employee@company.invalid
Date: Wed, 11 Nov 2026 10:05:00 +0000
Message-ID: <sample-002@notices.attacker.invalid>
Subject: Action required: revalidate your mailbox

Your mailbox needs revalidation today to prevent disruption.
Visit: hxxps://mailbox-check[.]invalid/login
```

## Analyst Questions
1. What is the *visible* From domain? How does it differ from the Return-Path?
2. What does `spf=pass` actually authenticate?
3. Why might `dkim=pass` and `dmarc=fail` appear together?
4. What does `Received` suggest about a sending host, and why can't its source IP be verified here?
5. Identify the social-engineering clues. Is there evidence of a real user clicking?

**Safety:** Do not navigate to the defanged URL or report any of these invented IOCs as a live threat.
