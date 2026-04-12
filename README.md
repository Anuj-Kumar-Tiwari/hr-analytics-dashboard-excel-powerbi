<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=28&pause=1000&color=E53935&center=true&vCenter=true&width=700&lines=HR+Analytics+Dashboard;Power+BI+%2B+DAX+Portfolio+Project;Decoding+Employee+Attrition+Patterns" alt="Typing SVG" />
</p>

<br/>

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Excel](https://img.shields.io/badge/Advanced_Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![CSV](https://img.shields.io/badge/IBM_HR_Dataset-FF6F00?style=for-the-badge&logo=files&logoColor=white)

<br/>

> **Analyzed attrition patterns across 1,470 IBM employees using Power BI & DAX — revealing a 16.1% attrition rate, with overtime and low salary as the top drivers of 237 exits.**

<br/>

[![LinkedIn](https://img.shields.io/badge/Anuj_Kumar_Tiwari-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/anuj-kumar-tiwari-107704208)
[![GitHub](https://img.shields.io/badge/GitHub-Anuj--Kumar--Tiwari-181717?style=flat-square&logo=github)](https://github.com/Anuj-Kumar-Tiwari)
[![Email](https://img.shields.io/badge/Email-anuujji@gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:anuujji@gmail.com)

</div>

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [KPI Summary](#-kpi-summary)
- [Dataset](#-dataset)
- [DAX Measures](#-dax-measures)
- [Dashboard](#-power-bi-dashboard)
- [Key Insights](#-key-insights)
- [How to Run](#-how-to-run)
- [Tech Stack](#-tech-stack)

---

## 🎯 Project Overview

This is an **end-to-end HR Analytics project** using the IBM HR Employee Attrition dataset. The objective was to identify key drivers of employee attrition, compute HR KPIs using DAX measures in Power BI, and deliver an interactive dashboard that HR teams can use for real-time workforce monitoring.

```
📦 IBM HR Dataset   →   🛠️ Power BI + DAX   →   📊 Interactive HR Dashboard
  1,470 employees        8+ DAX Measures          Attrition KPI Cards
  35 columns             Data Cleaning             Slicers + Drill-down
  Attrition Labels       Power Query               Department Analysis
```

---

## 💰 KPI Summary

<div align="center">

| 📊 Metric | 🔢 Value |
|:---|:---:|
| 👥 Total Employees | **1,470** |
| 🚪 Total Attrition | **237 employees** |
| 📉 Overall Attrition Rate | **16.1%** |
| 💵 Avg Monthly Income (Left) | **$4,787** |
| 💵 Avg Monthly Income (Stayed) | **$6,833** |
| ⏱️ Overtime-Driven Exits | **127 / 237 (53.6%)** |
| 💸 Low Salary Exits (≤$5K) | **163 / 237 (68.8%)** |
| 🔢 Avg Age — Employees Who Left | **33.6 years** |

</div>

---

## 🗂️ Dataset

The dataset is the **IBM HR Analytics Employee Attrition & Performance** dataset — a fictional but realistic HR dataset widely used for workforce analytics.

```
Source File:  WA_Fn-UseC_-HR-Employee-Attrition.csv
Table Name:   HR (renamed in Power BI)
Rows:         1,470 employees
Columns:      35 attributes
Target:       Attrition (Yes / No)
```

### 📋 Key Columns

| Column | Type | Description |
|--------|------|-------------|
| Attrition | Text | Whether the employee left (Yes / No) |
| Department | Text | Human Resources / Research & Development / Sales |
| JobRole | Text | 9 roles — Lab Technician, Sales Executive, etc. |
| MonthlyIncome | Number | Monthly salary ($1,009 – $19,999) |
| OverTime | Text | Whether employee works overtime (Yes / No) |
| MaritalStatus | Text | Single / Married / Divorced |
| Age | Number | Employee age (18–60) |
| YearsAtCompany | Number | Tenure at the company |
| JobSatisfaction | Number | Satisfaction score 1–4 |
| WorkLifeBalance | Number | Work-life balance score 1–4 |
| BusinessTravel | Text | Travel frequency category |
| EducationField | Text | Field of education background |

### 🧹 Columns Removed (Data Cleaning)
The following redundant columns were removed during Power Query cleaning:

```
❌ EmployeeCount    → All values = 1 (constant, no analytical value)
❌ StandardHours    → All values = 80 (constant)
❌ Over18           → All values = 'Y' (constant)
❌ DailyRate        → Redundant rate column
❌ HourlyRate       → Redundant rate column
❌ MonthlyRate      → Redundant rate column
```

---

## 🛠️ DAX Measures

All KPI measures were written in DAX inside Power BI. Key measures:

<details>
<summary><b>📋 Click to expand — Full DAX Measure List</b></summary>

<br/>

```dax
-- 1. Total Employees
Total Employees = COUNT(HR[EmployeeNumber])

-- 2. Total Attrition
Total Attrition = COUNTROWS(FILTER(HR, HR[Attrition] = "Yes"))

-- 3. Attrition Rate
Attrition Rate = DIVIDE([Total Attrition], [Total Employees], 0)

-- 4. Active Employees
Active Employees = [Total Employees] - [Total Attrition]

-- 5. Avg Monthly Income
Avg Monthly Income = AVERAGE(HR[MonthlyIncome])

-- 6. Low Salary Attrition Rate
Low Salary Attrition =
CALCULATE(
    [Total Attrition],
    HR[MonthlyIncome] <= 5000
)

-- 7. Overtime Attrition Count
Overtime Attrition =
CALCULATE(
    [Total Attrition],
    HR[OverTime] = "Yes"
)

-- 8. Dept-wise Attrition Rate
Dept Attrition Rate =
DIVIDE(
    CALCULATE([Total Attrition]),
    CALCULATE([Total Employees]),
    0
)
```

</details>

<br/>

| # | Measure | Formula Type | Result |
|---|---------|-------------|--------|
| 1 | Total Employees | COUNT | 1,470 |
| 2 | Total Attrition | COUNTROWS + FILTER | 237 |
| 3 | Attrition Rate | DIVIDE | 16.1% |
| 4 | Active Employees | Subtraction measure | 1,233 |
| 5 | Avg Monthly Income | AVERAGE | $6,503 overall |
| 6 | Low Salary Attrition | CALCULATE + Filter | 163 exits |
| 7 | Overtime Attrition | CALCULATE + Filter | 127 exits |
| 8 | Dept Attrition Rate | DIVIDE + CALCULATE | Per-dept % |

---

## 📊 Power BI Dashboard

The `HR_Dashboard.pbix` file contains an **interactive single-page HR Analytics dashboard** with slicers for Department, Gender, and Salary Slab.

### Visuals Included

| Visual | Chart Type | Insight |
|--------|-----------|---------|
| Attrition KPI Cards | Card Visuals | Total: 237 exits, Rate: 16.1% |
| Dept-wise Attrition | Donut Chart | Sales highest at 20.6% |
| Attrition by Job Role | Bar Chart | Lab Technician #1 (62 exits) |
| Attrition by Salary Slab | Bar Chart | Upto $2.5K highest exit rate |
| Attrition by Age Group | Line / Bar | Avg exit age: 33.6 yrs |
| Attrition by Gender | Donut Chart | Male: 150 exits, Female: 87 |
| Attrition by Marital Status | Bar Chart | Single employees: 120 exits (50.6%) |
| Overtime vs Non-Overtime | Bar Chart | OT employees: 127 exits (53.6%) |
| Attrition by Education Field | Bar Chart | Life Sciences: 89 exits |

### Slicers / Filters
- 🏢 Department (HR / R&D / Sales)
- ⚧️ Gender (Male / Female)
- 💰 Salary Slab (Upto 2.5K / 2.5K–5K / 5K–10K / 10K+)

---

## 💡 Key Insights

```
📉  ATTRITION RATE    →  16.1% overall (237 out of 1,470 employees)
🏢  TOP DEPT          →  Sales has highest attrition rate at 20.6%
👤  TOP ROLE          →  Laboratory Technician — 62 exits (#1)
⏱️  OVERTIME IMPACT   →  127 of 237 exits worked overtime (53.6%)
💸  SALARY DRIVER     →  163 of 237 exits earned ≤$5K/month (68.8%)
💰  INCOME GAP        →  Employees who left earned $2,046 less/month vs those who stayed
👥  GENDER            →  Male attrition: 150 exits; Female: 87 exits
💍  MARITAL STATUS    →  Single employees account for 50.6% of all exits (120/237)
🎓  EDUCATION         →  Life Sciences background: 89 exits (most affected field)
📅  TENURE            →  Avg years at company before leaving: 5.1 years
✈️  TRAVEL            →  Travel_Frequently employees: 69 exits
```

---

## 🚀 How to Run

### Step 1 — Open in Power BI Desktop

```
1. Open HR_Dashboard.pbix in Power BI Desktop
2. Go to: Home → Transform Data → Data Source Settings
3. Update the file path to your local WA_Fn-UseC_-HR-Employee-Attrition.csv
4. Click Refresh → Dashboard loads with live data
5. Use slicers to filter by Department, Gender, and Salary Slab
```

### Step 2 — Explore DAX Measures

```
1. In Power BI Desktop → Go to 'Report' view
2. Open the Fields pane on the right
3. All DAX measures are listed under the HR table
4. Click any measure → Edit in formula bar to review DAX logic
```

### Step 3 — Recreate from CSV (Optional)

```
1. Load WA_Fn-UseC_-HR-Employee-Attrition.csv into Power BI
2. Rename table to 'HR' in Power Query
3. Remove redundant columns (EmployeeCount, StandardHours, Over18, rate cols)
4. Create the 8 DAX measures listed above
5. Build visuals from scratch using the dashboard layout
```

---

## 🗃️ Project Structure

```
📁 HR-Analytics-Dashboard/
│
├── 📊 HR_Dashboard.pbix                         # Power BI dashboard file
├── 📄 WA_Fn-UseC_-HR-Employee-Attrition.csv     # IBM HR source dataset (1,470 rows)
├── 📄 HR-Employee-Attrition.xlsx                # Excel version of cleaned data
├── 📄 HR-Employee-Attrition-Data.csv            # Cleaned CSV for reference
├── 📝 README.md                                  # This documentation
└── 📋 HR_Analytics_Report.pdf                   # Project analysis report
```

---

## 🛠️ Tech Stack

<div align="center">

| Tool | Purpose |
|------|---------|
| ![Power BI](https://img.shields.io/badge/-Power%20BI-F2C811?logo=powerbi&logoColor=black&style=flat-square) | Interactive dashboard & data visualizations |
| **DAX** | 8+ KPI measures — Attrition Rate, Salary Analysis, OT Impact |
| **Power Query** | Data cleaning — removed redundant columns, fixed types |
| ![Excel](https://img.shields.io/badge/-Excel-217346?logo=microsoft-excel&logoColor=white&style=flat-square) | Pivot Table cross-analysis (Dept × Attrition) |

</div>

---

## 📬 Connect with Me

<div align="center">

If you found this project useful, feel free to ⭐ **star the repo** and connect!

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Anuj_Kumar_Tiwari-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/anuj-kumar-tiwari-107704208)
[![GitHub](https://img.shields.io/badge/GitHub-Anuj--Kumar--Tiwari-181717?style=for-the-badge&logo=github)](https://github.com/Anuj-Kumar-Tiwari)
[![Email](https://img.shields.io/badge/Gmail-anuujji@gmail.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:anuujji@gmail.com)

<br/>

*Made with ❤️ by Anuj Kumar Tiwari — Data Analyst Portfolio Project*

</div>
