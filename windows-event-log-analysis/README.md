# Windows Authentication Event Investigation

## Objective
Investigate Windows authentication activity using Windows Security Event Logs and PowerShell.

The goal was to identify successful logons, interpret logon types, distinguish Subject from New Logon, examine associated processes, and determine whether activity appeared local or remote.

## Environment

- Windows workstation
- Administrator PowerShell
- Windows Security Event Log
- Get-WinEvent

## Commands Used

```powershell
Get-WinEvent -LogName Security -MaxEvents 20
```

```powershell
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4624} -MaxEvents 10
```

## Finding 1: Service Logon

- Event ID: 4624
- Logon Type: 5
- New Logon account: SYSTEM
- Process: C:\Windows\System32\services.exe
- Source Network Address: not reported

### Analysis
Logon Type 5 represents a service logon. SYSTEM together with services.exe was consistent with expected Windows service activity.

## Finding 2: Interactive Session

- Event ID: 4624
- Logon Type: 2
- New Logon account: DWM-1
- Account Domain: Window Manager
- Process: C:\Windows\System32\winlogon.exe
- Source Network Address: not reported

### Analysis
Logon Type 2 represents an interactive logon. This event also demonstrated the difference between the Subject and New Logon fields.

Subject identifies the security context requesting the action. New Logon identifies the account receiving the new session.

## Finding 3: Workstation Unlock

- Event ID: 4624
- Logon Type: 7
- Account Domain: MicrosoftAccount
- Account Name: [REDACTED]
- Process: C:\Windows\System32\lsass.exe
- Source Network Address: not reported
- Elevated Token: No

### Analysis
Logon Type 7 represents a workstation unlock. No remote source network address was reported, supporting the conclusion that this was normal local workstation activity.

## Key Takeaways

- Event ID 4624 means a successful Windows logon.
- Logon Type 2 indicates an interactive logon.
- Logon Type 5 indicates a service logon.
- Logon Type 7 indicates a workstation unlock.
- The New Logon section identifies the account that received the session.
- Source Network Address can help determine whether authentication originated remotely.

## Outcome

This lab provided hands-on experience investigating Windows authentication activity using PowerShell and Windows Security Event Logs.

The investigation identified normal service activity, interactive session activity, and a workstation unlock event.

## Future Expansion

- Event ID 4625 failed logons
- Remote authentication analysis
- Account lockout investigation
- Privileged logon events
- SIEM ingestion and alert analysis
