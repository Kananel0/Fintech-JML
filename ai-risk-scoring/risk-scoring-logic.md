# AI & Risk-Based Entitlement Scoring Framework

This module details how machine learning signals from **Microsoft Entra ID Protection** and behavioral telemetry feed into an Identity Governance risk scoring system.

---

## Risk Scoring Formula & Weighting

Every identity is assigned a composite **Entitlement Risk Score ($RS$)** ranging from `0` to `100`:

$$RS = (W_1 \times R_I) + (W_2 \times D_A) + (W_3 \times S_{SOD}) + (W_4 \times A_P)$$

| Component | Variable | Description | Weight ($W$) |
|---|---|---|---|
| **Identity Protection Risk** | $R_I$ | Risk level flagged by Entra ID AI models (Leaked Credentials, Impossible Travel, Suspicious IP). | **35%** |
| **Dormant Access** | $D_A$ | User holds entitlements that haven't been utilized in $> 90$ days. | **25%** |
| **SoD Proximity** | $S_{SOD}$ | User holds 1 component of a toxic combination and requests adjacent access. | **20%** |
| **Privileged Access** | $A_P$ | Scope of administrative roles assigned (Global Admin, Payment Admin). | **20%** |

---

## Risk-Driven Governance Actions
┌────────────────────────┐
           │  Calculate Risk Score  │
           └───────────┬────────────┘
                       │
   ┌───────────────────┼───────────────────┐
   ▼                   ▼                   ▼
Score < 40          Score 40-70         Score > 70
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│ Auto-Approve│     │ Require Manager│   │ Block Access│
│ Standard    │     │ Approval +  │     │ + Trigger   │
│ Requests    │     │ Step-up MFA │     │ SOC Incident│
└─────────────┘     └─────────────┘     └─────────────┘


1. **Low Risk ($RS < 40$):** Standard automated lifecycle processing.
2. **Medium Risk ($RS = 40-70$):** Forces an out-of-cycle Access Review for the user's manager; requires Phishing-Resistant MFA to activate access.
3. **High Risk ($RS > 70$):** Immediately revokes PIM eligible assignments, drops active sessions, and alerts the Security Operations Center (SOC).