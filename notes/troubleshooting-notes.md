# Troubleshooting Notes

## Issue 1 — Expected Account Management Events Missing

### Cause

User Account Management auditing was disabled.

### Resolution

Enable auditing using:

```cmd
auditpol /set /subcategory:"User Account Management" /success:enable
```

---

## Issue 2 — Local Group Events Not Generated

### Cause

Security Group Management auditing was not enabled.

### Resolution

Review and enable the appropriate audit policy if group membership events are required.

---

## Issue 3 — Event Appeared in Event Viewer but Not Wazuh

### Cause

Event forwarding delay or indexing latency.

### Resolution

Wait several minutes and search Discover using a wider time range.

---

## Issue 4 — Only Event ID 4726 Appeared in Wazuh

### Cause

Windows generated multiple events, but only Event ID 4726 was successfully collected during the investigation period.

### Resolution

Validate endpoint logs first, then confirm ingestion through Wazuh before assuming collection issues.

---

## Issue 5 — Verify Wazuh Agent Health

### Cause

Potential communication interruption.

### Resolution

Verify agent status:

```bash
sudo /var/ossec/bin/agent_control -i 001
```

---

# Lessons Learned

- Windows audit policy determines which Security events are generated.
- Wazuh cannot collect events that Windows does not produce.
- Event Viewer should always validate endpoint logging before SIEM troubleshooting.
- AuditPol is an essential DFIR troubleshooting tool.
- Correlating Event Viewer, PowerShell, AuditPol, and Wazuh provides a reliable investigation workflow.
