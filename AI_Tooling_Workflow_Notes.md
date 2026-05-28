# AI / Tooling Workflow Notes

## Tools Used

| Tool | Purpose |
|------|---------|
| **Claude (Anthropic)** | AI assistant used throughout the assessment |
| **Python 3 / pandas / numpy** | Data loading, cleaning, and analysis |
| **Matplotlib** | Charts in the Jupyter Notebook |
| **Chart.js** | Interactive visualizations in the HTML report |

---

## How Claude Was Used

### 1. HTML report design
I have a basic understanding of HTML but struggled to produce a clean, well-structured visual report on my own. I used Claude to help with the layout, styling, and Chart.js integration. The underlying data and numbers all came from my own Python analysis. Claude handled the presentation layer.

### 2. Interpreting ambiguous columns
When I was unsure about a column's meaning or behavior, I used Claude as a sounding board. Two examples:

**Revenue field selection** The dataset had multiple charge-related columns. `charges_in_usd` contained structured data that would need additional parsing to extract usable numbers. Rather than spending time on that, I checked whether another column already had clean USD values and found `total_charges_usd`. I then asked Claude to confirm whether it was already inclusive of tax, given that the `tax` column sometimes showed values larger than the total. Claude confirmed the platform had already rolled everything into `total_charges_usd`, so I used that.

**geo_country vs country** I asked Claude to explain the difference between these two fields. Understanding that `geo_country` is IP-detected at the time of viewing (while `country` is self-reported at signup) was important for framing the geographic analysis correctly.

### 3. Debugging and error fixing
When I ran into errors such as file path issues in Jupyter, git push failures due to large CSV files, and git history rewriting, I described what I was trying to do and asked for the right approach or command to use.

### 4. Knowing what to analyze
After completing the core revenue and engagement analysis, I asked Claude what else would be worth looking at given the data available. Claude suggested churn indicators and LTV analysis. I attempted both but found the data too incomplete to do properly. `last_login` was missing for 80% of users, and `signup_date` had inconsistent formats and placeholder values. I documented these as data quality issues rather than forcing an analysis that would not be reliable.

### 5. Final cross-check
Before finalizing, I re-ran all metrics in Python and asked Claude to verify that every number in the HTML report matched. This step caught a few discrepancies that were corrected before submission.

---

## Reflection

The most useful pattern was: run the analysis in Python, look at the output, then use Claude to help interpret what it means in business terms or to move faster on parts I was less familiar with such as report design and debugging. The analytical decisions about what to include, what to flag, and what assumptions to make were mine throughout.

