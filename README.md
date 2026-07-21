# 🖥️ System Performance Analysis (XML + Power BI)

### Operational Analytics | XML · Power Query · Power BI · Python

---

## Overview

This project demonstrates an end-to-end operational analytics workflow using structured XML data and Power BI. The objective was to simulate the kind of system-performance monitoring used in engineering and aerospace environments — ingesting raw XML, transforming it through Power Query, and building interactive dashboards that surface KPIs, high-risk conditions, and operational trends.

> **Business Question:** *Which systems are operating at elevated risk, what conditions predict failure classification, and how can KPI monitoring be structured to support faster operational decisions?*

---

## Tools Used

| Phase     | Tool                  | Purpose                                                       |
|-----------|-----------------------|---------------------------------------------------------------|
| Generate  | Python                | Scripted creation of 1,000+ simulated system records in XML  |
| Ingest    | Power Query (Excel)   | XML parsing and transformation into tabular structure        |
| Clean     | Power Query           | Column standardization, type conversion, calculated fields   |
| Visualize | Power BI              | Interactive dashboards for KPI monitoring and risk analysis  |

---

## Dataset

The dataset contains 1,000+ simulated system performance records including:

- System ID and operational status (Active, Maintenance, Offline)
- Temperature and pressure readings
- Failure risk classification (Low, Medium, High)
- Date of record

All records were generated programmatically in Python to simulate the kind of structured operational data common in engineering and infrastructure monitoring contexts.

---

## Workflow

**1. XML Data Processing**
Imported XML data into Power Query and transformed nested structures into flat, tabular datasets ready for analysis.

**2. Data Cleaning**
Standardized column data types, removed invalid values, and created calculated risk indicator fields to support classification analysis.

**3. Dashboard Development**
Built interactive Power BI dashboards covering four analytical dimensions:
- KPI cards for average temperature, total system count, and high-risk percentage
- Temperature trend analysis over time, segmented by failure-risk category
- Comparative failure-risk distribution across operational statuses
- Drill-down tabular reporting with interactive slicers and filters

---

## Key Findings

- **High-risk systems consistently showed elevated temperature and pressure readings** relative to low- and medium-risk classifications, confirming these metrics as reliable early indicators of failure risk
- **Maintenance-status systems had a higher concentration of high-risk classifications** than active systems, suggesting that systems entering maintenance are already operating in degraded conditions
- **Temperature trends indicated increased operational risk during peak periods**, with high-risk spikes clustering around specific time windows
- **Comparative analysis revealed a strong relationship between operational status and failure-risk distribution**, supporting the use of status-based monitoring thresholds for automated alerting

---

## Recommendations

1. **Establish temperature and pressure thresholds as automated alert triggers** — the data shows clear separation between risk categories at specific reading levels, making rule-based monitoring feasible.
2. **Prioritize pre-maintenance inspection protocols** for systems approaching Maintenance status, given their elevated risk concentration.
3. **Incorporate time-of-period risk weighting** into operational planning to allocate resources ahead of historically high-risk windows.

---

## Dashboard Preview

[![System Performance Dashboard]](<img width="2560" height="1600" alt="operational_trends_dashboard" src="https://github.com/user-attachments/assets/dea708fd-c10e-4fb9-a8a4-1c184970ec4b" />
)

*Power BI dashboard showing KPI monitoring, risk trend analysis, and failure-risk distribution by operational status.*

---

## Repository Structure

```
xml_system_performance_analysis/
├── system_data                                  # XML source data file
├── xml_system_performance_analysis.pbit         # Power BI template file
├── xml_system_performance_dashboard.png         # Dashboard screenshot
└── README.md
```

---

## Contact

*Jace Cordell — [GitHub](https://github.com/jcordell0414) · [LinkedIn](https://www.linkedin.com/in/jcordell0414)*
