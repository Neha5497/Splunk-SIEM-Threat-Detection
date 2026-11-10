# SOC Investigation Methodology & Process

## Overview
This document outlines the step-by-step forensic process and methodology used by the Security Operations Center (SOC) analyst to investigate, triage, and validate the simulated brute-force attack discovered through Splunk SIEM log monitoring.

---

Step 1: Alert Triage & Initial Detection
- **Trigger Source:** A custom Splunk detection rule flagged an anomalous volume of failed login attempts exceeding the predefined threshold of 3 failures.
- **Initial Finding:** The query isolated external source IP `198.51.100.24` targeting the privileged `admin` user account with multiple continuous authentication failures within a short 1-minute time window (`2026-11-09T09:00:00` to `09:00:50`).

---

Step 2: Source IP & Scope Isolation
- **Analyst Action:** Investigated the offending IP address (`198.51.100.24`) to evaluate its broader activity profile across the authentication logs.
- **SPL Query Used:**
  ```spl
  src_ip="198.51.100.24" 
  | table timestamp user src_ip action status

Observation: Confirmed that the source IP was external and focused strictly on high-privilege administrative accounts (admin), indicating targeted credential harvesting rather than broad, indiscriminate network scanning.

Step 3: Success-After-Failure Post-Exploitation Analysis
Analyst Action: Pivoted to examine the timeline immediately following the failed attempts to determine whether the brute-force attack successfully bypassed authentication.

Findings: A successful login event (status=success) was logged for user admin originating from the exact same source IP (198.51.100.24) at 09:01:00—precisely 10 seconds after the final brute-force failure.

Conclusion: This "success-after-failure" sequence serves as a high-confidence Indicator of Compromise (IoC), confirming that the brute-force password guessing successfully compromised the administrative credential.

Step 4: Containment, Escalation & Remediation Recommendations
Perimeter IP Blocking: Immediately block source IP 198.51.100.24 at the firewall and Web Application Firewall (WAF) layer.

Credential Revocation: Invalidate all active user sessions for the compromised admin account and trigger an immediate forced password reset.

Security Control Enhancement: Enforce mandatory Multi-Factor Authentication (MFA) across all administrative access points to render automated brute-force attempts ineffective.

SIEM Monitoring: Keep the Splunk brute-force detection alert active for real-time visibility into any future threshold violations.
