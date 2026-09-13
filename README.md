# Power BI Management Reporting: KMU Demo

> End-to-end analytics solution for SME management reporting: from raw Excel data to a star schema model and a DAX-driven dashboard for owner-led companies (KMU/Mittelstand) that have outgrown manual reporting.

---

## Project Overview

This project demonstrates an end-to-end management reporting pipeline for a synthetic DACH company with 4 business segments across 5 regions, tracking plan/actual revenue, EBIT, order intake, and headcount costs.

**Data:** Artificial / synthetic dataset  
**File:** `pbix/Management-Report-Demo.pbix`

---

## Tech Stack

`Power BI` · `Power Query (M)` · `Star Schema Modeling` · `DAX`

---

## Pipeline

### 1. Extract
- Monthly Excel exports with one sheet per reporting period
<img width="1922" height="1080" alt="Screenshot 2026-08-31 at 20 49 24" src="https://github.com/user-attachments/assets/19449242-7025-482b-bd09-c1d09377e702" />

### 2. Transform (`Power Query`)
- Centralized workbook connection via `fx_Workbook`
- Automatic identification of valid monthly sheets via `fnIstMonatsblatt`
- Sheet transformation and reporting date extraction via `fnTransformBlatt`

### 3. Load & Model (Power BI)
- Star-schema dimensional data model
- Fact table containing KPI values and dimension keys
- Daily-grain `Dim_Datum` for time intelligence
- `Dim_Regionen` including coordinates for map visuals

### 4. Report & Analyse
- DAX-driven management KPIs
- Plan/actual and variance analysis
- Dynamic K€/Mio.€ formatting
- Conditional arrows and colour indicators

---

## Data Model

<img width="994" height="318" alt="Screenshot 2026-09-13 at 15 17 54" src="https://github.com/user-attachments/assets/2c7cec8d-8ef0-4339-99df-88ed89a24988" />

Monthly Excel exports are transformed into a clean star schema. The fact table holds only keys and KPI values. `Dim_Datum` is built at daily grain so `DATEADD`-based time intelligence returns correct results. `Dim_Regionen` includes coordinates for the map visual.

---

## Dashboard

<img width="1202" height="716" alt="Screenshot 2026-09-06 at 21 05 53" src="https://github.com/user-attachments/assets/e2c09bb3-42cb-42c7-a975-2ad2aceb8eb6" />

<img width="1206" height="523" alt="Screenshot 2026-09-06 at 22 14 50" src="https://github.com/user-attachments/assets/a744af9c-f2a5-422e-b46e-dd3c0339448b" />

---

## Key Highlights

- Daily-grain date dimension for reliable `DATEADD` time intelligence
- Fixed a duplicate key relationship error by replacing a concatenated text key with a proper date key
- Ingestion logic automatically scales to new months and years
- Dynamic K€/Mio.€ display formatting and conditional arrow/colour indicators via `SWITCH(TRUE(), ...)` and `UNICHAR`

---

## Repository Structure

    Power-BI-Management-Reporting-Demo/
    ├── pbix/
    │   └── Management-Report-Demo.pbix   # Full demo file
    └── README.md

---

## Data Disclaimer

Artificial dataset created for demonstration purposes only. All company, financial, regional, and operational data is synthetic.

---

## Author

Franziska Meyndt
