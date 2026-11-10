# Security Incident Report: Brute-Force Login Detection & Credential Compromise

## Incident Overview
- **Incident ID:** INC-2026-001
- **Date/Time of Detection:** 2026-11-09T09:02:00Z
- **Incident Severity:** High
- **Detection Mechanism:** Splunk SIEM (Custom Brute-Force Detection SPL Query)
- **Status:** Resolved / Simulated Lab Exercise

---

## Executive Summary
A high-severity security alert was triggered in the Splunk SIEM environment due to an anomalous spike in failed authentication attempts targeting the privileged `admin` user account. Forensic investigation confirmed a classic brute-force password-guessing attack originating from an external source IP address, which successfully culminated in an unauthorized login event.

---

## Indicators of Compromise (IoCs)
- **Attacker Source IP:** `198.51.100.24` (RFC 5737 Reserved Documentation Network)
- **Target User Account:** `admin`
- **Attack Vector:** Web / Administrative Login Brute-Force
- **Total Failed Attempts:** 6 consecutive failures
- **Final Authentication State:** Successful login (`status=success`) immediately following the brute-force sequence

---

## Detailed Timeline of Events
- **2026-11-09T09:00:00 - 09:00:50:** Six consecutive failed login attempts recorded for user `admin` originating from external source IP `198.51.100.24`.
- **2026-11-09T09:01:00:** A successful login event (`status=success`) was logged for user `admin` from the identical source IP (`198.51.100.24`), exactly 10 seconds post-failure.
- **2026-11-09T09:05:00 - 09:10:00:** Secondary benign authentication traffic observed from an unrelated IP (`203.0.113.50`) for users `john` and `alice`.

---

## Impact Assessment
- **Confidentiality & Integrity:** High risk of unauthorized access to the `admin` account due to successful post-brute-force authentication.
- **Scope:** Restricted to the simulated authentication service logs ingested into the local Splunk lab environment (`auth.log`).

---

## Remediation & Mitigation Steps
1. **Perimeter Defense:** Blacklist source IP `198.51.100.24` at the enterprise firewall and Web Application Firewall (WAF).
2. **Account Remediation:** Immediately revoke all active sessions for the `admin` account and enforce a mandatory credential reset.
3. **Security Controls Enhancement:** Implement Multi-Factor Authentication (MFA) for all privileged administrative accounts to render credential brute-force attempts ineffective.
4. **Ongoing Monitoring:** Maintain the active Splunk alert configuration to ensure real-time notification should similar failure thresholds (>3 attempts) occur in the future.
