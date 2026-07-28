# ISO 27001, SOX & PCI-DSS Audit Evidence Pack

This document consolidates audit evidence mappings for internal and external auditors evaluating identity lifecycle controls within the Microsoft Entra ID environment.

---

## Compliance Control Framework Mapping

| Regulatory Standard | Control ID | Requirement Description | Technical Evidence Location |
| :--- | :--- | :--- | :--- |
| **ISO 27001:2022** | **A.9.2.1** | User registration and de-registration process. | `process/jml-runbook.md` + Entra ID Audit Log export of automated Leaver events (`Kevin Botha`). |
| **ISO 27001:2022** | **A.9.2.6** | Periodic review and attestation of user access rights. | Quarterly Access Certification campaign completion reports (`governance/access-packages-config.md`). |
| **SOX Section 404** | **ITGC-AC-01** | Timely revocation of access upon employee termination. | Timestamped comparison logs: HR termination timestamp vs. Entra ID `AccountEnabled = $false` audit event. |
| **SOX Section 404** | **ITGC-AC-03** | Segregation of duties monitored and enforced for financial systems. | `governance/sod-conflict-matrix.md` + Custom MS Graph PowerShell audit execution logs (`sod_audit.ps1`). |
| **PCI-DSS v4.0** | **Requirement 7.2** | Access is granted based on business need-to-know (Least Privilege). | Entitlement Management access package definitions and justification fields for financial roles. |
| **PCI-DSS v4.0** | **Requirement 8.2** | User identity lifecycle management & active session control. | Token revocation logs (`Revoke-MgUserSignInSession`) generated during offboarding execution. |

---

## Sample Audit Verification Artifact

> **Auditor Query:** "Provide evidence that a terminated employee's access was revoked within 1 hour of HR offboarding."
> 
> **Evidence Result (Directory Audit Trail):**
> * **HR Termination Event:** `2026-06-15T14:00:00Z` (Employee: `Kevin Botha`)
> * **Entra ID Session Revocation:** `2026-06-15T14:02:11Z` (Delta: **2 mins 11 secs**)
> * **Account Disabled Timestamp:** `2026-06-15T14:02:12Z` (`AccountEnabled = $false`)