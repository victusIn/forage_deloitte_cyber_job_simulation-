# forage_deloitte_cyber_job_simulation-
Forensic Log Analysis &amp; Incident Response - Deloitte Cybersecurity Virtual Experience  An investigation into a simulated data breach at Daikibo Industrials. This project involved analyzing web server logs to identify automated data exfiltration (telemetry scraping) and evaluating intranet network architecture to determine attack vectors.
# Daikibo Industrials: Cyber Security Breach Investigation

## 📌 Project Overview
As part of the Deloitte Australia Cybersecurity Virtual Experience, I acted as a consultant to investigate a potential data breach at Daikibo Industrials. A news outlet leaked sensitive production data, and the client suspected their new assembly line status dashboard was the source.

## 🔍 Investigation Phase 1: Network Architecture
**Finding:** A direct external attack via the public internet was deemed impossible.

**Technical Reasoning:**
- The dashboard is hosted on a private **Intranet**.
- It is only accessible via **Static Internal IP addresses**.
- Conclusion: The dashboard is not "internet-facing." For an attacker to reach it, they would need existing access to the internal network (e.g., via VPN or a compromised internal workstation).



## 📊 Investigation Phase 2: Log Forensics
I performed a forensic audit of the `web_requests.log` file. The dashboard architecture does not support auto-refreshing; users must manually request updates.

### Identified Threat Actor
- **Suspicious User ID:** `mdB7yD2dp1BFZPontHBQ1Z`
- **Indicator of Compromise (IoC):** Robotic, scheduled API polling.

### The "Smoking Gun"
The logs showed this specific User ID making `GET /api/v1/status` requests at **exact hourly intervals**:
- **Timestamp:** 10:00:00
- **Timestamp:** 11:00:00
- **Timestamp:** 12:00:00



**Analysis:** This precision is impossible for a human user. It confirms the presence of a **telemetry scraper** (a script/cron job) running on an internal device to systematically exfiltrate production data.

## 🛠️ Skills Demonstrated
- **Log Analysis:** Sifting through raw web logs to identify non-human traffic patterns.
- **Incident Response:** Isolating a specific User ID as the source of a breach.
- **Strategic Communication:** Drafting executive summaries for non-technical stakeholders.
- **Network Security:** Understanding the implications of intranet-hosted services and static IP configurations.

## 🏁 Conclusion
The investigation successfully shifted the focus from an "external hack" to an **internal automated exfiltration event**. The identified User ID has been recommended for immediate revocation and the associated workstation flagged for forensic imaging.
