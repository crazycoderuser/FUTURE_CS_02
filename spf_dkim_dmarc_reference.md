# SPF, DKIM & DMARC — Analyst Reference Guide

A quick-reference guide for interpreting email authentication results during phishing analysis.

---

## SPF (Sender Policy Framework)

**What it does:** Verifies that the email was sent from a server that the domain owner has authorized.

**How to read the result:**

| Result | Meaning | Risk |
|--------|---------|------|
| `pass` | Server is authorized. Email is likely legitimate. | Low |
| `softfail` | Server is not listed but domain policy allows delivery. Treat as suspicious. | Medium |
| `fail` | Server is explicitly unauthorized. Strong phishing indicator. | High |
| `none` | Domain has no SPF record published. Cannot verify. | Medium |
| `neutral` | Domain owner makes no assertion either way. | Low-Medium |
| `temperror` | Temporary DNS error — retry may resolve. | Low |
| `permerror` | Permanent configuration error in the SPF record. | Medium |

---

## DKIM (DomainKeys Identified Mail)

**What it does:** Uses a cryptographic signature to verify that the email content has not been altered in transit and that it was authorized by the domain owner.

**How to read the result:**

| Result | Meaning | Risk |
|--------|---------|------|
| `pass` | Signature is valid. Email content is unaltered and authorized. | Low |
| `fail` | Signature is invalid or absent. Email may be forged or tampered with. | High |
| `none` | No DKIM signature present. Cannot verify. | Medium |
| `policy` | Signature is valid but domain policy prohibits it. | Medium |
| `neutral` | Signature present but not verifiable. | Medium |

**Important:** A DKIM pass for a spoofed domain (e.g., `amazon-support-help.org` signing its own email) only confirms that *that domain* signed the message — it does not confirm the email is from Amazon.

---

## DMARC (Domain-based Message Authentication, Reporting & Conformance)

**What it does:** Tells receiving mail servers what to do when SPF or DKIM checks fail, and specifies reporting requirements.

**Policy values:**

| Policy | Action on Failure | Notes |
|--------|------------------|-------|
| `p=none` | Deliver the email, log the failure only. | Weakest — commonly seen in early deployments |
| `p=quarantine` | Move to spam/junk folder. | Moderate protection |
| `p=reject` | Reject the email outright. | Strongest — recommended for all organizations |

**How to read a DMARC fail:** A DMARC fail means SPF and/or DKIM failed and the domain's authentication policy was violated. Even with `p=none`, a DMARC fail is a confirmed phishing indicator.

---

## Quick Decision Guide

When analyzing a suspicious email, check authentication results in this order:

1. If **SPF=fail AND DKIM=fail AND DMARC=fail** → almost certainly phishing. Classify as HIGH risk.
2. If **SPF=softfail OR DKIM=none** → suspicious. Check all other indicators before classifying.
3. If **SPF=pass AND DKIM=pass AND DMARC=pass** → authentication is valid. Focus indicator analysis on content and links.
4. **Always remember:** authentication passing for a spoofed domain (e.g., paypal-verify.com) means nothing — the domain itself is the threat.
