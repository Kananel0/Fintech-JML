# Segregation of Duties (SoD) Conflict Matrix

To mitigate financial fraud and maintain compliance with SOX and PCI-DSS, conflicting roles are strictly prohibited from co-existing on a single identity.

---

## Toxic Combinations & Preventative Controls

| Rule ID | Conflicting Role A | Conflicting Role B | Risk Impact | System Control / Action |
|---|---|---|---|---|
| **SOD-01** | `Payments Processing` | `Payments Approval` | Unauthorized wire transfers or fraudulent payout execution. | **Preventative:** Entra ID Entitlement Management blocks auto-assignment; alerts SOC if manually granted. |
| **SOD-02** | `Software Developer` | `Production Deployment Admin` | Pushing unreviewed code directly into production bypasses change controls. | **Preventative:** Access package request rejected automatically if user holds developer role. |
| **SOD-03** | `Vendor Onboarding Admin` | `Vendor Account Payable` | Creating fictitious vendor accounts and disbursing payments to them. | **Corrective:** Flagged during quarterly Access Certification campaigns for immediate revocation. |
| **SOD-04** | `Security Auditor` | `Security Policy Admin` | Auditor modifying security logs or controls to cover malicious activity. | **Preventative:** Hard conflict enforced via Entra Custom Security Attributes. |