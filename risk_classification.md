# Risk Classification Results

**Project:** Phishing Email Detection & Awareness System — Task 2  
**Date:** April 2025

---

## Classification Framework

| Level | Score Range | Definition |
|-------|------------|------------|
| LOW RISK | 0–3 points | Mildly suspicious or spam. No confirmed malicious elements. Monitor. |
| SUSPICIOUS | 4–7 points | Multiple indicators present. Requires human review before any action. |
| PHISHING | 8+ points | Confirmed malicious. Do not interact. Report to IT security immediately. |

**Override rule:** Any email containing a confirmed malicious payload, known malicious URL, or active credential-harvesting link is classified as PHISHING regardless of point total.

---

## Results Summary

| Sample | Subject | Score | Classification | Override Applied |
|--------|---------|-------|---------------|-----------------|
| Sample 01 | Urgent: Your Account Will Be Locked | 14 pts | PHISHING | No (score sufficient) |
| Sample 02 | Your Amazon Order Has Been Delayed | 6 pts | SUSPICIOUS | No |
| Sample 03 | Exclusive Offer For You | 2 pts | LOW RISK | No |

---

## Scoring Detail

### Sample 01 — 14 Points

| Indicator Type | Count | Points Each | Subtotal |
|---------------|-------|-------------|---------|
| HIGH indicators | 5 | +3 | 15 |
| MEDIUM indicators | 3 | +2 | 6 |
| LOW indicators | 2 | +1 | 2 |

Note: Points are additive per indicator count, not per category — total reflects all individual detections.  
**Final score: 14 → PHISHING**

### Sample 02 — 6 Points

| Indicator Type | Count | Points Each | Subtotal |
|---------------|-------|-------------|---------|
| HIGH indicators | 1 | +3 | 3 |
| MEDIUM indicators | 2 | +2 | 4 |
| LOW indicators | 1 | +1 | 1 |

**Final score: 6 → SUSPICIOUS**

### Sample 03 — 2 Points

| Indicator Type | Count | Points Each | Subtotal |
|---------------|-------|-------------|---------|
| HIGH indicators | 0 | +3 | 0 |
| MEDIUM indicators | 0 | +2 | 0 |
| LOW indicators | 2 | +1 | 2 |

**Final score: 2 → LOW RISK**
