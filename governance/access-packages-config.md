# Entitlement Management — Access Packages Configuration

Access Packages bundle applications, security groups, and cloud roles into single, role-based requestable units to uphold the Principle of Least Privilege (PoLP).

---

## 1. Access Package Catalog Matrix

| Catalog | Access Package Display Name | Included Resources | Approval Requirements | Expiration / Review | SoD Conflict Guardrail |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Core Workforce** | `Baseline Employee Access` | • M365 E5 License<br>• Group: `All-Employees`<br>• App: HR Self-Service Portal | **Automatic** (No approval required) | Never (Valid while active) | None |
| **Engineering** | `DevOps Contributor Access` | • Group: `DevOps-Engineers`<br>• App: GitHub Enterprise<br>• Role: Azure Dev Contributor | **1-Step:** Direct Manager Approval | 180 Days (Requires renewal) | None |
| **Finance Operations** | `Payments Processing Access` | • Group: `Payments Processing`<br>• App: SWIFT / Payment Gateway Portal | **2-Step:** Manager + FinOps Security Lead | 90 Days + Quarterly Review | ⚠️ Conflicting with `Payments Approval` |
| **Finance Operations** | `Payments Approval` | • Group: `Payments Approval`<br>• App: Payment Release Authorization | **2-Step:** Finance Director + Compliance Lead | 90 Days + Quarterly Review | ⚠️ Conflicting with `Payments Processing Access` |
| **Privileged Access** | `Database Admin Access` | • PIM Role: Azure SQL Admin<br>• App: Production DB Jump Box | **2-Step:** IT Director + Security Officer | 30 Days (Strict expiration) | None |

---

## 2. Policy Governance Rules

### Joiner Rule (Baseline)
- **Target Audience:** All members within the tenant.
- **Assignment Method:** Automatic assignment via dynamic user attributes (`department`, `userType eq 'Member'`).

### Mover / SoD Rule (Detective Control)
- **Policy Enforcement:** Custom PowerShell detective control (`sod_audit.ps1`) executing via Microsoft Graph API.
- **Trigger:** Any dual assignment of `Payments Processing Access` and `Payments Approval` is flagged immediately in the compliance audit log for access revocation.

### Access Review Schedule
- **Frequency:** Quarterly (90-day intervals).
- **Reviewer Type:** Direct Managers / Designated Resource Owners.
- **Action on Non-Response:** Remove access automatically after 14 days.