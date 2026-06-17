# System Performance Analysis: XML & Power BI
## Project Report

**Author:** Jace Cordell  
**Tools:** Python | XML | Power Query (Excel) | Power BI  
**Dataset:** 1,200 simulated system performance records  
**Date Range:** January 2026 – May 2026  
**Operational Statuses:** Active | Maintenance | Inactive

---

## 1. Ask

### Business Question
Which systems are operating at elevated failure risk, what conditions reliably predict risk classification, and how can KPI monitoring be structured to support faster operational decisions?

### Stakeholders
- Systems Operations Management
- Maintenance Planning Teams
- Risk and Reliability Engineering

### Success Metrics
- Identify the environmental thresholds (temperature, pressure) that separate risk classifications
- Understand whether operational status predicts failure risk concentration
- Build a monitoring framework that surfaces high-risk conditions before failure occurs

---

## 2. Prepare

### Data Source
Structured XML dataset generated programmatically in Python to simulate system-performance monitoring data commonly used in engineering and infrastructure environments. The dataset was designed to reflect realistic operational patterns across three system statuses over a five-month observation window.

### Dataset Overview

| Attribute | Value |
|---|---|
| Total records | 1,200 |
| Date range | January 1, 2026 – May 1, 2026 |
| Operational statuses | 3 (Active, Maintenance, Inactive) |
| Risk classifications | 3 (High, Medium, Low) |
| Key metrics | Temperature, Pressure, Failure Risk, Operational Status |

### Fields Collected

| Field | Description |
|---|---|
| `system_id` | Unique system identifier |
| `status` | Operational status (Active / Maintenance / Inactive) |
| `temperature` | System temperature reading |
| `pressure` | System pressure reading |
| `failure_risk` | Risk classification (High / Medium / Low) |
| `date` | Date of record |

---

## 3. Process

### XML Ingestion (Power Query)

The dataset was delivered as a structured XML file. Power Query was used to parse the nested XML structure and transform it into a flat tabular format suitable for analysis and visualization in Power BI.

### Cleaning Steps

| Issue | Action |
|---|---|
| Nested XML structure | Expanded and flattened via Power Query column expansion |
| Column data type mismatches | Standardized — `temperature` and `pressure` to decimal, `date` to date type |
| Invalid or out-of-range values | Removed records with null or implausible sensor readings |
| Risk indicator field | Validated classification consistency across all 1,200 records |

### Feature Engineering

A calculated `risk_indicator` column was added to support visual encoding and filtering in Power BI, mapping the three risk classifications to a numeric severity scale for conditional formatting in KPI cards and table visuals.

**Final record count after cleaning: 1,200**

---

## 4. Analyze

### 4.1 Fleet Overview (January – May 2026)

| KPI | Value |
|---|---|
| Total systems monitored | 1,200 |
| Average system temperature | 85.04° |
| High-risk systems | 574 (47.83%) |
| Medium-risk systems | 377 (31.42%) |
| Low-risk systems | 249 (20.75%) |

Nearly half of all monitored systems (47.83%) were classified as High Risk during the observation window — a significant finding that points to systemic operational stress rather than isolated failures.

---

### 4.2 Risk Distribution

| Risk Classification | System Count | % of Total |
|---|---|---|
| High | 574 | 47.83% |
| Medium | 377 | 31.42% |
| Low | 249 | 20.75% |

High-risk systems outnumber low-risk systems by more than 2:1, and together High and Medium risk account for 79.25% of all records. This distribution indicates that the majority of systems are operating under conditions that warrant monitoring intervention.

---

### 4.3 Failure Risk Distribution by Operational Status

The most significant finding of this analysis is the clear relationship between operational status and failure risk concentration.

| Status | High-Risk | Low-Risk | Medium-Risk | Total |
|---|---|---|---|---|
| Active | 210 | 81 | 127 | 418 |
| Maintenance | 198 | 85 | 122 | 405 |
| Inactive | 166 | 83 | 128 | 377 |

**Key finding:** High-risk events are disproportionately concentrated in Active and Maintenance statuses. Maintenance-status systems in particular showed nearly as many high-risk events as Active systems (198 vs. 210) despite representing fewer total records — suggesting that systems entering Maintenance are already operating in degraded conditions rather than being flagged proactively.

The ratio of High to Low risk events within the Maintenance group (198:85 = 2.33:1) is nearly identical to the Active group (210:81 = 2.59:1), which reinforces that Maintenance status does not correlate with reduced risk at the time of classification.

---

### 4.4 Temperature Trends by Risk Classification (January – May 2026)

Average temperature readings by month showed consistent separation between risk categories across the entire observation period, with high-risk systems running significantly hotter than medium- and low-risk systems.

| Risk Category | Approximate Avg Temp Range | Trend |
|---|---|---|
| High | ~90–99° | Rising — peaked in May 2026 |
| Medium | ~80–84° | Relatively stable |
| Low | ~70–72° | Stable with slight dip mid-period |

**Key finding:** High-risk system temperatures increased steadily from January through May 2026, approaching 99° by the end of the observation window. This rising trend — not just elevated readings, but an upward trajectory — is the most actionable signal in the dataset. It suggests that without intervention, high-risk systems will continue to accumulate thermal stress.

The separation between High and Medium temperature averages (~8–15°) is sufficiently large to support threshold-based alerting without generating excessive false positives from Medium-risk systems.

---

### 4.5 Temperature as a Risk Predictor

The consistent temperature separation across all five months of data suggests that temperature is a reliable leading indicator of failure risk classification. Systems averaging above approximately 88° were consistently classified as High Risk, while systems below approximately 75° were consistently Low Risk.

This threshold relationship supports the development of automated alert rules that do not require manual risk re-classification.

---

## 5. Share

### Dashboard

An interactive Power BI dashboard was developed to enable real-time operational monitoring across all three risk classifications and operational statuses.

**Dashboard components:**
- **KPI cards** — Average temperature (85.04°), High Risk % (47.83%), Total Systems (1,200)
- **Risk Distribution chart** — Total system counts by risk classification (High: 574, Medium: 377, Low: 249)
- **Avg Temperature by Month and Failure Risk** — Trend lines for all three risk categories, January–May 2026
- **Failure Risk Distribution by Operational Status** — Clustered bar chart comparing High/Medium/Low counts across Active, Maintenance, and Inactive statuses
- **Interactive slicers** — Filter by date range, operational status, and failure risk classification

📊 *Power BI dashboard file: `xml_system_performance_analysis.pbit`*

---

## 6. Act

### Recommendations

**1. Establish temperature-based automated alert thresholds.**

The data demonstrates clear and consistent temperature separation between High, Medium, and Low risk classifications across all five months. Systems averaging above 88° were reliably classified as High Risk. Implementing automated alerts when temperature exceeds this threshold — before a system is formally reclassified — would surface risk earlier in the degradation cycle and allow proactive intervention.

*KPI target: Flag 90% of eventual High-Risk systems via temperature alerts before manual risk reclassification occurs.*

**2. Implement pre-Maintenance inspection protocols for systems showing elevated temperature.**

Maintenance-status systems showed nearly the same High-Risk concentration as Active systems (198 vs. 210), indicating that systems are entering Maintenance in already-degraded states rather than being flagged early. A pre-Maintenance temperature and pressure screening protocol would ensure that the highest-risk systems are prioritized in the maintenance queue rather than processed in arrival order.

*KPI target: Reduce the High-Risk percentage within the Maintenance status group from the current 48.9% to below 35% within two maintenance cycles.*

**3. Develop period-specific resource allocation plans for April–May.**

High-risk system temperatures rose most sharply during April–May 2026, approaching 99° by the end of the observation window. Whether this reflects seasonal demand, aging infrastructure, or accumulated deferred maintenance, it points to predictable peak-stress periods. Pre-positioning maintenance resources and parts inventory ahead of these months would reduce response time when systems begin trending toward high-risk classification.

*KPI target: Reduce the rate of new High-Risk classifications during April–May by 20% in the next observation period through pre-positioned resources.*

**4. Build a composite risk score incorporating both temperature and pressure.**

This analysis focused primarily on temperature as a risk indicator given the data available. The dataset also includes pressure readings, which likely carry independent predictive value. Developing a composite risk score that weights both metrics would reduce false positives from systems that run hot but maintain stable pressure — and catch systems with abnormal pressure before temperature trends catch up.

*KPI target: Pilot composite risk scoring on the Maintenance-status population, where the High/Low ratio is highest, and validate against manually assigned classifications.*

---

## Appendix: Data Cleaning Log

**Source format:** Structured XML (nested elements)  
**Total records ingested:** 1,200  
**Records removed:** None — all records passed validation after type conversion  
**Key transformations:** XML expansion via Power Query, data type standardization, calculated risk indicator column added  
**Date range confirmed:** January 1, 2026 – May 1, 2026 (5-month window)

---

*Built as part of a data analytics portfolio project. All data is simulated for analytical demonstration purposes.*  
*Author: Jace Cordell | [GitHub](https://github.com/jcordell0414) | [LinkedIn](https://www.linkedin.com/in/jcordell0414)*
