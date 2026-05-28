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

- **Total Revenue:** $678,258 USD across 87,614 paid transactions
- **Top Market:** Thailand accounts for 84% of view sessions and ~84% of revenue
- **Viewer Conversion:** 94.2% of unique viewers also made a purchase
- **Best Event:** ONE Samurai 1 PPV drove the highest single-day revenue spike ($5,235 on Mar 20)
- **Data Quality:** 11 anomalies identified including inconsistent country codes, mixed boolean formats, truncated timestamps, and ~8% of orders missing user_id

## Recommendations Summary

1. Fix upstream data quality (country codes, booleans, vendor names)
2. Promote the 3-Month Pass (2.1× higher revenue per order)
3. Restore last_login tracking (80% of records missing)
4. Diversify beyond Thailand market
5. Build loyalty program for the 29.6% repeat-buyer segment
6. Investigate 7,164 unlinked purchase records

---

## How to View the Report

Open `ONE_FC_Analysis_Report.html` in any browser. No server or dependencies required.

Or view via GitHub Pages at: https://kudogoku.github.io/data-analyst-assessment/ONE_FC_Analysis_Report.html

---

## Assumptions

- Revenue = `total_charges_usd` for orders with status: fulfilled / completed / success / paid
- Country codes normalized to ISO 3166-1 alpha-2 (e.g., "THA" → "TH")
- 1,894 duplicate user_id rows removed (kept first occurrence)
- Refund dates before 2026 treated as placeholder/null values
- `kiswe_user_id` in viewdata assumed to map to `user_id` in purchase_data

Full assumption documentation is in the HTML report (Section 08).

---

## Tech Stack

- **Python 3** — pandas, numpy
- **Chart.js** — interactive visualizations in the HTML report
- **AI Tools** — Claude (Anthropic) for analysis assistance — see `AI_Tooling_Workflow_Notes.md`
