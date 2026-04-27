# URL & Domain Inspection Notes

**Project:** Phishing Email Detection & Awareness System — Task 2  
**Tools used:** VirusTotal, URLVoid, WHOIS, URLHaus  
**Date:** April 2025

> **Safety note:** No URLs below were visited directly. All checks were performed through reputation APIs and passive analysis tools only.

---

## Sample 01 — URL Analysis

**URL found:** `http://secure-account-verify.com/login`

| Check | Finding | Risk |
|-------|---------|------|
| Protocol | HTTP (not HTTPS) | HIGH — no encryption, no certificate |
| Domain vs claimed brand | No match — not affiliated with any known institution | HIGH |
| Domain age (WHOIS) | Registered 4 days before email send date | HIGH |
| URLVoid reputation | Flagged by 3/25 security engines | HIGH |
| URLHaus lookup | Not in database (too new) — treated as unknown/suspicious | MEDIUM |
| Hyphens in domain | 2 hyphens — borderline suspicious | LOW |
| IP resolution | 45.33.32.156 — Eastern Europe hosting provider | MEDIUM |

**Verdict:** Confirmed malicious. Do not visit under any circumstances.

---

## Sample 02 — URL Analysis

**URL found:** `http://amazon-support-help.org/verify-address`

| Check | Finding | Risk |
|-------|---------|------|
| Protocol | HTTP (not HTTPS) | HIGH — no encryption |
| Domain vs claimed brand | Does not match amazon.com — uses hyphenated variant | HIGH |
| Domain age (WHOIS) | Registered 12 days before email send date | HIGH |
| URLVoid reputation | Not flagged (too new for blacklists) | LOW |
| URLHaus lookup | Not in database | LOW |

**Verdict:** Suspicious. Domain impersonates Amazon but is not Amazon. Link should not be clicked; order status should be verified directly at amazon.com.

---

## Sample 03 — URL Analysis

**URL found:** `https://deals-newsletter.com/offer`

| Check | Finding | Risk |
|-------|---------|------|
| Protocol | HTTPS | LOW — certificate present |
| Domain vs claimed brand | Matches sender domain — consistent | LOW |
| Domain age (WHOIS) | Registered 2 years ago | LOW |
| URLVoid reputation | Not flagged | LOW |
| URLHaus lookup | Not in database | LOW |

**Verdict:** No malicious indicators detected. Link appears to belong to a legitimate (if unsolicited) marketing sender.

---

## Domain Inspection Methodology

For each sender domain identified, the following checks were performed in sequence:

1. **WHOIS lookup** — confirm registration date, registrant country, and hosting provider. Domains registered within 30 days of the email send date are flagged as HIGH risk.
2. **VirusTotal domain check** — submit the domain (not the full URL) to check against security engine databases.
3. **URLVoid** — check domain reputation score and blacklist status across 25+ engines.
4. **URLHaus** — query the abuse.ch database for known malicious payloads associated with the domain.
5. **Manual inspection** — compare the domain name against the claimed sender brand for typosquatting, subdomain tricks, and homograph attacks.
