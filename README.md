# Fintech Joiner-Mover-Leaver (JML) Automation & Compliance Program
### Microsoft Entra ID Governance | Entitlement Management | SoD Detective Controls | ISO 27001 | Risk-Based CA

![Status](https://img.shields.io/badge/status-complete-brightgreen)
![Industry](https://img.shields.io/badge/industry-Fintech-purple)
![Compliance](https://img.shields.io/badge/compliance-ISO%2027001%20%7C%20SOX%20%7C%20PCI--DSS-orange)


---

## 📌 What This Project Is

This project simulates a complete **identity lifecycle governance program** for a regulated fintech company with 500+ employees subject to **PCI-DSS, SOX, and ISO 27001**. In fintech, identity errors—such as an offboarded employee retaining access to a payments pipeline—present severe regulatory and financial risks.

The project builds an end-to-end **Joiner-Mover-Leaver (JML)** workflow using Microsoft Entra ID Governance and Microsoft Graph PowerShell, featuring:

- **Simulated HR-Driven Provisioning:** Mock HR updates triggering automatic Entra ID user management and dynamic department assignment.
- **Joiner Automation:** Onboarding acceleration using **Entitlement Management Access Packages**—role-based access bundles rather than one-off manual app grants.
- **Mover Automation:** Attribute recalculation upon department change with full directory audit log tracking.
- **Leaver Automation:** Immediate account blocking, session revocation, and license deprovisioning.
- **Segregation of Duties (SoD) Controls:** Custom PowerShell-based detective control querying Microsoft Graph API to continuously detect and flag conflicting entitlement combinations (e.g., *Payments Processing Access* + *Payments Approval*).
- **Access Certification Campaigns:** Scheduled recurring manager attestations to uphold Principle of Least Privilege (PoLP).
- **AI-Powered Risk Layer:** Machine-learning risk scoring via **Entra ID Identity Protection** (User Risk & Sign-in Risk) mapped to Conditional Access enforcement policies.

---

## 🎯 Why I Built This

Fintech is one of the highest-stakes environments for identity management. Auditors, regulators, and security teams scrutinize a core question: **"Who has access to what, and can you prove it was appropriate at every point in time?"**

This project demonstrates my ability to:
- Design automated identity workflows that eliminate human error during onboarding and offboarding.
- Engineer custom detective controls (SoD scripts via MS Graph) to solve governance gaps in hybrid/lab environments.
- Produce an actual **Audit Evidence Pack**—the exact artifacts an ISO 27001 or SOX auditor requests.
- Enforce risk-based identity protection using real-time machine learning signals rather than static access rules.

---

## 🛡️ How This Protects the Organization

| Risk | Control Implemented | Outcome |
| :--- | :--- | :--- |
| Ex-employee retains access to financial systems after leaving | Automated same-day leaver deprovisioning | Access is revoked the moment HR/Admin marks termination—no manual lag |
| Employee accumulates excessive access across multiple roles ("access creep") | Mover attribute recalculation on role change | Department attributes update cleanly, triggering access updates and audit trails |
| One person holds both processing and approval rights (fraud risk) | Graph API SoD Detective Control (`sod_audit.ps1`) | Toxic role combinations are dynamically audited and flagged for remediation |
| Manual onboarding grants inconsistent access | Entitlement Management access packages | New hires receive pre-approved, role-appropriate access bundles every time |
| Auditor asks "prove who had access to X on date Y" | Access certification campaigns + directory audit logs | Documented, timestamped evidence of manager attestation is available on demand |
| Account compromise or anomalous sign-in | AI-driven Identity Protection risk policies | ML risk signals (Medium+) automatically trigger mandatory MFA or password resets |

---

## 🏗️ Architecture / Process Flow

HR System (Simulated Feed)
│
▼
Microsoft Entra ID Governance
│
├── JOINER  → Access Package Assignment (Role-Based Bundle)
├── MOVER   → Dynamic Attribute Recalculation → Audit Logging
├── LEAVER  → Immediate Account Block + Token Revocation
│
├── SoD Detective Control (MS Graph API) → Audits & flags conflicting roles
├── Access Certification Campaigns → Quarterly manager attestation
└── AI Risk Layer (Identity Protection ML) → Risk-Based Conditional Access Enforcement


---

## 📂 Repository Structure

├── process/
│   ├── jml-runbook.md
│   └── process-flow-diagram.png
├── governance/
│   ├── access-packages-config.md
│   ├── sod-conflict-matrix.md
│   └── access-certification-report-sample.pdf
├── compliance/
│   └── audit-evidence-pack.md
├── ai-risk-scoring/
│   └── risk-scoring-framework.md
├── scripts/
│   └── sod_audit.ps1
├── screenshots/
└── README.md


---

## 🧰 Skills Demonstrated

`Microsoft Entra ID Governance` · `Microsoft Graph PowerShell` · `Entitlement Management` · `Segregation of Duties (SoD)` · `Access Certifications` · `Conditional Access & Identity Protection` · `ISO 27001` · `SOX` · `PCI-DSS`

---

## 🔗 Related Certification

This project was built as part of my preparation for the **Microsoft SC-300: Identity and Access Administrator** certification exam.

---
📩 Feel free to connect with me on [LinkedIn](https://www.linkedin.com/in/kananelo-mohale) to discuss the identity architecture and implementation decisions behind this project.