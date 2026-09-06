# Advanced SQL: Multi-CTE Cohort & User Performance Pipeline

[English Version](README.md) | [Русская версия](README_RU.md)

---

### Project Overview
An analytical SQL pipeline written in SQLite and Python (SQLAlchemy, Pandas) to evaluate monthly user retention, task success rates, and revenue trends across multiple relational tables

The query aggregates four relational tables (`users`, `codesubmit`, `transaction`, `language`) into a single monthly cohort report

Key Tasks Solved:
* User activity rates by registration month
* Monthly code submissions versus successful completions
* Cumulative running maximum revenue
* Dynamic identification of the top 5% programmers per language (via `PERCENT_RANK`)
* Filtering cohorts where revenue grew month-over-month (via `LAG`)

---

### SQL Pipeline Architecture

The query logic is divided into 8 modular Common Table Expressions (CTEs):

1. **`us_agg`**: Calculates active user share grouped by registration date (`date_joined`)
2. **`codesubmit_per_month`**: Aggregates total submissions and successful completions per month
3. **`month_revenue`**: Computes monthly revenue and running maximum using `MAX(SUM(...)) OVER (ORDER BY ...)`
4. **`code_lang`**: Groups user submissions and successes by programming language and month
5. **`five_perc_prep`**: Calculates percentile ranks for each user within their language using `PERCENT_RANK()`
6. **`five_perc`**: Identifies the 95th percentile threshold (top 5% cut-off)
7. **`top5per_us`**: Groups top user IDs into a comma-separated string using `GROUP_CONCAT`
8. **`for_last`**: Joins all intermediate CTEs and pulls the prior month's revenue using `LAG()`

The final `SELECT` filters out cohorts that did not achieve positive revenue growth compared to the prior month

---

### Synthetic Data Context
This pipeline was designed and tested on an anonymized dataset to validate complex SQL logic under edge cases (window functions, multi-level CTE joins, string aggregations)

---

### Setup & Run
```bash
git clone https://github.com/aleks-analytics/advanced-sql-cohort-pipeline.git
cd advanced-sql-cohort-pipeline
pip install pandas sqlalchemy matplotlib seaborn plotly
jupyter notebook
