Advanced SQL & Cohort Analytics Pipeline / Аналитический SQL-пайплайн когортного анализа
English Version
 | 
Русская версия
🇬🇧 English Version
📌 Project Overview
An end-to-end analytical SQL pipeline built with Python, SQLite, and SQLAlchemy to evaluate monthly user cohorts, task completion metrics, and revenue dynamics from relational tables (users, codesubmit, transaction, language).

🏗️ SQL Architecture & CTE Pipeline
The query is architected as an 8-stage modular Common Table Expression (CTE) pipeline:

1. us_agg: Active user percentage grouped by registration month.
2. codesubmit_per_month: Monthly total and successful code submissions.
3. month_revenue: Monthly revenue and running cumulative historical maximum.
4. code_lang: User performance breakdown per programming language.
5. five_perc_prep: Percentile ranking per language using PERCENT_RANK().
6. five_perc: Extracts the 95th percentile threshold.
7. top5per_us: Aggregates top 5% user IDs using GROUP_CONCAT.
8. for_last: Assembles master report and retrieves previous month revenue via LAG().
🛠️ Key Technical Features:
Window Percentiles (PERCENT_RANK() OVER): Dynamically isolates the top 5% performing programmers per language within each monthly cohort.
Time-Series Lookups (LAG() OVER): Accesses prior month revenue without expensive self-joins.
Running Aggregations: Calculates cumulative running revenue max via MAX(SUM(...)) OVER (ORDER BY ...).
String Aggregation (GROUP_CONCAT): Compiles high-performing user IDs into compact relational records.
Note on Dataset: This pipeline was developed and benchmarked on an anonymized, synthetic relational dataset designed to validate complex SQL edge cases and window function logic.

🚀 Quickstart
Clone the repository: git clone https://github.com/aleks-analytics/advanced-sql-cohort-pipeline.git
Install dependencies: pip install pandas sqlalchemy matplotlib seaborn plotly
Launch the notebook: jupyter notebook
