# wazuh-rogue-it-technician-investigation-dfir-lab
## Overview

This Digital Forensics and Incident Response (DFIR) lab demonstrates how suspicious administrative activity can be investigated using native Windows Security logs and Wazuh.

Rather than relying on Sysmon, the investigation uses Windows Security Event Logs, Event Viewer, PowerShell, Audit Policy configuration, and Wazuh Discover to analyze administrator actions involving account management.

During the investigation, Windows generated Security Event IDs 4724 (password reset) and 4726 (user account deletion). The lab also demonstrates how Windows audit policy configuration directly affects event generation and forensic visibility.

---

# Executive Summary

This investigation focused on reconstructing suspicious administrator activity performed by a simulated rogue IT technician.

The investigation included:

- Creating a temporary user account
- Resetting the account password
- Deleting the account
- Investigating Windows Security events
- Validating events using Event Viewer
- Verifying events using PowerShell
- Investigating activity using Wazuh Discover
- Troubleshooting missing Security Event IDs by reviewing audit policy

The investigation emphasizes validating endpoint logging before assuming SIEM collection issues.

---

# Learning Objectives

- Understand Windows account management auditing.
- Investigate password reset activity.
- Investigate user account deletion.
- Validate Security logs using Event Viewer.
- Verify events using PowerShell.
- Investigate events using Wazuh Discover.
- Understand how audit policy affects event generation.
- Reconstruct administrative activity.

---

# Skills Demonstrated

- Windows DFIR Investigation
- Windows Security Log Analysis
- Account Management Investigation
- Event Viewer Analysis
- PowerShell Event Validation
- Audit Policy Troubleshooting
- Wazuh Discover Investigation
- Timeline Reconstruction
- Digital Evidence Documentation
- DFIR Troubleshooting
- MITRE ATT&CK Mapping

---

# Tools Used

- Wazuh Dashboard (Discover)
- Windows Event Viewer
- Windows PowerShell
- AuditPol
- Windows Security Event Log
- Wazuh Agent

---

# Lab Environment

| Component | Details |
|-----------|---------|
| SIEM | Wazuh 4.12 |
| Endpoint | Windows 11 Pro |
| Server | Oracle Linux 9 |
| Investigation Type | Windows DFIR |
| Event Source | Windows Security Log |
| Sysmon | Not Used |

---

# Investigation Scenario

A suspicious IT technician was suspected of abusing administrative privileges.

The objectives were to determine:

- Which account management actions occurred
- Which Windows Security events were generated
- Whether Wazuh collected the activity
- Why some expected Event IDs were missing
- How audit policy influenced the investigation

---

# Investigation Workflow

1. Verify Wazuh agent connectivity.
2. Simulate administrative account activity.
3. Review Windows Security logs.
4. Validate events using Event Viewer.
5. Verify activity using PowerShell.
6. Review Windows audit policy.
7. Investigate events using Wazuh Discover.
8. Correlate investigative findings.
9. Document evidence.

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Persistence | Create Account | T1136.001 |
| Privilege Escalation | Account Manipulation | T1098 |

### Why Rogue Administrator Investigations Matter

Unauthorized administrator actions such as password resets or account deletion may indicate insider abuse or attempts to conceal malicious activity. Correlating account-management events helps analysts reconstruct privileged user activity during incident response.

---

# Evidence Collected

- Windows Security Event Log
- Event Viewer
- PowerShell validation
- AuditPol configuration
- Wazuh Discover

---

# Evidence Correlation

| Evidence Source | Information Obtained | Investigation Value |
|-----------------|---------------------|--------------------|
| Event Viewer | Events 4724 & 4726 | Primary evidence |
| PowerShell | Event validation | Independent verification |
| AuditPol | Audit configuration | Troubleshooting |
| Wazuh Discover | Event 4726 | SIEM validation |

---

# Investigation Findings

- Windows generated Event ID 4724 during password reset.
- Windows generated Event ID 4726 during account deletion.
- Wazuh successfully collected Event ID 4726.
- Several expected account-management events were initially missing because User Account Management auditing was disabled.
- Enabling the appropriate audit policy improved forensic visibility.

---

# Key Takeaways

- Windows audit policy directly affects Security event generation.
- Event Viewer should always be used to validate endpoint logging.
- Wazuh can only collect events that Windows generates.
- Audit policy verification is an essential DFIR troubleshooting step.
- Multiple evidence sources improve investigation reliability.

---
