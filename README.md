# Mini-SOC Lab: SIEM Log Monitoring & Threat Detection with Splunk

A hands-on Security Operations Center (SOC) lab built to practice log ingestion, threat detection, incident investigation, and SIEM dashboard creation using Splunk.

---

## 🛠️ Project Architecture & Overview
This project simulates a real-world security incident inside an enterprise network, focusing on detecting, investigating, and reporting a **brute-force login attack** targeting administrative credentials.

* **Log Ingestion:** Authentication logs (`auth.log`) ingested and indexed via Splunk Enterprise.
* **Threat Detection:** Custom Search Processing Language (SPL) queries to flag anomalous authentication patterns.
* **Incident Investigation:** Forensic timeline reconstruction of a "success-after-failure" compromise indicator.
* **Dashboard & Alerting:** Real-time visibility panels tracking security metrics and brute-force indicators.

---

## 📂 Repository Structure
```text
Splunk-SIEM-Threat-Detection/
│
├── sample-logs/
│   └── auth.log
│
├── SPL-queries/
│   ├── brute-force-detection.spl
│   ├── ip-investigation.spl
│   └── dashboard-queries.spl
│
├── screenshots/
│   ├── brute-force detection.png
│   └── Dashboards.png
│   └── ip-investigation.png
│ 
├── reports/
│   ├── investigation-process.md
│   └── incident-report.md
│
└── README.md

---

## Quick Start / Lab Steps Completed:
1.Environment Setup: Configured a local project workspace and verified macOS architecture compatibility for Splunk.
2.Log Generation: Created synthetic authentication logs (sample-logs/auth.log) modeling normal and malicious user activity.
3.Log Ingestion: Uploaded and parsed authentication logs into Splunk Enterprise under the Search & Reporting.
4.Threat Detection: Built and executed SPL queries to isolate brute-force indicators (> 3 failed attempts).
5.Investigation: Performed forensic pivot analysis on suspicious IP 198.51.100.24.
6.Dashboard & Alerting: Configured real-time security alerts and a modular SOC dashboard (SOC Security Operations & Threat Monitoring).

---

## Sample Security Logs (sample-logs/auth.log)

timestamp=2026-11-09T09:00:00 user=admin src_ip=198.51.100.24 action=login status=failed
timestamp=2026-11-09T09:00:10 user=admin src_ip=198.51.100.24 action=login status=failed
timestamp=2026-11-09T09:00:20 user=admin src_ip=198.51.100.24 action=login status=failed
timestamp=2026-11-09T09:00:30 user=admin src_ip=198.51.100.24 action=login status=failed
timestamp=2026-11-09T09:00:40 user=admin src_ip=198.51.100.24 action=login status=failed
timestamp=2026-11-09T09:00:50 user=admin src_ip=198.51.100.24 action=login status=failed
timestamp=2026-11-09T09:01:00 user=admin src_ip=198.51.100.24 action=login status=success
timestamp=2026-11-09T09:05:00 user=john src_ip=203.0.113.50 action=login status=success
timestamp=2026-11-09T09:06:00 user=john src_ip=203.0.113.50 action=login status=failed
timestamp=2026-11-09T09:10:00 user=alice src_ip=203.0.113.50 action=login status=success

---

## Core SPL Threat Detection Queries (SPL-queries/)

1.Brute-Force Detection Query:
action=login status=failed 
| stats count by src_ip user 
| where count > 3 
| rename count as "Failed Attempts"

2.Suspicious IP Forensic Timeline:
src_ip="198.51.100.24" 
| table timestamp user src_ip action status

---

## Documentation & Reports

Detailed forensic investigation workflows can be found in reports/investigation-process.md

Full security incident write-ups are available in reports/incident-report.md


