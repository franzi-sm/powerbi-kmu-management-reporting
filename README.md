# Power BI Management Reporting: KMU Demo

End to end analytics solution for SME management reporting: from raw Excel data to a star schema model and a DAX driven dashboard for owner led companies (KMU/Mittelstand) that have outgrown manual reporting.

Dataset is synthetic: a DACH company with 4 business segments across 5 regions, tracking plan/actual revenue, EBIT, order intake, and headcount costs.

**Contents:** `pbix/Management-Report-Demo.pbix`, the full demo file.

---

## Pipeline

<img width="1922" height="1080" alt="Screenshot 2026-08-31 at 20 49 24" src="https://github.com/user-attachments/assets/17524b91-b1eb-4bb2-90d8-7a87d1ab97f5" />

Raw Excel exports are ingested, cleaned, and modeled into a star schema, then surfaced in an interactive Power BI cockpit.

## Data Model

<img width="994" height="318" alt="Screenshot 2026-09-13 at 15 17 54" src="https://github.com/user-attachments/assets/2c7cec8d-8ef0-4339-99df-88ed89a24988" />

Monthly Excel exports (one sheet per period) are transformed into a clean star schema. The fact table holds only keys and KPI values. `Dim_Datum` is built at daily grain so `DATEADD` based time intelligence returns correct results. `Dim_Regionen` includes coordinates for the map visual.

## Power Query (M)

- `fx_Workbook` — a single centralized query connecting to the source Excel file, so every other query reads from one point of truth
- `fnIstMonatsblatt` — pattern-matches sheet names to identify valid monthly-data sheets, so new months/years are picked up automatically on refresh
- `fnTransformBlatt` — reshapes each sheet and derives the reporting date directly from the sheet name

---

## Key Highlights

- Daily grain date dimension, required for `DATEADD` time intelligence to work correctly
- Fixed a duplicate key relationship error by replacing a concatenated text key with a proper date key
- Ingestion logic scales to new months and years automatically, no query maintenance
- Dynamic K€/Mio.€ display formatting and conditional arrow/color indicators via `SWITCH(TRUE(), ...)` and `UNICHAR`

<img width="485" height="294" alt="image" src="https://github.com/user-attachments/assets/660b27fe-db05-49a3-9f30-7bcc2a29eaf0" />

<img width="403" height="166" alt="image" src="https://github.com/user-attachments/assets/ee3cc129-d472-4d26-b80e-11fa31a480de" />


## Tech Stack

Power BI Desktop, Power Query (M), DAX, Star Schema Modeling

## About

Built by Franziska Meyndt, Business & Data Analytics, freelance Power BI development for SMEs (dashboarding, data modeling, reporting automation).
