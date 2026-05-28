# AI / Tooling Workflow Notes

## Tools Used

| Tool | Purpose |
|------|---------|
| **Claude (Anthropic)** | AI assistant used during the assessment |
| **Python / pandas / numpy** | Data loading, cleaning, and analysis |
| **Matplotlib** | Data visualizations in the Jupyter Notebook |
| **Chart.js** | Interactive visualizations in the HTML report |

---

## How Claude Was Used

### 1. HTML Report Design
I have a basic understanding of HTML but struggled to produce a clean, well-structured visual report on my own. I used Claude to help with the layout, styling, and Chart.js integration. The underlying data and numbers all came from my own Python analysis — Claude handled the presentation layer.

### 2. Debugging & Error Fixing
When I hit errors during the analysis or while setting up the GitHub repository, I used Claude as a support resource — describing what I was trying to do and asking for the right approach or code to use, rather than searching through documentation alone.

### 3. Understanding the Data
This was my first time working with streaming platform data. I used Claude as a sounding board to help interpret what certain columns meant in context — for example, understanding the difference between `geo_country` (IP-based location at time of viewing) vs `country` (self-reported at signup), and why sessions could be much higher than unique users.

---

## Reflection

Using Claude helped me work through unfamiliar parts of the assessment faster — particularly around report design and debugging. That said, the analytical decisions were my own: which metrics to calculate, how to interpret the data, what anomalies were worth flagging, and what the business implications actually were.

There were also moments where I caught Claude producing incorrect outputs and corrected them myself — which reinforced that AI tools are only useful when you're actively thinking alongside them, not just accepting what they produce.
