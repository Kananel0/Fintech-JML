# Joiner-Mover-Leaver (JML) Standard Operating Procedure & Automation Runbook

This document details the automated workflow logic for identity lifecycle events across all 500+ identities in the fintech environment.

---

## 🚀 1. Joiner Workflow (Onboarding)

* **Trigger:** HR System pushes new employee record via API / CSV sync with status `Active` and `Start Date <= Today`.
* **SOP Steps:**
  1. **Identity Provisioning:** Entra ID Account created automatically; UPN mapped as `firstname.lastname@fintech.com`.
  2. **Core Attributes Populated:** `Department`, `JobTitle`, `CostCenter`, `ManagerID`, `EmployeeType`.
  3. **Dynamic Group Assignment:** User falls into target dynamic groups based on attribute rules (e.g., `Dept-Engineering-All`).
  4. **Entitlement Management Package Assignment:** Auto-assigns the pre-approved baseline **Access Package** (M365 License, Slack, Base Azure AD Apps) requiring no manual approval.
  5. **Temporary Access Pass (TAP):** Generates a TAP sent to the hiring manager for Day 1 passwordless onboarding.

---

## 🔄 2. Mover Workflow (Role Transition)

* **Trigger:** HR updates `Department`, `JobTitle`, or `ManagerID`.
* **SOP Steps:**
  1. **Dynamic Group Re-evaluation:** Entra ID engine updates group memberships in real-time based on updated attributes.
  2. **Access Removal:** Deprecated access packages tied to the previous department are revoked automatically.
  3. **New Entitlement Request:** User or Manager requests the new role's Access Package via MyAccess portal.
  4. **Segregation of Duties (SoD) Check:** Entitlement engine checks if new access conflicts with existing roles before routing for Manager approval.
  5. **Audit Event Logged:** Event tagged as `Identity Lifecycle - Mover` in Log Analytics.

---

## 🛑 3. Leaver Workflow (Offboarding)

* **Trigger:** HR marks employee status as `Terminated` or sets `End Date = Today`.
* **SOP Steps:**
  1. **Immediate Revocation (T+0 Mins):**
     * Account disabled (`AccountEnabled = False`).
     * Revoke all active HTTP sessions / Refresh Tokens via PowerShell / Graph API (`Revoke-MgUserSignInSession`).
  2. **Access Package Stripping:** Remove all assigned Entitlement Management access packages.
  3. **License Reclamation:** Unassign high-cost licenses (E5 / Power BI) to return them to the available pool.
  4. **Mailbox & Data Retention Hold:** Apply Legal Hold / Litigation Hold on Exchange Online mailbox and OneDrive.
  5. **Offboarding Log Export:** Generate an immutable offboarding audit trail for compliance verification.