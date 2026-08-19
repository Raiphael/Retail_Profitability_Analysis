# Retail Profitability & Returns Analysis

*A project exploring category profitability, discounting behavior, and product returns in a multi-category retail dataset.*

## Table of Contents
- [Project Overview](#project-overview)
- [Business Context & Questions](#business-context--questions)
- [Data Source](#data-source)
- [Tools Used](#tools-used)
- [Methodology](#methodology)
- [Key Findings](#key-findings)
- [Repository Structure](#repository-structure)
- [How to Reproduce](#how-to-reproduce)
- [Limitations](#limitations)
- [Business Context/Recommendation](#business-conclusionrecommendation)
- [Author](#author)

## Project Overview
This project analyzes a relational retail dataset to understand which product categories are actually profitable once discounts and returns are factored in, using SQL for aggregation and Python for deeper transaction-level testing.

## Business Context & Questions
This project is framed around two connected business questions:

1. **Profitability** — Which product categories generate the most profit, and how much of that comes from sales volume versus per-unit margin?
2. **Returns & discounting** — Does heavier discounting correlate with higher return rates, and how much profit (if any) do returns actually cost each category?

## Data Source
A relational retail transaction dataset, provided as both CSVs and a SQLite database:

| File | Description |
|---|---|
| `categories.csv` | 10 product categories |
| `products.csv` | 100 products, linked to categories |
| `customers.csv` | 1,000 customers — demographics, region, segment |
| `orders.csv` | 10,000 orders |
| `order_details.csv` | ~30,271 line items — quantity, unit cost, unit price, discount rate, return status |
| `retail_store.db` | Same data, pre-loaded as a relational SQLite database |

## Tools Used
- **SQL (SQLite)** — joins across tables, category-level aggregation
- **Python (pandas)** — transaction-level analysis, correlation testing
- **seaborn / matplotlib** — data visualization
- **SciPy** — statistical significance testing (Pearson correlation, p-values)
- **Jupyter Notebook** — analysis environment
- **Git / GitHub** — version control and publishing

## Methodology
1. Framed the two business questions above before writing any queries
2. Explored the data — loaded all five tables, checked structure, data types, and nulls (`eda.ipynb`)
3. **Question 1:** wrote a SQL query joining `order_details`, `products`, and `categories` to compute discount-adjusted total profit, sales volume, and volume-weighted per-unit margin per category
4. Added a supporting query computing profit margin as a percentage of revenue per category, to separate dollar-based margin from percentage-based margin
5. **Question 2:** wrote a SQL query computing average discount rate, return rate, and profit lost to returns per category
6. Tested the discount-rate/return-rate relationship at two levels — individual line items (n = 30,271) and category averages (n = 10) — using Pearson correlation
7. Checked statistical significance (p-values) at both levels with `scipy.stats.pearsonr`, given how small the category-level sample is
8. Visualized each finding with seaborn and interpreted it directly against the business questions

## Key Findings
**Question 1: Profitability**
- There's no single "most profitable" category — the answer depends on whether profitability is measured in total dollars or in margin efficiency, and those two lenses point to different winners.
- One category dominates on total profit, driven almost entirely by a high price point and strong sales volume rather than efficient pricing — it moves a lot of relatively expensive product, but isn't the best-run category by markup.
- A different category leads when profitability is measured as a percentage of revenue instead, despite generating far less total profit — a genuine margin-efficiency story rather than a volume story.
- In short, this store has two distinct paths to profitability: one built on volume and price point, another built on pricing efficiency — and conflating the two would misread which categories are actually performing well.

**Question 2: Returns & Discounting**
- Heavier discounting does not predict higher return rates in this data. This was tested twice — once across every individual transaction, and once across category-level averages — and neither test showed a statistically meaningful relationship. A strategy of cutting discounts to reduce returns would not be supported by this analysis.
- Return rate and the dollar cost of returns tell two different stories, echoing the same dollar-vs-percentage split from Question 1. The category with the best (lowest) return rate in the store also has the single highest dollar cost from returns — simply because it's a high-value category, so even a low rate adds up.
- One category stands out as genuinely worth operational attention: it has both an elevated return rate *and* healthy margins, meaning its returns are costly for two compounding reasons rather than one.
- A couple of categories show the opposite pattern — high return rates but low dollar impact — because their baseline profitability is low to begin with, so frequent returns don't translate into much lost revenue.

## Business Conclusion/Recommendation
Pulling both questions together, four things stand out:
- Profitability in this store isn't one thing — some categories win through volume and price point, others through pricing efficiency, and treating them the same would miss the more useful lever for each. The volume-driven category likely has room to test a modest price increase without much impact on demand, while the margin-efficient category is a stronger candidate for growth investment, since each additional dollar of its revenue converts to profit better than most others.
- Discounting isn't a meaningful driver of returns here — confirmed at both the individual-transaction and category level, with neither showing a statistically meaningful relationship. Discount decisions can be made on sales and marketing grounds alone, without factoring in return risk.
- Returns aren't a uniform problem across categories either. One category combines an elevated return rate with strong margins, making it the clearest candidate for a root-cause investigation into quality, sizing, or packaging. Another has the best return rate in the store but the highest dollar cost per return, simply because of its price point — there, the better fix is tightening the return-handling process itself (freshness windows, damage-in-transit checks), not trying to lower a rate that's already strong.
- The broader takeaway: no single metric tells the full story here. Dollar profit, percentage margin, and return rate each surface a different pattern, and several categories only reveal their real risk or strength once more than one of those numbers is read together.


## Repository Structure
```
├── retail_data/       # Raw CSVs and SQLite database
├── notebooks/         # SQL + pandas analysis notebook(s)
├── outputs/           # Exported charts and result tables
├── requirements.txt   # Python dependencies
└── README.md
```

## How to Reproduce
1. Clone this repo: `git clone <your-repo-url>`
2. Create and activate a virtual environment: `python -m venv venv`
3. Install dependencies: `pip install -r requirements.txt`
4. Open the notebook in `notebooks/` and run the cells in order

## Limitations
- Regional sample sizes are uneven (e.g., only 9 customers from the Black Sea region vs. 566 from Marmara), so regional comparisons should be read with caution
- Dollar-based profit figures (`TotalProfit`, `WeightedPerUnitMargin`) are nominal, not inflation-adjusted. Prices compound ~10% annually from 2021–2026, and order volume grew substantially over the same period, so multi-year totals reflect cumulative business growth as much as category performance. Percentage margin (`MarginPct`) is unaffected by this — it stays stable (~30-31%) year over year regardless of inflation
- The category-level correlation between discount rate and return rate (r = 0.36) is not statistically significant (p = 0.30, n = 10) — too small a sample to draw a reliable conclusion from on its own. The transaction-level test (r = 0.006, n = 30,271, p = 0.31) is the more trustworthy result and is what this analysis's conclusions rely on

## Author
*Jorge Raphael Co* — *[[LinkedIn Profile]](https://www.linkedin.com/in/jorge-raphael-co)*
