# 👥 HR Employee Attrition Dashboard — Case Study

> **Tools:** Power BI · DAX · Power Query · IBM HR Dataset  
> **Type:** People Analytics | Business Intelligence  
> **GitHub:** [View Project](https://github.com/asgeek96/HR-Employee-Attrition-Dashboard)

---

## 📌 The Business Problem

Employee attrition is one of the most expensive and disruptive challenges any organisation faces. Replacing a single employee can cost anywhere between 50% to 200% of their annual salary — yet most HR teams lack the visibility to act before people leave.

The question this project set out to answer was simple:

> **"Who is leaving, why are they leaving, and what can the business do about it?"**

Without clear data, HR decisions rely on gut feeling. With the right dashboard, they can become proactive, targeted, and measurable.

---

## 🎯 Objective

Build an interactive Power BI dashboard that:

- Identifies the **root causes** of attrition across the organisation
- Surfaces **high-risk employee segments** before they resign
- Gives HR and business leaders **actionable KPIs** they can monitor monthly
- Replaces static spreadsheet reports with a **self-service analytics tool**

---

## 📊 The Dataset

- **Source:** IBM HR Analytics Dataset (publicly available)
- **Size:** 1,470 employee records
- **Features:** 35 attributes including department, job role, salary, overtime, satisfaction scores, tenure, and age
- **Attrition Rate:** 16.1% overall — significantly above the healthy industry benchmark of 10–12%

---

## 🏗️ Approach

### Step 1 — Understanding the Data

Before building anything, I spent time understanding what the data was actually telling me. Key questions I explored:

- Which departments had the highest attrition?
- Was overtime correlated with leaving?
- Did salary level predict attrition risk?
- Were newer employees leaving faster than tenured ones?

This exploratory phase shaped every design decision in the dashboard.

### Step 2 — Data Preparation in Power Query

The raw dataset needed several transformations before it was analysis-ready:

- **Age group binning** — created custom age bands (18–25, 26–35, 36–45, 46+) to enable generational analysis
- **Tenure segmentation** — grouped years at company into bands (0–2, 3–5, 6–10, 10+)
- **Custom columns** — created Income Gap column comparing monthly income of leavers vs stayers per role
- **Data type corrections** — ensured satisfaction scores and rating fields were treated as numeric, not text

### Step 3 — Data Modelling

Built a clean single-table model with calculated columns feeding all visuals. Key model decisions:

- Separated attrition flag into a calculated measure rather than a filter for more flexible DAX
- Created a disconnected table for dynamic KPI switching
- Ensured all slicers were cross-filtered correctly to avoid double-counting

### Step 4 — DAX Measures

Built 12 core DAX measures to power the dashboard:

```dax
-- Attrition Rate
Attrition Rate = 
DIVIDE(
    COUNTROWS(FILTER('HR_Data', 'HR_Data'[Attrition] = "Yes")),
    COUNTROWS('HR_Data'),
    0
)

-- Overtime Attrition Rate
Overtime Attrition Rate = 
CALCULATE(
    [Attrition Rate],
    'HR_Data'[OverTime] = "Yes"
)

-- Income Gap (Leavers vs Stayers)
Income Gap = 
CALCULATE(AVERAGE('HR_Data'[MonthlyIncome]), 'HR_Data'[Attrition] = "No") -
CALCULATE(AVERAGE('HR_Data'[MonthlyIncome]), 'HR_Data'[Attrition] = "Yes")

-- Tenure Comparison
Avg Tenure Leavers = 
CALCULATE(
    AVERAGE('HR_Data'[YearsAtCompany]),
    'HR_Data'[Attrition] = "Yes"
)
```

### Step 5 — Dashboard Design

Built a **2-page Power BI report:**

**Page 1 — Executive Overview**
- Overall attrition rate KPI card
- Attrition by department (bar chart)
- Attrition by job role (ranked bar)
- Age group attrition heatmap
- Key filters: Department, Gender, Job Role

**Page 2 — Deep Dive Analysis**
- Overtime vs Non-Overtime attrition comparison
- Satisfaction matrix (Job, Environment, Relationship, Work-Life)
- Income gap by role (leavers vs stayers)
- Tenure analysis of leavers
- Conditional formatting throughout — red/amber/green for instant readability

---

## 📈 Key Findings

### Finding 1 — Overtime is the Strongest Attrition Predictor
Employees working overtime leave at **30.5%** vs **10.4%** for non-overtime employees — nearly **3× the rate**. This single insight alone justifies the entire project. If the business can reduce mandatory overtime for high-risk roles, it directly reduces attrition.

### Finding 2 — Sales Representatives are the Highest Risk Role
Sales Representatives had an attrition rate of **39.8%** — the highest of any role in the organisation. Combined with below-average salaries for the role, this points to a compensation and workload imbalance.

### Finding 3 — Income Gap is a Silent Driver
Employees who left earned on average **$2,046/month less** than employees who stayed in equivalent roles. This income gap was consistent across departments, suggesting salary competitiveness is a systemic issue rather than a department-specific one.

### Finding 4 — Early Tenure Employees Leave Fastest
The highest attrition cluster is employees with **0–2 years tenure**. This points to onboarding and early engagement gaps — new employees are not finding enough reason to stay beyond their first year.

### Finding 5 — Low Job Satisfaction Multiplies Risk
When overtime + low job satisfaction score (1–2) are combined, attrition risk exceeds **45%**. This combination is the highest-risk employee profile in the dataset.

---

## 💡 Business Recommendations

Based on the analysis, three targeted interventions would have the highest ROI:

1. **Audit overtime policies for Sales and R&D** — these two departments drive the most attrition and show the highest overtime rates
2. **Salary review for Sales Representatives** — the $2,046 income gap suggests the market rate has moved and compensation hasn't kept pace
3. **Strengthen onboarding for 0–2 year employees** — structured 90-day and 6-month check-ins would help identify disengagement before it becomes resignation

---

## 🛠️ Technical Stack

| Component | Technology |
|---|---|
| Data Source | IBM HR Dataset (CSV) |
| Data Preparation | Power Query (M language) |
| Data Model | Single-table + calculated columns |
| Calculations | DAX (12 measures) |
| Visualisation | Power BI Desktop |
| Report Pages | 2-page interactive report |
| Interactivity | Cross-page slicers, conditional formatting, satisfaction matrix |

---

## 🧠 What I Learned

- **Business framing matters more than technical complexity.** The most impactful insight in this project — the 3× overtime attrition rate — required a single DAX measure and a bar chart. The value was in asking the right question, not building complex models.
- **Conditional formatting is underused.** Applying red/amber/green formatting to the satisfaction matrix made patterns instantly visible without a single number needing to be read.
- **Power Query transformations are invisible but critical.** The age group binning and tenure segmentation in Power Query are what made the deeper analysis possible. Without clean, structured data, the DAX measures would have returned misleading results.

---

## 📂 Project Structure

```
HR-Employee-Attrition-Dashboard/
│
├── data/
│   └── HR_Analytics.csv
│
├── powerbi/
│   └── HR_Attrition_Dashboard.pbix
│
├── screenshots/
│   ├── HR Employee Attrition.png
│   └── Deep Dive Analysis.png
│
├── docs/
│   └── case-study.md          ← This file
│
└── README.md
```

---

## 🔗 Links

- **GitHub Repository:** [HR-Employee-Attrition-Dashboard](https://github.com/asgeek96/HR-Employee-Attrition-Dashboard)
- **LinkedIn:** [Anubhav Srivastava](https://www.linkedin.com/in/asgeek)

---

*Built by Anubhav Srivastava — Data Analyst | Business Intelligence | Power BI*
