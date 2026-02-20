# 💰 Finance & Budget Analysis — SQL + Power BI

<div align="center">

![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-E03A3E?style=for-the-badge&logo=microsoft&logoColor=white)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)

**A complete end-to-end financial analysis solution — transforming raw company data into actionable BI insights through relational database design, 8 analytical SQL views, and a 3-page interactive Power BI dashboard.**

</div>

---

## 🌐 Live Dashboard

> 🔴 **Click the banner below to access the interactive Power BI dashboard:**

<div align="center">

[![Live Dashboard](https://img.shields.io/badge/🚀%20View%20Live%20Dashboard-Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://app.powerbi.com/reportEmbed?reportId=20206b93-8f19-4666-be09-8eb6d45ca093&autoAuth=true&ctid=2e589d81-ea7a-4dc7-8fb2-84ba95cc947f)

**[👉 Open Interactive Dashboard](https://app.powerbi.com/reportEmbed?reportId=20206b93-8f19-4666-be09-8eb6d45ca093&autoAuth=true&ctid=2e589d81-ea7a-4dc7-8fb2-84ba95cc947f)**

</div>

> ⚠️ _Access may require organizational credentials. Hosted on Microsoft Power BI Service._

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Live Dashboard](#-live-dashboard)
- [Tech Stack](#️-tech-stack)
- [Repository Structure](#-repository-structure)
- [Database Schema](#️-database-schema)
- [SQL Views](#-sql-views)
- [Dashboard Pages](#-dashboard-pages)
- [How to Run](#️-how-to-run)
- [Key Outcomes](#-key-outcomes)
- [Author](#-author)

---

## 📌 Overview

This project delivers a full **Finance & Budget Analysis** solution for a multi-department organization, built on a normalized SQL Server database and visualized through Power BI.

The system enables business leaders to:

- 💰 **Track** revenue, expenses, and net profit across departments
- 📊 **Compare** year-over-year and month-over-month financial performance
- 🔍 **Identify** top-spending departments and cost efficiency opportunities
- 📈 **Monitor** profit growth trends with DAX-powered conditional KPI formatting

---

## 🛠️ Tech Stack

<div align="center">

| Technology | Purpose |
|---|---|
| ![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?logo=microsoftsqlserver&logoColor=white) | Relational database, table design & data import |
| ![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?logo=powerbi&logoColor=black) | Multi-page interactive dashboards |
| ![DAX](https://img.shields.io/badge/DAX-E03A3E?logo=microsoft&logoColor=white) | Profit growth metrics & conditional KPI formatting |
| ![CSV](https://img.shields.io/badge/CSV-217346?logo=microsoftexcel&logoColor=white) | Source data imported via BULK INSERT |

</div>

---

## 📁 Repository Structure

```
Finance-Budget-Analysis/
│
├── 📂 Data/
│   ├── departments.csv      ← Department IDs and names
│   ├── expenses.csv         ← Expense records by department & category
│   └── revenues.csv         ← Revenue records by department & category
│
├── 📂 Dashboard/
│   ├── Executive Summary.PNG
│   ├── Department Insights.PNG
│   └── Trend Analysis.PNG
│
├── 📄 tables.sql            ← DB creation, table schema & BULK INSERT
├── 📄 views.sql             ← 8 analytical SQL views
└── 📄 README.md
```

| File / Folder | Description |
|---|---|
| `Data/` | Raw CSV files — departments, revenues, and expenses |
| `Dashboard/` | Exported dashboard screenshots (3 pages) |
| `tables.sql` | Creates the database, tables, and imports CSV data |
| `views.sql` | 8 analytical SQL views used to power the dashboards |
| `README.md` | Project documentation |

---

## 🗄️ Database Schema

Three relational tables form the backbone of this project:

```
┌─────────────────────┐
│     Departments     │
│─────────────────────│
│ DepartmentID (PK)   │
│ DepartmentName      │
└────────┬────────────┘
         │ (FK: DepartmentID)
    ┌────┴────────────────────────┐
    │                             │
    ▼                             ▼
┌──────────────────┐   ┌──────────────────┐
│     Revenues     │   │     Expenses     │
│──────────────────│   │──────────────────│
│ RevenueID (PK)   │   │ ExpenseID (PK)   │
│ DepartmentID(FK) │   │ DepartmentID(FK) │
│ Amount           │   │ Amount           │
│ RevenueDate      │   │ ExpenseDate      │
│ Category         │   │ Category         │
└──────────────────┘   └──────────────────┘
```

Both `Revenues` and `Expenses` reference `Departments` via a foreign key on `DepartmentID`.

---

## 🔍 SQL Views

All analytical logic lives in `views.sql` — **8 views** designed to feed directly into Power BI:

| View | Description |
|---|---|
| `vw_MonthlyProfit` | Monthly revenue, expense, and net profit per department |
| `vw_DepartmentExpenses` | Monthly expense breakdown by department and category |
| `vw_RevenueTrends` | Monthly revenue trends by department and category |
| `vw_ExpenseTrends` | Monthly expense trends by department and category |
| `vw_DepartmentSummary` | Total revenue, expense, net profit, and transaction counts |
| `vw_TopSpendingDepartments` | Departments with the highest expenses in the last 12 months |
| `vw_ProfitGrowth` | Month-over-month profit growth rate per department |
| `vw_YearlyComparison` | Year-over-year revenue, expense, and profit per department |

### 💡 Example — `vw_TopSpendingDepartments`

```sql
CREATE VIEW vw_TopSpendingDepartments AS
SELECT
    departments.DepartmentName,
    SUM(expenses.Amount) AS TotalExpense
FROM departments
INNER JOIN expenses
    ON departments.DepartmentID = expenses.DepartmentID
WHERE expenses.ExpenseDate >= DATEADD(MONTH, -12, GETDATE())
GROUP BY
    departments.DepartmentName;
```

---

## 📈 Dashboard Pages

The Power BI dashboard consists of **three comprehensive pages**:

### 1. 🏢 Executive Summary
[![Screenshot](Dashboard/Executive%20Summary.PNG)](Dashboard/Executive%20Summary.PNG)

Tracks **Total Revenue**, **Total Expenses**, and **Profit Growth %** across the entire company.
- DAX measures dynamically color KPIs 🟢 green for positive growth and 🔴 red for negative growth
- High-level snapshot for C-suite and management reporting

### 2. 🏬 Department Insights
[![Screenshot](Dashboard/Department%20Insights.PNG)](Dashboard/Department%20Insights.PNG)

Highlights the **top-spending departments** with bar charts and card visuals.
- Side-by-side breakdown of actual spending vs. allocated budget
- Drill-through capability for per-department deep dives

### 3. 📉 Trend Analysis
[![Screenshot](Dashboard/Trend%20Analysis.PNG)](Dashboard/Trend%20Analysis.PNG)

Visualizes **monthly revenue trends** and profit trajectories.
- Line and scatter charts with forecast indicators
- Reveals seasonality and growth trajectory patterns

---

## ▶️ How to Run

```bash
# Step 1 — Set up the database
# Open SQL Server Management Studio and run:
tables.sql
# ⚠️ Update BULK INSERT file paths to match your local Data/ folder

# Step 2 — Create all 8 analytical views
views.sql

# Step 3 — Connect Power BI
# Open Power BI Desktop → Get Data → SQL Server
# Connect to your local SQL Server instance

# Step 4 — Load and explore
# Import all 8 views as data sources
# Refer to Dashboard/ screenshots or the live link above
```

---

## 🎯 Key Outcomes

| Achievement | Detail |
|---|---|
| 🗄️ **Normalized Database** | 3-table relational schema optimized for financial BI reporting |
| 🔍 **8 Reusable SQL Views** | Covering profit trends, department summaries & YoY comparisons |
| 📊 **3-Page Power BI Dashboard** | Dynamic DAX measures with conditional KPI formatting |
| 💡 **Management-Ready Insights** | Revenue performance, cost efficiency & departmental spending |

---

## 👤 Author

<div align="center">

**Abdelaali Ennamat**

_Data Analyst | SQL · Power BI · Python_

[![GitHub](https://img.shields.io/badge/GitHub-ABDELAALI--ENNAMAT-181717?style=for-the-badge&logo=github)](https://github.com/ABDELAALI-ENNAMAT)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Abdelaali%20Ennamat-0A66C2?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/abdelaali-ennamat)

</div>

---

<div align="center">

⭐ **If you found this project useful, please consider giving it a star!** ⭐

</div>