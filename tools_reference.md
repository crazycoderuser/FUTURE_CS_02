# Tools Reference Guide

**Project:** Phishing Email Detection & Awareness System — Task 2

All tools used in this analysis are free, publicly accessible, and require no account registration unless noted. No malicious URLs were visited directly during the analysis process.

---

## Email Header Analysis

### Google Admin Toolbox — Message Header Analyzer
- **URL:** https://toolbox.googleapps.com/apps/messageheader/
- **How to use:** Paste the full raw email header (copy from your email client via "Show original" or "View source") into the text area and click Analyze. The tool visualizes the Received chain, delivery timeline, and flags any delays or anomalies.
- **Best for:** Tracing the email's routing path from origin to delivery.

### MXToolbox Email Header Analyzer
- **URL:** https://mxtoolbox.com/EmailHeaders.aspx
- **How to use:** Paste the raw header and submit. MXToolbox parses SPF, DKIM, and DMARC authentication results clearly and highlights any failures.
- **Best for:** Authentication result verification (SPF / DKIM / DMARC).

---

## Domain & URL Inspection

### VirusTotal
- **URL:** https://www.virustotal.com
- **How to use:** Paste a URL, domain, or IP address into the search bar. VirusTotal checks it against 70+ security engine databases and returns a verdict. Never paste a URL you intend to visit.
- **Best for:** Checking whether a URL or domain has been flagged as malicious by any security vendor.

### URLVoid
- **URL:** https://www.urlvoid.com
- **How to use:** Enter the domain name (without http://) and submit. URLVoid checks against 25+ blacklists and shows domain reputation, first seen date, and hosting country.
- **Best for:** Domain reputation scoring and blacklist verification.

### URLHaus (abuse.ch)
- **URL:** https://urlhaus.abuse.ch
- **API endpoint:** https://urlhaus-api.abuse.ch/v1/url/
- **How to use:** Search by URL or domain on the website, or query the API by submitting a POST request with the URL parameter. Returns known malware hosting and payload information.
- **Best for:** Checking whether a URL is associated with a known malware distribution campaign.

### WHOIS Lookup
- **URL:** https://whois.domaintools.com
- **How to use:** Enter the domain name and submit. The result shows registration date, registrar, registrant country, and hosting provider. Domains registered within 30 days of the suspected email send date should be treated as HIGH risk.
- **Best for:** Checking domain age — a strong indicator of phishing infrastructure.

---

## Report Generation

### Python 3.11
- **Purpose:** Scripting the analysis pipeline and automating PDF report generation.
- **Install:** https://www.python.org/downloads/

### ReportLab (Python library)
- **Purpose:** Generating professional, multi-section PDF reports programmatically.
- **Install:** `pip install reportlab`
- **Documentation:** https://docs.reportlab.com

---

## How to Access Email Headers

| Email Client | Steps |
|-------------|-------|
| Gmail | Open email → Three dots (⋮) menu → "Show original" → Copy header block |
| Outlook (web) | Open email → Three dots → "View message source" |
| Outlook (desktop) | File → Properties → "Internet headers" box |
| Apple Mail | View → Message → "All Headers" |
| Thunderbird | View → "Message Source" (Ctrl+U) |
