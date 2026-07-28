# Segregation of Duties (SoD) Conflict Matrix

To mitigate financial fraud and satisfy **SOX Section 404** and **PCI-DSS 7.1.1** requirements, toxic role combinations are monitored and restricted across all identity workflows.

---

## Toxic Combinations & Control Mechanisms

| Rule ID | Conflicting Role A | Conflicting Role B | Risk Impact | System Control & Enforcement |
| :--- | :--- | :--- | :--- | :--- |
| **SOD-01** | `Payments Processing Access` | `Payments Approval` | Unauthorized wire transfers or fraudulent payout execution. | **Detective Control:** Custom MS Graph PowerShell (`sod_audit.ps1`) continuously audits active assignments and flags dual-holders for immediate remediation. |
| **SOD-02** | `Software Developer` | `Production Deployment Admin` | Pushing unreviewed code directly into production, bypassing change management. | **Preventative Control:** Access Package assignment policy requires secondary approval step from SecOps if user holds Developer role. |
| **SOD-03** | `Vendor Onboarding Admin` | `Accounts Payable` | Creating fictitious vendor accounts and disbursing unauthorized payments. | **Corrective Control:** Flagged during quarterly Access Certification campaigns for immediate manager attestation/revocation. |
| **SOD-04** | `Security Auditor` | `Security Policy Admin` | Modifying audit logging parameters or security policies to conceal unauthorized changes. | **Preventative Control:** PIM role assignment restrictions enforced via Entra ID Privileged Identity Management. |