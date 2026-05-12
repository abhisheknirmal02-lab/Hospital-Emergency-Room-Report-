# 🏥 Hospital Emergency Room Dashboard
**Power BI · DAX · Healthcare Analytics · Apr 2023 – Oct 2024**


---

## 📌 Project Overview

A multi-page Power BI dashboard analysing **9,216 unique Emergency Room patient visits** over 19 months (April 2023 – October 2024). The project combines advanced DAX calculated columns and measures with a 4-page interactive report — enabling hospital administrators to identify bottlenecks, optimise staffing, and improve patient satisfaction outcomes.

---

## 📊 Key Metrics

| Metric | Value |
|---|---|
| Unique Patients | 9,216 |
| Avg Wait Time | 35.3 minutes |
| Avg Satisfaction Score | 4.99 / 10 |
| Patients Referred | 2,045 |
| Seen Within 30 min | 58.41% |
| Admission Split | ~50% admitted / 50% released |

---

## 🧮 DAX Measures

```dax
No. of patient          = DISTINCTCOUNT('Hospital ER_Data'[Patient Id])

Avg Wait Time           = FORMAT(AVERAGE('Hospital ER_Data'[Patient Waittime]),"0.0") & " Min"

No. of Patients Referred = CALCULATE(
                              COUNTROWS('Hospital ER_Data'),
                              'Hospital ER_Data'[Department Referral] <> "None"
                           )
```

---

## 🧮 DAX Calculated Columns

```dax
-- Admission classification
Admission Status  = IF([Patient Admission Flag] = TRUE, "Admitted", "Not Admitted")
Waittime Status   = IF([Patient Waittime] <= 30, "Within Target", "Target Missed")
Admission Hour    = HOUR('Hospital ER_Data'[Patient Admission Date])

-- Age banding (SWITCH)
Age Group = SWITCH(TRUE(),
    [Patient Age] >= 70, "70-79",
    [Patient Age] >= 60, "60-69",
    [Patient Age] >= 50, "50-59",
    [Patient Age] >= 40, "40-49",
    [Patient Age] >= 30, "30-39",
    [Patient Age] >= 20, "20-29",
    [Patient Age] >= 10, "10-19", "0-9")

-- Hourly interval banding (SWITCH)
Waittime Interval = SWITCH(TRUE(),
    [Admission Hour] < 2,  "01-02",
    [Admission Hour] < 4,  "03-04", ...)

-- Date table columns
Day Name     = FORMAT('Date Table'[Date], "DDD")
Month        = FORMAT('Date Table'[Date], "mmm")
Month Number = MONTH('Date Table'[Date])
Month & Year = [Month] & " " & [Year]
Week Day     = WEEKDAY('Date Table'[Date], 2)
```

---

## 🔍 Analytical Findings

**Wait Time & Satisfaction**
- 41.59% of patients missed the 30-minute target — a key operational gap
- Satisfaction score of 4.99/10 signals room for significant improvement

**Peak Busy Periods**
- Busiest day: **Saturday** (1,377 patients), followed by Friday & Thursday
- Peak hours: **11 AM · 1 PM · 7 PM · 11 PM** — require ample staffing

**Demographics & Referrals**
- Largest age group: **30–39 years** (1,200 patients)
- Top referral: **General Practice** (1,840 cases), then Orthopedics (995)
- Near 50/50 admission split: 4,612 admitted vs 4,604 treated & released

---

## 💡 Business Recommendations

- Increase **Saturday staffing** — highest footfall with longest wait pressures
- Deploy additional triage at **11 AM, 1 PM, 7 PM & 11 PM** to reduce target misses
- Fast-track **General Practice referral pathways** to reduce ER over-reliance
- Launch **patient experience programme** focused on communication & wait transparency
- Investigate the 50/50 admission split — community health outreach may reduce avoidable ER visits

---

## 📋 Dashboard Pages

| Page | Description |
|---|---|
| 1 · Consolidated View | Full-year KPIs, age/gender/race/referral breakdowns, day-hour heatmap |
| 2 · Monthly View | Month & year slicer with daily sparklines and department drill-down |
| 3 · Patient Details | Individual-level drill-through table with all 12 fields |
| 4 · Key Takeaways | Narrative descriptive analysis summary for executives |

---

## 🛠 Tools & Techniques

`Power BI Desktop` `DAX Measures` `DAX Calculated Columns` `Date Table` `Data Modelling`
`KPI Cards` `Sparklines` `Donut Charts` `Bar Charts` `Matrix Heatmap` `Page Navigation` `Drill-through Table`

---

## 📁 Repository Files

| File | Description |
|---|---|
|[Power Bi Report ](https://github.com/abhisheknirmal02-lab/Hospital-Emergency-Room-Report-/blob/main/Hospital%20Emergency%20room%20%20Dashboard.pbit) | Power BI template — 4-page report |
| [Hospital data](https://github.com/abhisheknirmal02-lab/Hospital-Emergency-Room-Report-/blob/main/Hospital%20ER_Data.csv) | Raw dataset — 9,216 rows × 12 columns |
| [DAX Code](https://github.com/abhisheknirmal02-lab/Hospital-Emergency-Room-Report-/blob/main/Hospital%20%20dashboard%20DAX%20Code.xlsx) | All DAX measures & calculated columns |

---

## 🖼️ Dashboard Preview

**Page 1 — Consolidated View**
![Consolidated View]()

**Page 2 — Monthly View**
![Monthly View]()

**Page 3 — Patient Details**
![Patient Details]()

**Page 4 — Key Takeaways**
![Key Takeaways]()

---

📁 `.pbit` template included &nbsp;|&nbsp; 🧮 3 measures · 9 calc. columns &nbsp;|&nbsp; 📦 9,216 records · 12 columns &nbsp;|&nbsp; 📋 4 report pages
