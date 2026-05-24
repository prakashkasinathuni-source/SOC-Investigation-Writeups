# Phishing Email Investigation

## Alert Description
A phishing alert was triggered after a user received an email containing a suspicious attachment. The attachment attempted to execute a malicious PowerShell command upon opening.

---

## Severity
High

---

## Detection Source
Microsoft Defender for Endpoint

---

## Investigation Steps

1. Reviewed the email headers and sender reputation.
2. Identified suspicious attachment named `Invoice_2025.docm`.
3. Analyzed PowerShell execution logs from the endpoint.
4. Checked outbound network connections initiated after document execution.
5. Queried SIEM for similar activity across other hosts.
6. Verified whether the user credentials were compromised.

---

## Logs Reviewed

- Microsoft Defender Alerts
- Windows Event Logs
- PowerShell Operational Logs
- Sysmon Logs
- Firewall Logs

---

## Indicators of Compromise (IOCs)

| Type | Value |
|------|------|
| IP Address | 185.225.69.104 |
| Domain | secure-login-check.com |
| File Hash | 3fa4f2d8abf2f9d11c7a |
| Filename | Invoice_2025.docm |

---

## PowerShell Command Observed

```powershell
powershell.exe -ExecutionPolicy Bypass -EncodedCommand SQBFAFgA
```

---

## MITRE ATT&CK Mapping

| Tactic | Technique |
|--------|-----------|
| Initial Access | Phishing (T1566) |
| Execution | PowerShell (T1059.001) |
| Command and Control | Application Layer Protocol (T1071) |

---

## Root Cause

The user opened a malicious macro-enabled document received through email. The document executed an obfuscated PowerShell command that attempted to download additional payloads from an external domain.

---

## Containment Actions

- Isolated affected endpoint
- Blocked malicious domain on firewall
- Removed phishing email from user mailbox
- Reset user credentials
- Initiated full antivirus scan

---

## Final Conclusion

The phishing attempt was successfully detected before lateral movement or privilege escalation occurred. No evidence of data exfiltration was identified during the investigation.

---

## Recommendations

- Enable attachment sandboxing
- Conduct phishing awareness training
- Block macro-enabled documents from external senders
- Improve PowerShell monitoring
- Enforce MFA for all users
