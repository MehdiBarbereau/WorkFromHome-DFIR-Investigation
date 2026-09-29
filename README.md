# WorkFromHome — DFIR Investigation

Digital Forensics & Incident Response investigation of a compromised Windows environment based on the CyberDefenders **WorkFromHome** training lab.

The objective of this project was to reconstruct the attack timeline by correlating multiple Windows forensic artifacts and determine how the threat actor gained access, expanded their privileges, exfiltrated data, evaded security controls, and established persistence.

## Investigation Overview

The investigation reconstructed the following attack chain:

**AnyDesk Remote Access → Internal Resource Access → Data Exfiltration → RDP Access → Privilege Escalation → Defense Evasion → Persistence**

Key findings included:

- AnyDesk was downloaded and used to provide remote access to an external actor operating as `ZeroCTO`.
- Compromised senior developer credentials were used to access an internal resource.
- `Annual_Business_Plan_2025.pdf` was downloaded and transferred from the compromised workstation.
- The senior developer account was subsequently accessed through RDP.
- `SeTakeOwnershipPrivilege` was abused alongside `takeown.exe` and `icacls.exe`.
- `sethc.exe` was replaced with `cmd.exe` to obtain a privileged command shell.
- The AnyDesk directory was added to Microsoft Defender exclusions.
- AnyDesk was configured to start automatically, establishing persistence.

## Forensic Artifacts Analyzed

The investigation involved correlation of:

- Windows Event Logs
- NTFS metadata
- Prefetch files
- Windows Registry artifacts
- Microsoft Edge browser history
- File transfer artifacts
- Windows service and persistence artifacts

## Tools

- Eric Zimmerman Tools
  - MFTECmd
  - PECmd
  - EvtxECmd
  - Timeline Explorer
  - Registry Explorer
- Event Log Explorer
- Windows Event Viewer
- DB Browser for SQLite
- Notepad++

## MITRE ATT&CK

The observed activity was mapped to the following MITRE ATT&CK techniques:

| Tactic | Technique | ID |
|---|---|---|
| Initial Access | Valid Accounts | T1078 |
| Command and Control | Remote Desktop Software | T1219.002 |
| Lateral Movement | Remote Desktop Protocol | T1021.001 |
| Privilege Escalation | Accessibility Features | T1546.008 |
| Defense Impairment | Disable or Modify Tools | T1685 |
| Persistence | Windows Service | T1543.003 |

## Full Investigation Report

The complete investigation report contains the reconstructed incident timeline, forensic evidence, technical analysis, MITRE ATT&CK mapping, relevant artifacts, and remediation recommendations.

➡️ **[Read the full DFIR investigation report](report/WorkFromHome_DFIR_Investigation_Report.pdf)**

## Repository Structure

```text
WorkFromHome-DFIR-Investigation/
├── README.md
├── report/
│   └── WorkFromHome_DFIR_Investigation_Report.pdf
├── evidence/
│   └── selected forensic evidence
└── mitre/
    └── ATT&CK mapping
