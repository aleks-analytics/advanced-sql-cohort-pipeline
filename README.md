# SQL Cohort & User Performance Analysis

An analytical SQL pipeline written in SQLite and Python (SQLAlchemy, Pandas) to evaluate monthly user retention, task success rates, and revenue trends across multiple relational tables.

---

## Overview

The query processes 4 tables (`users`, `codesubmit`, `transaction`, `language`) into a single monthly cohort report. 

It handles:
- User activity rates by registration month
- Monthly code submissions vs. successful completions
- Cumulative running revenue max
- Dynamic identification of the top 5% programmers per language (via `PERCENT_RANK`)
- Filtering for cohorts where revenue grew month-over-month (via `LAG`)

---

## SQL Pipeline Structure

The logic is broken down into 8 modular Common Table Expressions (CTEs):

1. **`us_agg`**: Calculates active user share grouped by `date_joined` (Year-Month).
2. **`codesubmit_per_month`**: Counts total submissions and successful attempts per month.
3. **`month_revenue`**: Computes monthly revenue and running max via `MAX(SUM(...)) OVER (ORDER BY ...)`.
4. **`code_lang`**: Groups user submissions and successes by programming language and month.
5. **`five_perc_prep`**: Calculates percentile ranks for each user within their language using `PERCENT_RANK()`.
6. **`five_perc`**: Identifies the 95th percentile threshold (top 5% cut-off).
7. **`top5per_us`**: Aggregates top user IDs into a comma-separated list using `GROUP_CONCAT`.
8. **`for_last`**: Joins all intermediate tables and pulls the previous month's revenue using `LAG()`.

The final `SELECT` filters out any cohorts that did not show positive revenue growth compared to the prior month.

---

## Note on Synthetic Data

This pipeline was built and tested on an anonymized synthetic dataset designed to validate edge cases in complex SQL queries (window functions, multi-level CTE joins, string aggregations).

---

## Setup & Execution

```bash
git clone https://github.com/aleks-analytics/advanced-sql-cohort-pipeline.git
cd advanced-sql-cohort-pipeline
pip install pandas sqlalchemy matplotlib seaborn plotly
jupyter notebook
