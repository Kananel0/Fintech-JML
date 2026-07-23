# Entitlement Management — Access Packages Configuration

Access Packages bundle applications, security groups, and SharePoint sites into single, role-based requestable units.

---

## Access Package Catalog Matrix

| Catalog | Access Package Name | Included Resources | Approval Requirements | Expiration / Review |
|---|---|---|---|---|
| **Core Workforce** | `PKG-Baseline-Employee` | • M365 E5 License<br>• Group: `All-Employees`<br>• App: HR Self-Service Portal | **Automatic** (No approval required) | Never (Valid while employed) |
| **Engineering** | `PKG-DevOps-Contributor` | • Group: `DevOps-Engineers`<br>• App: GitHub Enterprise<br>• Role: Azure Dev Contributor | **1-Step:** Direct Manager Approval | 180 Days (Requires renewal) |
| **Finance Operations** | `PKG-Payments-Processing` | • Group: `FinOps-Payments`<br>• App: SWIFT/Payment Gateway Portal | **2-Step:** Manager + FinOps Security Lead | 90 Days + Access Review |
| **Privileged Access** | `PKG-Database-Admin` | • PIM Eligible Role: Azure SQL Admin<br>• App: Production DB Jump Box | **2-Step:** IT Director + Security Officer | 30 Days (Strict expiration) |