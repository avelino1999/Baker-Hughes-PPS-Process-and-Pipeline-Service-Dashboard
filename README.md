# 📊 Baker Hughes PPS | Process and Pipeline Service Dashboard

An end-to-end Power BI analytics solution designed to track global pipeline inspection operations and pre-commissioning services for Baker Hughes Process and Pipeline Services (PPS). The dashboard transforms 10,000 raw operational records into an interactive view highlighting completion performance, asset integrity risks, and compliance tracking.

---

## 📌 Project Overview & Problem Statement

Field operations across global oil & gas basins generate large volumes of operational logging data. The goal of this project was to:

- **Clean & Standardize Data:** Normalize regional entries, fix data typing errors, and parse inspection tool outputs.
- **Track Key Operational Metrics:** Calculate job volume, execution completion rates, and average corrosion levels.
- **Highlight High-Risk Assets:** Isolate critical defects (Max Wall Loss > 50%) and track safety compliance (`HSE_Audit_Passed`) across active field segments.

---

## 🛠️ Tech Stack & Key Skills Used

- **Business Intelligence:** Microsoft Power BI Desktop
- **Data Engineering (ETL):** Power Query, M Code (`List.Accumulate`, text parsing, data type normalization)
- **Data Analytics:** DAX (Data Analysis Expressions)
- **Visualization:** Executive F-Pattern Dashboard Design, Dual-Axis Line & Column Charts, Global Bubble Mapping, Contextual Slicers

---

## 📊 Dashboard Key Metrics & Layout

| Metric | Value | Business Description |
| :--- | :---: | :--- |
| **Total Jobs** | 10K | Total operational field logs processed globally. |
| **Completion Rate %** | 54.64% | Share of inspection and service runs successfully completed. |
| **Avg Wall Loss %** | 5.59% | Mean defect/corrosion depth across all inspected pipeline segments. |
| **High Risk Defects** | 508 | Total critical instances where pipeline wall loss exceeded safety thresholds ($>50\%$). |

### Visual Layout Breakdown

- **Executive Slicers (Top Ribbon):** Dynamic drop-down filters for `Status` and `Service_Line`.
- **KPI Header Cards:** High-level summary of total operations, completion rate, average degradation, and high-risk alerts.
- **Geographic Distribution Map (Middle Left):** Interactive world map displaying operational density and high-risk defects across regions (North America, Gulf of Mexico, North Sea, Europe, Africa, Asia Pacific).
- **Monthly Execution Trend (Middle Right):** Combined Column & Line chart mapping Total Jobs (Bars) against Completion Rate % (Line) across all 12 months.
- **Actionable Asset Integrity Log (Bottom Table):** Granular field log showing `Job_ID`, `Region`, `Pipeline_Segment`, `Service_Line`, `Max_Wall_Loss_Pct`, `Status`, and `HSE_Audit_Passed`.

---

## 🧮 Core DAX Measures

```dax
-- 1. Total Jobs Count
Total Jobs = COUNTROWS('Baker_Hughes_PPS_10k_Operations_Log')

-- 2. Overall Completion Rate %
Completion Rate % = 
DIVIDE(
    CALCULATE([Total Jobs], 'Baker_Hughes_PPS_10k_Operations_Log'[Status] = "Completed"),
    [Total Jobs],
    0
)

-- 3. High Risk Defect Alerts (>50% Wall Loss)
High Risk Defects = 
CALCULATE(
    [Total Jobs],
    'Baker_Hughes_PPS_10k_Operations_Log'[Max_Wall_Loss_Pct] > 0.50
)

-- 4. Average Pipeline Degradation Depth
Avg Wall Loss % = AVERAGE('Baker_Hughes_PPS_10k_Operations_Log'[Max_Wall_Loss_Pct])
```

---

## 💡 Business Impact & Value Delivered

- **Risk Mitigation:** Surface-level visibility into 508 critical pipeline defects ($>50\%$ wall loss) to prioritize immediate field maintenance and repair ("dig") schedules.
- **Operational Efficiency:** Identified seasonal trends and tracked completion performance ($54.64\%$ average) to optimize field crew allocation.
- **Compliance Oversight:** Integrated HSE audit results directly into the inspection log to flag unvalidated jobs or safety compliance gaps (e.g., failed audits).

---

## 🚀 How to Run This Project

1. Clone or download this repository.
2. Open `Baker_Hughes_PPS_Operations_Dashboard.pbix` in Power BI Desktop.
3. Use the top slicers (`Status` / `Service_Line`) or click on any region on the map to cross-filter the report dynamically.
