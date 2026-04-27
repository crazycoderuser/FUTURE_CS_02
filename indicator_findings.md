# Phishing Indicator Findings

**Project:** Phishing Email Detection & Awareness System — Task 2  
**Scope:** Three email samples analyzed across four indicator categories  
**Date:** April 2025

---

## Indicator Categories

All indicators are classified under one of four categories:

- **Sender & Domain** — issues with the originating email address or domain
- **Content & Language** — psychological manipulation tactics in the email body
- **Link & URL** — suspicious or malicious links embedded in the email
- **Metadata** — anomalies in headers, send time, or routing

---

## Sample 01 — Full Indicator Breakdown

**Classification:** PHISHING | **Score:** 14 points

| # | Indicator | Category | Weight | Detail |
|---|-----------|----------|--------|--------|
| 1 | Spoofed sender domain | Sender & Domain | HIGH (+3) | `secure-account-verify.com` has no affiliation with any legitimate institution. Registered 4 days before send date. |
| 2 | SPF: FAIL | Sender & Domain | HIGH (+3) | Originating server (45.33.32.156, Eastern Europe) is not an authorized sender for this domain. |
| 3 | DKIM: FAIL | Sender & Domain | HIGH (+3) | No valid cryptographic signature. Email authenticity cannot be verified. |
| 4 | Malicious HTTP link | Link & URL | HIGH (+3) | `http://secure-account-verify.com/login` uses HTTP, belongs to a fake domain, and requests credentials. |
| 5 | Credential request | Content & Language | HIGH (+3) | "Verify your details immediately" — explicit credential harvesting attempt via external link. |
| 6 | Urgency language | Content & Language | MEDIUM (+2) | "Within 24 hours", "immediately" — artificial deadline to prevent verification. |
| 7 | Fear language | Content & Language | MEDIUM (+2) | "Permanent account lock", "suspicious activity" — designed to trigger panic. |
| 8 | Generic greeting | Content & Language | MEDIUM (+2) | "Dear User" — confirms mass campaign; sender does not know the target. |
| 9 | Vague threat | Content & Language | LOW (+1) | No specific transaction, date, or account details provided. |
| 10 | Unusual send time | Metadata | LOW (+1) | Sent at 02:14 AM — outside normal business hours. |

**Total: 14 points → PHISHING (override threshold: 8+ points)**

---

## Sample 02 — Full Indicator Breakdown

**Classification:** SUSPICIOUS | **Score:** 6 points

| # | Indicator | Category | Weight | Detail |
|---|-----------|----------|--------|--------|
| 1 | Brand domain spoofing | Sender & Domain | HIGH (+3) | `amazon-support-help.org` impersonates Amazon but is not `amazon.com`. |
| 2 | SPF: SOFTFAIL | Sender & Domain | MEDIUM (+2) | Sending server is not explicitly authorized but policy allows delivery. |
| 3 | Generic greeting | Content & Language | MEDIUM (+2) | "Dear Customer" — no registered name used. |
| 4 | Vague reason | Content & Language | LOW (+1) | "Verification issue" cited with no order number or date. |

**Total: 6 points → SUSPICIOUS (range: 4–7 points)**

---

## Sample 03 — Full Indicator Breakdown

**Classification:** LOW RISK | **Score:** 2 points

| # | Indicator | Category | Weight | Detail |
|---|-----------|----------|--------|--------|
| 1 | Generic greeting | Content & Language | LOW (+1) | "Hello there" — no registered name. |
| 2 | Mild urgency phrasing | Content & Language | LOW (+1) | "Limited time" — present but not fear-based or threatening. |

**Total: 2 points → LOW RISK (range: 0–3 points)**

---

## Cross-Sample Patterns

**Generic greetings appeared in all three samples.** The absence of a recipient's registered name is the most consistent single indicator across the sample set. It confirms that mass-sent campaigns do not have access to the target's account information.

**Authentication failures are definitive for Sample 01.** SPF, DKIM, and DMARC all fail on the highest-risk sample, providing technical confirmation that supplements the social engineering analysis.

**Risk scales directly with the number of combined tactics.** Sample 01 uses fear, urgency, authority, domain spoofing, and a credential-harvesting link simultaneously. The layering of tactics — not any single indicator — is what elevates it to a confirmed phishing classification.
