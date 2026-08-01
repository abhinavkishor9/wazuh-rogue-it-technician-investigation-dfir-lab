# Investigation Notes

## Lab Summary

This investigation focused on analyzing suspicious administrator activity using native Windows Security logs and Wazuh Discover.

The investigation reconstructed password reset and account deletion activity while identifying how Windows audit policy affected Security event generation.

---

## Analyst Methodology

1. Verify Wazuh agent connectivity.
2. Simulate administrative account activity.
3. Review Windows Security logs.
4. Validate events using Event Viewer.
5. Verify events using PowerShell.
6. Review Windows audit policy.
7. Investigate Wazuh Discover.
8. Correlate evidence.
9. Document findings.

---

## Investigation Scenario

A temporary user account was managed by a simulated rogue IT technician.

The investigation aimed to determine:

- Whether account-management events were generated.
- Which administrative actions occurred.
- Whether Wazuh collected the activity.
- Whether Windows audit policy affected the investigation.

---

## Evidence Collected

### Evidence 1 – Password Reset

Collected:

- Event ID 4724

Finding:

Confirmed password reset activity in Event Viewer.

---

### Evidence 2 – User Account Deletion

Collected:

- Event ID 4726

Finding:

Confirmed successful account deletion.

---

### Evidence 3 – PowerShell Validation

Command Used

```powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4724,4726
}
```

Finding:

Validated Security events independently of Event Viewer.

---

### Evidence 4 – Wazuh Discover

Collected:

- Event ID 4726

Finding:

Confirmed successful SIEM collection of the account deletion event.

---

### Evidence 5 – Audit Policy

Collected:

- User Account Management audit configuration

Finding:

Initial investigation revealed auditing was disabled, explaining why several expected Security events were missing.

---

## DFIR Analysis

The investigation demonstrated that Windows Security event generation depends on audit policy configuration. Event IDs 4724 and 4726 provided sufficient evidence to reconstruct administrator activity, while reviewing AuditPol explained why additional account-management events were not initially available.

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Persistence | Create Account | T1136.001 |
| Privilege Escalation | Account Manipulation | T1098 |

---

## Analyst Observations

- Audit policy should always be verified during DFIR investigations.
- Event Viewer remains the authoritative Windows evidence source.
- PowerShell provides quick event validation.
- Wazuh successfully collected Event ID 4726.
- Endpoint validation should precede SIEM troubleshooting.

---

## Conclusion

This investigation demonstrated how suspicious administrator activity can be reconstructed using Windows Security logs and Wazuh Discover while highlighting the importance of audit policy verification during forensic investigations.
