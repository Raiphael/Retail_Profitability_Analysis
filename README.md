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
- [Next Steps](#next-steps)
- [Author](#author)

## Project Overview
*[2-3 sentences: what this project does, why you chose it, and the dataset it's built on. Example to adapt: "This project analyzes a relational retail dataset to understand which product categories are actually profitable once discounts and returns are factored in, using SQL for aggregation and Python for deeper transaction-level testing."]*

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
- **Jupyter Notebook** — analysis environment
- **Git / GitHub** — version control and publishing
- *[Add matplotlib / seaborn / Excel here once you decide how you're visualizing]*

## Methodology
1. Framed the business questions above before writing any queries
2. Wrote a SQL query joining `order_details`, `products`, and `categories` to compute revenue, cost, gross profit, margin %, average discount rate, and return rate per category
3. Tested the relationship between discount rate and return likelihood at the individual line-item level in pandas (correlation + return rate by discount bucket)


## Key Findings

- **Most profitable category by margin:** 
- **Most profitable category by total volume:** 
- **Relationship between discount rate and returns:** 
- **Impact of returns on net margin:** 

## Next steps
- 


## Repository Structure
```
├── data/              # Raw CSVs and SQLite database
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

## Author
*Jorge Raphael Co* — *[[LinkedIn Profile]](https://www.linkedin.com/in/jorge-raphael-co)*
