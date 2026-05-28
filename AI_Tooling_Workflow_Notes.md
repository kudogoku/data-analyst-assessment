# AI / Tooling Workflow Notes

## Tools Used

| Tool | Purpose |
|------|---------|
| **Claude (Anthropic)** | Primary AI assistant throughout the assessment |
| **Python / pandas** | Data loading, cleaning, and analysis |
| **Chart.js** | Interactive visualizations in the HTML report |
| **Google** | Reference for ISO 3166 country codes, Chart.js docs |

---

## How Claude Was Used

### 1. Archive Extraction
The data was provided as a `.7z` file. When standard tools weren't available in the environment, I used Claude to write a Python script using `ctypes` to call the system's `libarchive.so` directly — extracting all three CSVs without needing to install anything.

> **Prompt used:** *"7z isn't installed, but libarchive.so.13 is available. Write Python using ctypes to list and extract files from a .7z archive."*

I validated the output by checking file sizes matched the archive manifest before proceeding.

---

### 2. Data Exploration & Cleaning Strategy
After loading the datasets, I used Claude to help identify systematic issues across all three files simultaneously rather than discovering them one at a time.

> **Workflow:** Run pandas `.describe()`, `.value_counts()`, and `.isnull().sum()` → paste output to Claude → discuss what anomalies are worth fixing vs. flagging.

**Example where I modified Claude's suggestion:** Claude initially suggested dropping all rows with truncated `signup_date` values. I instead decided to flag the issue and work around it, since removing those rows would have eliminated ~90% of the user dataset — not appropriate given the task was analysis, not cleansing-for-ML.

---

### 3. Revenue Analysis Logic
Claude helped draft the SQL-equivalent logic for grouping revenue by product, vendor, and month in pandas. I reviewed and adjusted the paid status filter — Claude initially included only `'fulfilled'` but I expanded it to also include `'completed'`, `'success'`, and `'paid'` after checking that these all represent genuine successful transactions.

**Rejected suggestion:** Claude proposed using `charges_in_usd` as the revenue field. I rejected this because that column contains a large embedded JSON blob, not a simple numeric value. `total_charges_usd` is the correct pre-calculated field.

---

### 4. Report Design
Claude generated the HTML report with embedded Chart.js visualizations. I reviewed all chart data points against the raw analysis output to confirm accuracy before including them. The daily revenue chart, product doughnut, and event bar chart were all manually verified against the pandas groupby outputs.

---

### 5. Data Quality Categorization
I used Claude to help organize and prioritize the anomalies into HIGH / MEDIUM / LOW severity categories. The categorization logic was mine — HIGH = breaks analysis results, MEDIUM = distorts metrics, LOW = cosmetic/minor.

---

## What I Validated or Rejected

| AI Suggestion | Action | Reason |
|---------------|--------|--------|
| Use `charges_in_usd` for revenue | ❌ Rejected | Column contains JSON, not a number |
| Drop rows with truncated signup dates | ❌ Modified | Would remove 90% of data — flag instead |
| Include only `fulfilled` status as paid | ✏️ Modified | `completed`, `success`, `paid` also represent real transactions |
| Normalize country to 3-letter codes | ✏️ Modified | Used 2-letter ISO alpha-2 instead — more standard |
| Mark all 3,597 backdated refunds as errors | ✅ Accepted | Refund date before order date is logically impossible |

---

## Reflection

Using Claude significantly accelerated the extraction and cleaning phases. The value wasn't in having it generate final answers — it was in quickly generating code to explore data I'd never seen before, which I then read, verified, and adjusted. Every number in the report was cross-checked against the raw pandas output.

The assessment brief is right that "using AI to generate code without understanding it will likely become evident during review." The places where I pushed back or modified suggestions — particularly around the revenue field and status normalization — are where actual business understanding matters, and no AI tool can substitute for reading the data carefully.
