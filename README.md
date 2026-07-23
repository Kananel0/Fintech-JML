# Fintech JML

# Fintech Joiner-Mover-Leaver (JML) Automation & Compliance Program
### Microsoft Entra ID Governance | Entitlement Management | SoD | ISO 27001 | AI Risk Scoring

![Status](https://img.shields.io/badge/status-complete-brightgreen)
![Industry](https://img.shields.io/badge/industry-Fintech-purple)
![Compliance](https://img.shields.io/badge/compliance-ISO%2027001%20%7C%20SOX%20%7C%20PCI--DSS-orange)

▶️ **Demo Video:** [Watch on YouTube](PASTE_YOUTUBE_LINK_HERE)

---

## 📌 What This Project Is

This project simulates the full **identity lifecycle governance program** for a regulated fintech company with 500+ employees, subject to **PCI-DSS, SOX, and ISO 27001**. In fintech, an identity mistake — like an ex-employee retaining access to a payments system — isn't just a security issue, it's a regulatory and financial one.

The project builds an end-to-end **Joiner-Mover-Leaver (JML)** process on Microsoft Entra ID Governance, including:

- Simulated HR-driven provisioning (mock HR feed) that triggers automatic Entra ID account creation and dynamic group membership based on department, job title, and cost center
- **Joiner:** automated onboarding using **Entitlement Management access packages** — role-based access bundles instead of manual, one-off app grants
- **Mover:** automatic access recalculation when an employee changes department, removing old entitlements and granting new ones, with a full audit trail of the change
- **Leaver:** same-day deprovisioning, license reclamation, and a compliance-driven mailbox/data retention hold
- **Segregation of Duties (SoD)** checks — e.g., a user in "Payments Processing" cannot simultaneously hold "Payment Approval" rights
- Recurring **access certification campaigns** where managers formally attest to their team's access
- An **AI-based risk scoring layer** using Entra ID Identity Protection signals to flag unusual entitlement combinations or dormant privileged accounts

## 🎯 Why I Built This

Fintech is one of the highest-stakes environments for identity management — auditors, regulators, and attackers are all looking at the same weak point: **who has access to what, and can you prove it was appropriate at every point in time.**

I built this project to demonstrate that I can:
- Design lifecycle automation that removes human error from onboarding/offboarding at scale (500+ employees)
- Build in **preventative** controls (SoD) rather than relying only on after-the-fact detection
- Produce actual **audit evidence** — not just configure a tool, but generate the reports a real ISO 27001 or SOX auditor would request
- Apply AI/risk-based thinking to identity governance, rather than treating access reviews as a checkbox exercise

## 🛡️ How This Protects the Organization

| Risk | Control Implemented | Outcome |
|---|---|---|
| Ex-employee retains access to financial systems after leaving | Automated same-day leaver deprovisioning | Access is revoked the moment HR marks termination — no manual lag |
| Employee accumulates access across multiple roles over time ("access creep") | Mover automation recalculates entitlements on role change | Old access is removed automatically, not left in place "just in case" |
| One person can both process and approve a payment (fraud risk) | Segregation of Duties (SoD) policy enforcement | Conflicting role combinations are blocked at request time, not discovered later |
| Manual onboarding grants excessive or inconsistent access | Entitlement Management access packages | New hires get a pre-approved, role-appropriate access bundle every time |
| Regulator or auditor asks "prove who had access to X on date Y" | Access certification campaigns + audit logging | Documented, timestamped evidence of manager attestation is available on demand |
| Dormant privileged accounts go unnoticed and become a target | AI-driven risk scoring on entitlements | Unusual or stale access patterns are flagged for review automatically |

## 🏗️ Architecture / Process Flow

```
HR System (simulated feed)
        │
        ▼
Microsoft Entra ID Governance
        │
        ├── JOINER  → Access Package Assignment (role-based bundle)
        ├── MOVER   → Dynamic Group Re-evaluation → Access Recalculation
        ├── LEAVER  → Automated Deprovisioning + License Reclamation + Retention Hold
        │
        ├── Segregation of Duties Engine → Blocks conflicting entitlement combos
        ├── Access Certification Campaigns → Manager attestation (recurring)
        └── AI Risk Scoring (Identity Protection signals) → Flags anomalies
```

## 📂 Repository Structure

```
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
│   └── risk-scoring-logic.md
├── screenshots/
└── README.md
```

## 🧰 Skills Demonstrated

`Microsoft Entra ID Governance` · `Entitlement Management` · `Dynamic Groups` · `Segregation of Duties` · `Access Certifications` · `Identity Lifecycle Automation` · `ISO 27001` · `SOX` · `PCI-DSS` · `AI-Assisted Risk Scoring`

## 🔗 Related Certification

This project was built as part of my preparation for **Microsoft SC-300: Identity and Access Administrator**.

---
📩 Feel free to connect with me on [LinkedIn](PASTE_LINKEDIN_LINK_HERE) if you'd like to discuss the design decisions behind this project.
