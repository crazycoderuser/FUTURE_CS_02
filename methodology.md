# Analysis Methodology

**Project:** Phishing Email Detection & Awareness System — Task 2

This document describes the end-to-end analysis methodology applied in this project. The seven-step process is modelled on real SOC (Security Operations Center) analyst workflows and is reproducible for any suspicious email.

---

## Step 1 — Sample Collection

Phishing email samples were sourced from publicly available educational resources and the task brief. Raw email text and headers were preserved verbatim as plain-text files to maintain evidence integrity. No sample contains real credentials, real personally identifiable information, or live malicious URLs.

**Sources consulted:**
- Task 2 brief (primary sample)
- PhishTank (https://www.phishtank.com) — community-verified phishing URL database
- OpenPhish (https://openphish.com) — active phishing feed

**Evidence preservation rule:** Every sample is stored exactly as received, with analyst notes appended in a clearly separated section. The original email content is never modified.

---

## Step 2 — First-Pass Manual Review

Before using any tools, each email was read manually to record first impressions. This trains the analyst's instincts and documents the psychological impact of the email as a non-technical user would experience it.

Questions answered at this stage: Who does this email claim to be from? What is it asking me to do? What emotion is it trying to trigger? Does anything feel wrong?

---

## Step 3 — Email Header Analysis

Full email headers were extracted and submitted to Google's Message Header Analyzer and MXToolbox. The analysis examined the `Received:` chain (read bottom-up to trace origin), `X-Originating-IP:`, `Return-Path:`, `Reply-To:`, and the `Authentication-Results:` block.

SPF, DKIM, and DMARC results were recorded and interpreted against the reference guide in `evidence/header-analysis/spf_dkim_dmarc_reference.md`.

---

## Step 4 — Sender Domain & URL Inspection

Each sender domain and every URL embedded in the email body was inspected using WHOIS (registration age), VirusTotal, URLVoid, and URLHaus. No URLs were visited directly. All checks were performed through passive analysis and reputation APIs.

Domain inspection criteria: registration age under 30 days, domain does not match claimed brand, use of typosquatting or subdomain tricks, IP address geolocation inconsistency.

URL inspection criteria: HTTP vs HTTPS, domain mismatch, URL shortener usage, excessive hyphens, IP address in URL, presence in known malicious URL databases.

---

## Step 5 — Indicator Identification and Classification

All detected anomalies were catalogued under four categories: Sender & Domain, Content & Language, Link & URL, and Metadata. Each indicator was assigned a risk weight: HIGH (+3 points), MEDIUM (+2 points), or LOW (+1 point).

The complete indicator list for each sample is documented in `analysis/indicator_findings.md`.

---

## Step 6 — Risk Scoring and Classification

The point totals from Step 5 were applied to the classification thresholds: 0–3 = Low Risk, 4–7 = Suspicious, 8+ = Phishing. The override rule was checked separately: any confirmed malicious payload or credential-harvesting link automatically forces a Phishing classification.

Results are documented in `analysis/risk_classification.md`.

---

## Step 7 — Report Generation

All findings were compiled into a client-ready PDF awareness report using Python and ReportLab. The report is structured for two audiences: security analysts (detailed indicator tables and scoring breakdowns) and non-technical employees (plain-language attack explanation, prevention tips, and Do's & Don'ts reference card).

The report is available at `report/Phishing_Awareness_Report.pdf`.

---

## Reproducibility

Any analyst can reproduce this methodology on a new email sample by following these steps in sequence, using the tools listed in `docs/tools_reference.md`, and applying the indicator weights and classification thresholds documented in `analysis/risk_classification.md`.
