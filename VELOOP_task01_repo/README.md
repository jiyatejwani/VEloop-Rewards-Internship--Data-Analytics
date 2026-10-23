# VELOOP Rewards — Product Analytics & Data Readiness Blueprint

**Data Analyst Internship · Task 01** · Jiya Tejwani

> ⚠️ **All data in this project is SIMULATED / FICTIONAL**, supplied for analytical testing. Nothing here represents actual VELOOP users, earnings, withdrawals, revenue, retention, or performance.

🔗 **Live site:** _add your Vercel URL here after deploying_ · **Dashboard:** `/#dashboard`

---

## What this project is

VELOOP Rewards is an online rewards-and-engagement product in early development. It does **not yet have the production data** required for conventional product analytics. This project builds the *analytics foundation* that makes meaningful analysis possible once real activity exists: it maps what the product must measure, audits what the simulated data can support today, and specifies what still has to be built.

The live site has four views:

- **Overview** — the readiness verdict and the two findings that shape everything.
- **Dashboard** — 13 live charts computed from the simulated behavioural data (Deliverable #14, realised).
- **Deliverables** — an index of all 21 task deliverables with download links.
- **Data Model** — the 10-entity logical model (6 existing, 4 proposed).

## Two findings that shape everything

1. **The two supplied files are two different user populations.** Both reuse the `VLUSR000001…` ID scheme, but of 1,000 shared IDs, **zero** map to the same person. `user_id` is not a shared key across files — they cannot be joined, only analysed separately or re-keyed.
2. **The entire monetisation layer is missing.** Rewards ledger, wallet transactions, withdrawals, and the referral lifecycle do not exist as tables, and no monetary amount field appears anywhere. Only **7 of 20** sampled KPIs are computable today; the rest depend on proposed structures.

## Readiness verdict

| Status | Areas | Meaning |
|---|---|---|
| ✅ Confirmed | 7 | Data exists and is verified in the simulated set |
| 🟡 To-Be-Verified | 8 | Partially present; needs engineering confirmation |
| 🔴 Proposed | 15 | Does not exist today; must be built (the gap) |

## Deliverables (21)

| # | Deliverable | Format | Status |
|---|---|---|---|
| 1 | Executive Summary | Word | ✅ `deliverables/` |
| 2 | Product Data Audit | Word | ✅ `deliverables/` |
| 3 | Data Coverage Matrix | Excel | ✅ `deliverables/` |
| 4 | User & Account Analytics Specification | Word | ✅ `deliverables/` |
| 5 | Earning & Reward Analytics | Word | ✅ `deliverables/` |
| 6 | Wallet & Withdrawal Analytics | Word | ✅ `deliverables/` |
| 7 | Referral & Engagement Analytics | Word | ✅ `deliverables/` |
| 8 | Event Tracking Plan (38 events) | Excel | ✅ `deliverables/` |
| 9 | Data Dictionary (121 fields) | Excel | ✅ `deliverables/` |
| 10 | Logical Data Model + ER diagram | Word + PNG | ✅ `deliverables/` |
| 11 | KPI Catalogue (37 KPIs) | Excel | ✅ `deliverables/` |
| 12 | Simulated Data Profiling | Excel | ✅ `deliverables/` |
| 13 | Data Quality Audit | Excel | ✅ `deliverables/` |
| 14 | Dashboard Blueprint | **live site** | ✅ this site |
| 15 | Developer Analytics Handoff | Excel | ✅ `deliverables/` |
| 16 | Data Pipeline Proposal | Word + PNG | ✅ `deliverables/` |
| 17 | Privacy & Governance Proposal | Word | ✅ `deliverables/` |
| 18 | Analytics Readiness Assessment | Excel | ✅ `deliverables/` |
| 19 | Source & Verification Register | Excel | ✅ `deliverables/` |
| 20 | Implementation Backlog | Excel | ✅ `deliverables/` |
| 21 | Final Consolidated Report | Word | ✅ `deliverables/` |

## How the dashboard numbers were produced

The behavioural dataset (1,000 users · 7,913 sessions · 35,704 events · 9,846 task attempts) was profiled and aggregated in **Python (pandas)**; the computed figures are embedded in `data.js` and rendered client-side with **Chart.js**. The site is a dependency-free static page — no build step.

## Repo structure

```
.
├── index.html          # the dashboard + deliverables site
├── data.js             # pre-computed metrics (simulated)
├── vercel.json         # static config
├── deliverables/       # the completed task deliverables (.xlsx / .docx)
├── analysis/           # Python (pandas) scripts that produce the findings
│   ├── 01_profile_datasets.py
│   ├── 02_data_quality_audit.py
│   └── 03_build_dashboard_data.py
└── sql/
    └── kpi_queries.sql # KPI definitions in SQL
```

## Reproduce the analysis

```bash
cd analysis
pip install -r requirements.txt
# drop the two supplied workbooks into analysis/data/
python 01_profile_datasets.py      # profiling + referential integrity (#12)
python 02_data_quality_audit.py    # data-quality issues (#13)
python 03_build_dashboard_data.py  # regenerates ../data.js for the dashboard
```

The KPI formulas are defined in SQL in [`sql/kpi_queries.sql`](sql/kpi_queries.sql) — seven computable from the supplied data today, three marked PROPOSED because they depend on tables that do not exist yet.

## Deploy

This is a static site — it deploys to Vercel with zero configuration. See the deployment steps provided alongside this repo.

---

_Integrity note: every analytical conclusion in this project traces to the supplied simulated data or to a documented assumption (see the Source & Verification Register, #19). Simulated data is never presented as an actual VELOOP result._
