# Investigation Timeline

| Time | Activity | Evidence |
|------|----------|----------|
| 09:00 | Verified Wazuh agent connectivity | agent_control |
| 09:05 | Simulated administrator activity | Windows |
| 09:10 | Reviewed Windows Security log | Event Viewer |
| 09:15 | Observed Event ID 4724 | Password Reset |
| 09:20 | Observed Event ID 4726 | Account Deletion |
| 09:25 | Validated events using PowerShell | Get-WinEvent |
| 09:30 | Reviewed AuditPol configuration | auditpol |
| 09:35 | Enabled User Account Management auditing | auditpol |
| 09:40 | Investigated Wazuh Discover | Discover |
| 09:45 | Correlated findings | Documentation |

---

# Investigation Flow

Investigation Started

↓

Verified Agent Health

↓

Simulated Administrator Activity

↓

Reviewed Event Viewer

↓

Validated Using PowerShell

↓

Reviewed Audit Policy

↓

Investigated Wazuh Discover

↓

Correlated Evidence

↓

Investigation Completed

---

# Summary

The investigation reconstructed suspicious administrator activity using native Windows Security logs and Wazuh Discover. Windows generated Event IDs **4724** and **4726**, while Wazuh successfully collected **4726**. The investigation also demonstrated that Windows audit policy configuration directly influences Security event generation and should always be validated during DFIR investigations.
