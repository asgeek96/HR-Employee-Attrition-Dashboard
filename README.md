# HR Employee Attrition Dashboard
**Tool:** Power BI | **Dataset:** IBM HR Analytics (1,470 employees, 35 features)

A two-page interactive Power BI dashboard analysing employee attrition patterns across roles, departments, age groups, compensation, and satisfaction scores — built to surface actionable retention insights for HR and business leadership.

---

## Dashboard Pages

### Page 1 — Executive Overview
High-level KPIs and attrition breakdown by role, department, age group, and overtime status.

### Page 2 — Deep Dive
Satisfaction score comparisons, income and tenure gaps between employees who stayed vs left, and a department-level satisfaction matrix with conditional formatting.

---

## Key Findings

**1. Overtime is the single strongest attrition driver**
Employees working overtime leave at a rate of 30.5% — nearly 3× the 10.4% rate of those without overtime. Recommendation: cap mandatory overtime for high-risk roles, particularly Sales Representatives.

**2. Frontline sales roles are at critical risk**
Sales Representatives have the highest attrition rate at 39.8%, nearly double the company average of 16.1%. Combined with below-average satisfaction scores, this points to structural issues in workload, compensation, or career progression in sales.

**3. A $2,046/month income gap exists between stayers and leavers**
Employees who left earned an average of $4,787/month vs $6,833 for those who stayed — a 30% gap. Tenure also differs significantly: leavers averaged 5.1 years vs 7.4 years for stayers. Targeted compensation reviews for Lab Technicians and Sales Representatives could meaningfully reduce voluntary turnover.

**4. Under-25s are the highest-risk age group**
Employees aged 18–25 leave at a rate of 35.8% — nearly 4× the rate of the most stable group (36–45 at 9.2%). Early-career support structures, mentorship programmes, and clearer promotion paths could reduce attrition in this segment.

---

## Data Limitations

- This is a fictional IBM dataset created for HR analytics practice — findings are illustrative, not based on a real company
- Satisfaction scores are self-reported on a 1–4 scale, which introduces subjectivity
- The dataset is a cross-sectional snapshot; no longitudinal trends can be established
- Causality cannot be inferred — variables like overtime and attrition are correlated but the direction of causality is unclear

---

## Files in This Repository

| File | Description |
|---|---|
| `HR-Employee-Attrition.csv` | Raw dataset (IBM HR Analytics) |
| `HR_Attrition_Dashboard.pbix` | Power BI project file |
| `HR_Attrition_Dashboard.pdf` | Exported dashboard (both pages) |
| `case-study.md ` | Case Study file |
| `README.md` | This file |

---

## DAX Measures Used

```
Attrition Rate = DIVIDE([Employees Left], [Total Employees], 0)

Employees Left = CALCULATE(COUNTROWS('Table'), 'Table'[Attrition] = "Yes")

Overtime Attrition Rate = CALCULATE([Attrition Rate], 'Table'[OverTime] = "Yes")

Avg Income (Stayed) = CALCULATE(AVERAGE('Table'[MonthlyIncome]), 'Table'[Attrition] = "No")

Avg Income (Left) = CALCULATE(AVERAGE('Table'[MonthlyIncome]), 'Table'[Attrition] = "Yes")
```

---

## Tools & Skills Demonstrated

- Power BI Desktop (data modelling, DAX, report design)
- Power Query (data type validation, custom columns, age group binning)
- Conditional formatting (rule-based color coding on charts and matrix)
- DAX measures (CALCULATE, DIVIDE, AVERAGE, COUNTROWS)
- Data storytelling (insight-led layout, analyst brief)

---

## Dataset Source

IBM HR Analytics Employee Attrition & Performance — available on [Kaggle](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset)
