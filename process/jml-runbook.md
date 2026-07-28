# Joiner-Mover-Leaver (JML) Standard Operating Procedure & Automation Runbook

This document details the automated workflow logic and operational procedures for identity lifecycle events across all 500+ identities in the fintech environment.

---

## 🚀 1. Joiner Workflow (Onboarding)

* **Trigger:** HR System pushes new employee record via API / CSV sync with status `Active` and `Start Date <= Today`.
* **SOP Steps:**
  1. **Identity Provisioning:** Entra ID Account created automatically; UPN mapped as `firstname.lastname@scara.io`.
  2. **Core Attributes Populated:** `Department`, `JobTitle`, `CostCenter`, `ManagerID`, `EmployeeType`.
  3. **Dynamic Group Assignment:** User falls into target dynamic groups based on attribute rules (e.g., `Dept-Engineering-All`).
  4. **Entitlement Management Package Assignment:** Auto-assigns the pre-approved baseline **Access Package** (M365 E5 License, HR Portal, Baseline Apps) requiring no manual approval.
  5. **Temporary Access Pass (TAP):** Generates a TAP sent to the hiring manager for Day 1 passwordless onboarding.

---

## 🔄 2. Mover Workflow (Role Transition)

* **Trigger:** HR updates `Department`, `JobTitle`, or `ManagerID`.
* **SOP Steps:**
  1. **Dynamic Group Re-evaluation:** Entra ID engine updates dynamic group memberships in real-time based on updated user attributes.
  2. **Attribute Recalculation:** User department and job attributes are modified via Microsoft Graph (`Update-MgUser`).
  3. **Access Adjustment:** Deprecated access packages tied to the previous department are revoked, and new role access packages are assigned via MyAccess or direct entitlement policies.
  4. **Segregation of Duties (SoD) Audit:** Custom PowerShell detective control (`sod_audit.ps1`) audits active assignments via Microsoft Graph API to detect and flag any conflicting entitlement combinations (e.g., `Payments Processing Access` + `Payments Approval`).
  5. **Audit Event Logged:** Event tagged as `Identity Lifecycle - Mover` in Entra ID Audit Logs.

---

## 🛑 3. Leaver Workflow (Offboarding)

* **Trigger:** HR marks employee status as `Terminated` or sets `End Date = Today`.
* **SOP Steps:**
  1. **Immediate Revocation (T+0 Mins):**
     * Account disabled (`AccountEnabled = $false`).
     * Revoke all active HTTP sessions / Refresh Tokens via Microsoft Graph PowerShell (`Revoke-MgUserSignInSession -UserId $userId`).
  2. **Access Package Stripping:** Remove all assigned Entitlement Management access packages.
  3. **License Reclamation:** Unassign high-cost licenses (M365 E5 / Power BI) to return them to the available tenant pool.
  4. **Mailbox & Data Retention Hold:** Apply Litigation Hold on Exchange Online mailbox and OneDrive for compliance auditing (**ISO 27001 A.9.2.6**).
  5. **Offboarding Log Export:** Generate an immutable offboarding audit trail verifying sign-in block and timestamped account state.