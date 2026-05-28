# ONE FC Streaming Platform — Data Analyst Assessment

## Overview

This repository contains my submission for the Data Analyst Technical Assessment. The analysis covers user behavior, revenue performance, event engagement, and data quality for a digital streaming platform (ONE FC), using three datasets spanning January–May 2026.

---

## Datasets

| File | Rows | Description |
|------|------|-------------|
| `userdata.csv` | 65,032 | User account information (country, signup date, active status) |
| `viewdata.csv` | 1,048,575 | Streaming session logs (event, country, session timing) |
| `purchase_data.csv` | 89,434 | Purchase transactions (product, revenue, payment vendor, status) |

---

## Deliverables

| File | Description |
|------|-------------|
| `ONE_FC_Analysis_Report.html` | Full interactive report with charts and findings |
| `ONE_analysis.ipynb` | Jupyter Notebook — data cleaning, EDA, and metrics |
| `README.md` | This file |
| `AI_Tooling_Workflow_Notes.md` | Notes on AI tool usage during assessment |

---

## Key Findings

- **Total Revenue:** $678,258 USD across 87,614 paid transactions (avg $7.74/order)
- **Top Market:** Thailand accounts for 84% of view sessions and 84.3% of revenue
- **Active Viewers:** 98.3% of registered users (62,049 of 63,138) have watched at least once
- **Best Event by Viewers:** Superfan Fights Mar 20 — 41,948 unique viewers
- **Best Event by Engagement:** ONE Samurai 1 PPV — 9.8 sessions per viewer
- **Data Quality:** 11 anomalies identified including inconsistent country codes, mixed boolean formats, placeholder signup dates, and 8% of orders missing user_id

## Recommendations Summary

1. Fix upstream data quality (country codes, booleans, vendor names, date formats)
2. Promote the 3-Month Pass (2.1× higher revenue per order than monthly)
3. Restore last_login tracking (80% of records missing — churn analysis not possible)
4. Diversify beyond Thailand market (84% revenue concentration is a risk)
5. Build loyalty program for the 29.6% repeat-buyer segment
6. Investigate 7,164 unlinked purchase records ($55,247 in unattributed revenue)

---

## How to View the Report

Open `ONE_FC_Analysis_Report.html` in any browser. No server or dependencies required.

GitHub Pages: https://kudogoku.github.io/data-analyst-assessment/ONE_FC_Analysis_Report.html

---

## Assumptions

- Revenue = `total_charges_usd` for orders with status: fulfilled / completed
- `tax` and `unit_price` are in local currency — not used in revenue calculations
- Country codes normalized to ISO 3166-1 alpha-2 (e.g., "THA" → "TH")
- 1,894 duplicate user_id rows removed from userdata (kept first occurrence)
- `time_refund_processed = 2024-01-01` treated as system default, not real refund date
- 1,894 users with `signup_date = "1/1/2030"` treated as valid users with unknown signup date
- `kiswe_user_id` in viewdata assumed to map to `user_id` in purchase_data

---

## Tech Stack

- **Python 3** — pandas, numpy, matplotlib
- **Chart.js** — interactive visualizations in the HTML report
- **AI Tools** — Claude (Anthropic) — see `AI_Tooling_Workflow_Notes.md`

---

*Analysis by Warinthip Arakkul — May 2026*
