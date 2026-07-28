# AI & Risk-Based Entitlement Scoring Framework

This module details how machine learning signals from **Microsoft Entra ID Protection** and behavioral telemetry feed into an Identity Governance risk scoring model to evaluate access requests and active entitlements.

---

## 1. Risk Scoring Formula & Weighting

Every identity is evaluated against a composite **Entitlement Risk Score ($RS$)** ranging from `0` to `100`:

$$RS = (W_1 \times R_I) + (W_2 \times D_A) + (W_3 \times S_{SOD}) + (W_4 \times A_P)$$

| Component | Variable | Description | Weight ($W$) | Primary Signal Source |
| :--- | :--- | :--- | :--- | :--- |
| **Identity Protection Risk** | $R_I$ | Real-time ML risk flagged by Entra ID Protection (Leaked Credentials, Impossible Travel, Suspicious IP). | **35%** | Entra ID Identity Protection API |
| **Dormant Access** | $D_A$ | User holds entitlements or group memberships unutilized for $> 90$ days. | **25%** | Entra ID Audit & Sign-in Logs |
| **SoD Proximity** | $S_{SOD}$ | User holds 1 component of a toxic role pair and requests adjacent access. | **20%** | Custom MS Graph Script (`sod_audit.ps1`) |
| **Privileged Access** | $A_P$ | Scope of administrative or high-impact roles assigned (Global Admin, Payment Admin). | **20%** | Entra ID Directory Roles & PIM |

---

## 2. Risk-Driven Governance Logic

                ┌────────────────────────┐
                │  Calculate Risk Score  │
                └───────────┬────────────┘
                            │
   ┌────────────────────────┼────────────────────────┐
   ▼                        ▼                        ▼
Score < 40               Score 40-70              Score > 70
┌─────────────┐          ┌─────────────┐          ┌─────────────┐
│ Auto-Approve│          │ Require     │          │ Block Access│
│ Standard    │          │ Manager     │          │ + Trigger   │
│ Requests    │          │ Approval +  │          │ SOC Incident│
│             │          │ Step-up MFA │          │             │
└─────────────┘          └─────────────┘          └─────────────┘


### Risk Tier Thresholds
1. **Low Risk ($RS < 40$):** Standard automated JML processing via Entitlement Management Access Packages.
2. **Medium Risk ($RS = 40 - 70$):** Triggers step-up MFA via Conditional Access and schedules an out-of-cycle Access Review for the manager.
3. **High Risk ($RS > 70$):** Enforces immediate token revocation via Microsoft Graph (`Revoke-MgUserSignInSession`), disables active assignments, and logs a high-severity alert for SOC remediation.

---

> **Implementation Note:** In this environment, real-time risk scoring ($R_I$) is actively enforced via risk-based Conditional Access policies (`Enforce User Risk Policy` and `Enforce Sign-in Risk Policy`). SoD conflict tracking ($S_{SOD}$) is executed via custom Microsoft Graph PowerShell auditing.