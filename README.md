
# Phishing Email Detection & Awareness System
### Cybersecurity Internship — Task 2

![Security](https://img.shields.io/badge/Domain-Email%20Security-blue?style=flat-square)
![Task](https://img.shields.io/badge/Task-2%20%7C%20Phishing%20Detection-red?style=flat-square)
![Status](https://img.shields.io/badge/Status-Complete-green?style=flat-square)
![Python](https://img.shields.io/badge/Python-3.11%2B-yellow?style=flat-square)

---

## Overview

This repository documents the complete analysis, methodology, evidence, and reporting output for **Task 2** of the Cybersecurity Internship Program — a hands-on phishing email detection and awareness project. The work is structured exactly as a real Security Operations Center (SOC) analyst would approach it: collecting evidence, analyzing headers and indicators, classifying risk, and producing a client-ready awareness report.

> **Important:** All email samples in this repository are synthetic or publicly documented phishing examples used for educational purposes only. No real user data is included. No malicious URLs were visited or interacted with during this analysis.

---

## Repository Structure

```
phishing-detection-task2/
│
├── README.md
│
├── evidence/
│   ├── sample-emails/
│   │   ├── sample_01_high_risk.txt
│   │   ├── sample_02_medium_risk.txt
│   │   ├── sample_03_low_risk.txt
│   │   └── sample_emails_metadata.json
│   └── header-analysis/
│       ├── header_sample_01.txt
│       ├── header_analysis_notes.md
│       └── spf_dkim_dmarc_reference.md
│
├── analysis/
│   ├── indicator_findings.md
│   ├── risk_classification.md
│   └── url_domain_inspection.md
│
├── report/
│   └── Phishing_Awareness_Report.pdf
│
└── docs/
    ├── tools_reference.md
    └── methodology.md
```

---

## Tools Used

### Email Header Analysis

| Tool | Purpose | URL |
|------|---------|-----|
| Google Admin Toolbox — Message Header Analyzer | Parse email headers, trace routing hops, verify delivery timeline | https://toolbox.googleapps.com/apps/messageheader/ |
| MXToolbox Email Header Analyzer | SPF, DKIM, DMARC authentication result verification | https://mxtoolbox.com/EmailHeaders.aspx |

### Domain & URL Inspection

| Tool | Purpose | URL |
|------|---------|-----|
| VirusTotal | Check URLs and domains against 70+ security engine databases | https://www.virustotal.com |
| URLVoid | Domain reputation, registration age, blacklist status | https://www.urlvoid.com |
| URLHaus (abuse.ch) | Known malicious URL and payload database lookup | https://urlhaus.abuse.ch |
| WHOIS Lookup | Domain registration date, registrant info, hosting provider | https://whois.domaintools.com |

### Report Generation

| Tool | Purpose |
|------|---------|
| Python 3.11 | Analysis scripting and automation |
| ReportLab | Professional multi-section PDF report generation |

---

## Analysis Approach

The analysis follows a structured seven-step methodology modelled on real SOC analyst workflows.

**Step 1 — Sample Collection.** Three phishing email samples were collected covering a range of risk levels: one confirmed high-risk credential-harvesting attack, one medium-risk suspicious email with an unverified sender domain, and one low-risk borderline spam message. Raw email text and headers are preserved as plain-text files in `evidence/sample-emails/`.

**Step 2 — Email Header Parsing.** Full email headers were extracted and analyzed using Google's Message Header Analyzer and MXToolbox. Key fields examined included the `Received:` routing chain, `Return-Path:`, `Reply-To:`, `Message-ID:`, `X-Originating-IP:`, and the `Authentication-Results:` block for SPF, DKIM, and DMARC outcomes.

**Step 3 — Sender Domain & URL Inspection.** Each sender domain was inspected for typosquatting, subdomain spoofing, and registration age via WHOIS. All URLs in each email body were extracted, checked for HTTPS usage, compared against the claimed sender brand, and verified against VirusTotal and URLHaus.

**Step 4 — Phishing Indicator Identification.** Indicators were categorized into four groups — Sender & Domain, Email Content & Language, Link & URL, and Attachment — with each indicator documented alongside its severity weight (HIGH / MEDIUM / LOW) and a plain-language explanation.

**Step 5 — Risk Classification.** A point-based scoring system was applied. HIGH indicators contribute +3 points, MEDIUM +2, and LOW +1. Thresholds: 0–3 = Safe, 4–7 = Suspicious, 8+ = Phishing. An override rule forces a Phishing classification whenever a confirmed malicious payload or active credential-harvesting link is detected, regardless of the total score.

**Step 6 — Findings Documentation.** All indicator findings, scoring breakdowns, and classification verdicts were compiled into structured markdown files within the `analysis/` directory for technical review.

**Step 7 — Awareness Report Generation.** A client-ready PDF report was generated covering the threat overview, full indicator analysis, risk classification, plain-language attack explanation, prevention tips, and an employee Do's & Don'ts reference card.

---

## Risk Classification Summary

| Sample | Subject | Risk Level | Score | Key Indicators |
|--------|---------|-----------|-------|---------------|
| Sample 01 | Urgent: Your Account Will Be Locked | 🔴 PHISHING | 14 pts | Spoofed domain, malicious HTTP link, credential request, urgency + fear language |
| Sample 02 | Your Amazon Order Has Been Delayed | 🟡 SUSPICIOUS | 6 pts | Suspicious sender domain, generic greeting, unverified link destination |
| Sample 03 | Exclusive Offer For You | 🟢 LOW RISK | 2 pts | Generic offer language, no confirmed malicious link |

---

## Key Findings

**Social engineering dominates over technical sophistication.** All three samples relied primarily on psychological manipulation — fear, urgency, and authority — rather than malware or technical exploits. The human layer remains the primary attack surface.

**Domain spoofing is the primary deception vector.** The high-risk sample used a purpose-registered domain (`secure-account-verify.com`) designed to appear legitimate at a glance. It was registered within 30 days of the email being sent, carried no SPF record, and failed DKIM authentication entirely.

**HTTP links are a definitive red flag.** The malicious link in Sample 01 used HTTP rather than HTTPS. No legitimate financial institution delivers login pages over an unencrypted connection; this single indicator alone is sufficient grounds for a Suspicious classification.

**Generic greetings indicate mass campaigns.** All three samples used generic salutations — "Dear User", "Dear Customer" — rather than the recipient's registered name, confirming that the attacker had no knowledge of the individual target.

---

## Prevention Recommendations

Three controls would have the highest practical impact for any organisation:

1. **DMARC enforcement** — publishing `p=reject` at the domain level prevents attackers from spoofing your domain to target your own employees and customers.
2. **Employee phishing simulation training** — regular simulated phishing campaigns are the single most effective method for building human-layer resistance.
3. **Multi-Factor Authentication on all accounts** — even if credentials are successfully harvested via phishing, MFA blocks the attacker from exploiting them.

---

## How to Use This Repository

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/phishing-detection-task2.git
cd phishing-detection-task2

# Review the sample emails
cat evidence/sample-emails/sample_01_high_risk.txt

# Read the full indicator analysis
cat analysis/indicator_findings.md

# Open the awareness report
open report/Phishing_Awareness_Report.pdf
```

---

## Disclaimer

All phishing email samples in this repository are synthetic examples created for educational purposes. No real credentials, personally identifiable information, or live malicious URLs are present. This project is security education — not security exploitation.

---

## Author

**Cybersecurity Internship — Task 2**
Domain: Email Security / Threat Analysis
Program: Future Interns Cybersecurity Internship
