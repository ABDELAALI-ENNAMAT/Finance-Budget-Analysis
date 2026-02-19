# 💰 Finance & Budget Analysis — SQL + Power BI

A complete end-to-end financial analysis project built with **SQL Server** and **Power BI**.  
The project explores a company's revenues, expenses, and departmental performance — turning raw data into actionable insights through relational data modeling, analytical SQL views, and interactive dashboards.

---

## 🔴 Live Dashboard

**👉 [Click here to view the interactive Power BI dashboard](https://app.powerbi.com/reportEmbed?reportId=20206b93-8f19-4666-be09-8eb6d45ca093&autoAuth=true&ctid=2e589d81-ea7a-4dc7-8fb2-84ba95cc947f)**

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| **SQL Server** | Data modeling, relational tables, and KPI views |
| **Power BI** | Multi-page interactive dashboards |
| **DAX** | Profit growth metrics and conditional KPI formatting |
| **CSV** | Source data imported via BULK INSERT |

---

## 📁 Repository Structure

```
Finance-Budget-Analysis/
│
├── Data/
│   ├── departments.csv
│   ├── expenses.csv
│   └── revenues.csv
│
├── Dashboard/
│   ├── Executive Summary.PNG
│   ├── Department Insights.PNG
│   └── Trend Analysis.PNG
│
├── tables.sql
├── views.sql
│
└── README.md
```

| File / Folder | Description |
|---------------|-------------|
| `Data/` | Raw CSV files — departments, revenues, and expenses |
| `Dashboard/` | Exported dashboard screenshots (3 pages) |
| `tables.sql` | Creates the database, tables, and imports CSV data |
| `views.sql` | 8 analytical SQL views used to power the dashboards |
| `README.md` | Project documentation |

---

## 🗄️ Database Schema

Three relational tables form the foundation of this project:

- **Departments** — department IDs and names
- **Revenues** — revenue records linked to departments by date and category
- **Expenses** — expense records linked to departments by date and category

Both `Revenues` and `Expenses` reference `Departments` via a foreign key on `DepartmentID`.

---

## 🔍 SQL Views

All analytical logic lives in `views.sql` — 8 views designed to feed directly into Power BI:

| View | Description |
|------|-------------|
| `vw_MonthlyProfit` | Monthly revenue, expense, and net profit per department |
| `vw_DepartmentExpenses` | Monthly expense breakdown by department and category |
| `vw_RevenueTrends` | Monthly revenue trends by department and category |
| `vw_ExpenseTrends` | Monthly expense trends by department and category |
| `vw_DepartmentSummary` | Total revenue, expense, net profit, and transaction counts |
| `vw_TopSpendingDepartments` | Departments with the highest expenses in the last 12 months |
| `vw_ProfitGrowth` | Month-over-month profit growth rate per department |
| `vw_YearlyComparison` | Year-over-year revenue, expense, and profit per department |

### Example — `vw_TopSpendingDepartments`

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

The Power BI dashboard consists of three comprehensive pages:

**1. Executive Summary** ([Screenshot](Dashboard/Executive%20Summary.PNG))  
Tracks Total Revenue, Total Expenses, and Profit Growth % across the company. DAX measures dynamically color KPIs green for positive growth and red for negative growth.

**2. Department Insights** ([Screenshot](Dashboard/Department%20Insights.PNG))  
Highlights the top spending departments using bar charts and card visuals, with a side-by-side breakdown of actual spending vs. allocated budget.

**3. Trend Analysis** ([Screenshot](Dashboard/Trend%20Analysis.PNG))  
Visualizes monthly revenue trends and profit trajectories through line and scatter charts, including forecast indicators.

---

## ▶️ How to Run

1. **Open SQL Server and run `tables.sql`**
   > ⚠️ Update the file paths in the `BULK INSERT` statements to match your local `Data/` folder location
2. **Run `views.sql`** to create all 8 analytical views
3. **Open Power BI Desktop** and connect to your SQL Server instance
4. **Load the views** as data sources and build your report — or refer to the dashboard screenshots and live link above

---

## 🎯 Key Outcomes

- Designed a normalized **relational database** optimized for financial BI reporting
- Built **8 reusable SQL views** covering profit trends, department summaries, and year-over-year comparisons
- Developed a **3-page Power BI dashboard** with dynamic DAX measures and conditional formatting
- Delivered clear, management-ready insights on revenue performance, cost efficiency, and departmental spending

---

## 👤 Author

**Abdelaali Ennamat**  
Data Analyst | SQL · Power BI · Python

🔗 [LinkedIn](https://www.linkedin.com/in/abdelaali-ennamat) · [GitHub](https://github.com/ABDELAALI-ENNAMAT)
