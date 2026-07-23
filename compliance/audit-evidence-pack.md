# ISO 27001, SOX & PCI-DSS Audit Evidence Pack

This document consolidates audit evidence mappings for internal and external auditors evaluating identity lifecycle controls.

---

## Compliance Control Framework Mapping

| Regulatory Standard | Control ID | Requirement Description | Technical Evidence Location |
|---|---|---|---|
| **ISO 27001:2013** | **A.9.2.1** | User registration and de-registration process. | `process/jml-runbook.md` + Audit Log export of automated Leaver events. |
| **ISO 27001:2013** | **A.9.2.6** | Review of user access rights. | Quarterly Access Certification campaign completion reports (`governance/access-packages-config.md`). |
| **SOX Section 404** | **ITGC-AC-01** | Timely revocation of access upon employee termination. | Timestamped comparison logs: HR termination timestamp vs. Entra ID `AccountEnabled = false` event. |
| **SOX Section 404** | **ITGC-AC-03** | Segregation of duties enforced for financial systems. | `governance/sod-conflict-matrix.md` + Entitlement Management block policy logs. |
| **PCI-DSS v4.0** | **Requirement 7.2** | Access is granted based on business need-to-know (Least Privilege). | Entitlement Management access package definitions and justification fields. |
| **PCI-DSS v4.0** | **Requirement 8.2** | User identity lifecycle management & session control. | Token revocation logs (`Revoke-MgUserSignInSession`) generated during offboarding runs. |

---

## Sample Audit Verification Artifact

> **Auditor Query:** "Provide evidence that a terminated employee's access was revoked within 1 hour of HR offboarding."
> 
> **Evidence Result (Log Analytics Query):**
> * **HR Termination Event:** `2026-06-15T14:00:00Z` (Employee: `user.test@fintech.com`)
> * **Entra ID Session Revocation:** `2026-06-15T14:02:11Z` (Delta: **2 mins 11 secs**)
> * **Account Disabled Timestamp:** `2026-06-15T14:02:12Z`