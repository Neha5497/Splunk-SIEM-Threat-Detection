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
