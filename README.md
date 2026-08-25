# Advanced SQL & Cohort Analytics Pipeline / Аналитический SQL-пайплайн когортного анализа

[English Version](#english-version) | [Русская версия](#russian-version)

---

<a name="english-version"></a>
## 🇬🇧 English Version

### 📌 Project Overview
An end-to-end analytical SQL pipeline built with **Python, SQLite, and SQLAlchemy** to evaluate monthly user cohorts, task completion metrics, and revenue dynamics from relational tables (`users`, `codesubmit`, `transaction`, `language`).

### 🏗️ SQL Architecture & CTE Pipeline
The query is architected as an 8-stage modular Common Table Expression (CTE) pipeline:
