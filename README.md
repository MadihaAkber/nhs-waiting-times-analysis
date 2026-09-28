# NHS Elective Care Waiting Times Analysis

## Project Overview

This project analyses **NHS England Referral to Treatment (RTT) elective-care waiting-time data** to explore the size of incomplete waiting lists, long waits, and variation across NHS providers and clinical specialties.

The project demonstrates an end-to-end data analytics workflow using **Python, Pandas, SQL, SQLite, Power BI, Power Query and DAX**.

---

## Business Questions

The analysis was designed to answer:

- How large is the elective-care waiting list?
- What proportion of incomplete pathways have waited more than 18 weeks?
- How many pathways have waited more than 52 weeks?
- How many pathways have waited more than 104 weeks?
- Which NHS providers have the largest waiting lists?
- Which providers have the greatest long-wait burden?
- Which clinical specialties have the largest waiting lists?
- Which specialties have the greatest 52+ week waiting burden?
- Can monthly waiting-list totals be compared reliably across the full reporting period?

---

## Data

**Source:** NHS England Referral to Treatment (RTT) Waiting Times  
**Reporting period:** April 2025 to March 2026  
**Analysis population:** `Part_2` — Incomplete Pathways

The original NHS data contained detailed weekly waiting-time buckets. These were transformed into more useful analytical measures, including:

- Total incomplete pathways
- Waiting 18+ weeks
- Waiting 52+ weeks
- Waiting 104+ weeks

The aggregate treatment-function category `C_999 (Total)` was excluded from specialty-level comparisons so that it was not treated as an individual clinical specialty.

### Data Availability

The full raw and processed datasets are not included in this repository because of GitHub file-size limitations.

The project uses publicly available NHS England RTT waiting-times data.

---

## Tools Used

- **Python** — data preparation and transformation
- **Pandas** — data cleaning, manipulation and validation
- **SQL** — querying and analysis
- **SQLite** — database used for SQL analysis
- **Power Query** — final data transformation
- **Power BI** — interactive dashboard development
- **DAX** — KPI and percentage measures
- **GitHub** — project documentation and portfolio presentation

---

## Project Workflow

### 1. Python Data Preparation

Monthly NHS RTT datasets were combined and inspected using **Python and Pandas**.

The analysis was restricted to:

`Part_2 — Incomplete Pathways`

This was important because the objective was to analyse patients/pathways that were **still waiting for treatment**, rather than combining incomplete pathways with completed pathways.

The detailed weekly waiting-time fields were used to create analytical measures for:

- 18+ week waits
- 52+ week waits
- 104+ week waits

The cleaned dataset was then exported for SQL and Power BI analysis.

---

### 2. SQL Analysis

The cleaned dataset was imported into **SQLite**.

SQL was used to analyse overall waiting-list volume and compare waiting pressures across NHS providers and clinical specialties.

The analysis used:

- `SELECT`
- `WHERE`
- `SUM`
- `COUNT`
- `GROUP BY`
- `ORDER BY`
- `HAVING`
- `LIMIT`
- `ROUND`
- Percentage calculations

SQL analysis included:

- Total incomplete pathways
- 18+ week waits
- 52+ week waits
- 104+ week waits
- Providers with the largest waiting lists
- Providers with high long-wait percentages
- Specialties with the largest waiting lists
- Specialties with the greatest long-wait burden

---

### 3. Data Quality Investigation

An important part of the project was validating the data before interpreting the results.

During analysis, February and March 2026 appeared to show a very large increase in total waiting-list volume.

Further investigation showed that the number of providers represented in the dataset had changed substantially.

Earlier months generally contained approximately **24–40 providers**, while February and March contained approximately **295 providers**.

This meant that the apparent increase could not safely be interpreted as a genuine increase in NHS waiting-list pressure because the underlying reporting coverage had changed.

Therefore, raw monthly totals were **not treated as directly comparable across the full 12-month period**.

This finding demonstrates the importance of investigating changes in the underlying data before drawing conclusions from a time series.

---

## Power BI Dashboard

An interactive Power BI report was developed to communicate the results.

The report includes multiple pages for overall, specialty and provider-level analysis.

### NHS Waiting Times Overview

The overview page presents headline waiting-time indicators, including:

- Total Waiting
- Waiting 18+ Weeks
- Waiting 52+ Weeks
- Waiting 104+ Weeks
- Percentage Waiting 18+ Weeks
- Percentage Waiting 52+ Weeks
- Specialty-level waiting-list comparisons

---

### Specialty Analysis

The Specialty Analysis page allows waiting-list pressure to be compared across clinical specialties.

It includes:

- Specialty-level waiting-list volume
- 18+ week waits
- 52+ week waits
- 104+ week waits
- Percentage waiting 52+ weeks
- Specialty comparison charts
- Interactive filters

This allows both **absolute waiting-list volume** and **long-wait burden** to be investigated.

---

### Provider Analysis

The Provider Analysis page compares waiting-time performance across NHS providers.

It includes:

- Total waiting by provider
- 18+ week waits
- 52+ week waits
- 104+ week waits
- Percentage waiting 52+ weeks
- Provider comparison charts
- Conditional formatting
- Interactive filtering

For percentage-based provider comparisons, waiting-list volume should also be considered so that very small providers do not appear disproportionately important because of small denominators.

---

### Provider Detail

A dedicated **drill-through page** allows individual NHS providers to be investigated in greater detail.

Users can select a provider from the main report and drill through to view:

- Provider-specific KPIs
- Total waiting
- 18+ week waits
- 52+ week waits
- 104+ week waits
- Specialty breakdowns

---

### Interactive Tooltip

A dedicated Power BI tooltip provides additional waiting-time information when users interact with report visuals.

This improves the dashboard's usability while keeping the main report pages clean.

---

## DAX Measures

Several DAX measures were created to support the dashboard.

### Total Waiting

```DAX
Total Waiting =
SUM('NHS_Waiting_Times_Cleaned'[Total All])
```

### Waiting 18+ Weeks

```DAX
Waiting 18+ =
SUM('NHS_Waiting_Times_Cleaned'[Wait_18Plus_Weeks])
```

### Waiting 52+ Weeks

```DAX
Waiting 52+ =
SUM('NHS_Waiting_Times_Cleaned'[Wait_52Plus_Weeks])
```

### Waiting 104+ Weeks

```DAX
Waiting 104+ =
SUM('NHS_Waiting_Times_Cleaned'[Gt 104 Weeks SUM 1])
```

### Percentage Waiting 18+ Weeks

```DAX
% Waiting 18+ =
DIVIDE(
    [Waiting 18+],
    [Total Waiting]
)
```

### Percentage Waiting 52+ Weeks

```DAX
% Waiting 52+ =
DIVIDE(
    [Waiting 52+],
    [Total Waiting]
)
```

---

## Key Analytical Findings

The analysis highlighted several important points:

- A substantial proportion of incomplete pathways were waiting beyond **18 weeks**.
- A smaller but important group of pathways had waits exceeding **52 weeks**.
- **104+ week waits** were considerably less common.
- Waiting-list pressure varied across both **clinical specialties and NHS providers**.
- Looking only at total waiting-list volume does not provide the full picture; long-wait percentages are also useful for identifying areas experiencing greater waiting-time pressure.
- A major change in provider coverage occurred in **February and March 2026**, meaning that the raw monthly totals should not automatically be interpreted as a genuine increase in waiting-list size.

---

## Data Limitations

The reporting coverage was not consistent across the entire 12-month period.

February and March 2026 contained substantially more NHS providers than earlier months.

For this reason, raw monthly totals were not treated as directly comparable across the complete reporting period without further harmonisation of provider coverage.

The dashboard therefore focuses primarily on:

- Waiting-list volume
- Long-wait burden
- Provider comparisons
- Specialty comparisons

rather than presenting a potentially misleading year-long trend.

---

## Skills Demonstrated

This project demonstrates practical experience with:

- Python
- Pandas
- Data cleaning
- Data transformation
- Data validation
- Exploratory data analysis
- SQL
- SQLite
- Data aggregation
- Filtering
- Percentage calculations
- Power Query
- Power BI
- DAX
- KPI development
- Interactive dashboard design
- Drill-through
- Tooltips
- Conditional formatting
- Healthcare data analysis
- Data-quality investigation
- Communicating analytical limitations

---

## Dashboard Screenshots

### NHS Waiting Times Overview

![NHS Waiting Times Overview](screenshots/overview.png)

### Specialty Analysis

![Specialty Analysis](screenshots/specialty.png)

### Provider Analysis

![Provider Analysis](screenshots/provider.png)

---

## Repository Structure

```text
nhs-waiting-times-analysis/
│
├── README.md
│
├── python/
│   └── nhs_waiting_times_analysis.py
│
├── sql/
│   └── NHS_Waiting_Times.db
│
├── powerbi/
│   └── NHS_Waiting_Times.pbix
│
├── screenshots/
│   ├── overview.png
│   ├── specialty.png
│   └── provider.png
│
└── data/
    └── README.md
```

---

## Portfolio Summary

This project demonstrates an **end-to-end healthcare data analytics workflow**.

Raw NHS waiting-time data was cleaned and transformed using **Python and Pandas**, investigated using **SQL and SQLite**, and presented through an interactive **Power BI dashboard** using Power Query and DAX.

A key part of the project was identifying a structural change in provider coverage during February and March 2026. Rather than interpreting the resulting increase in raw totals as a genuine waiting-list trend, the change was investigated and documented as a data-quality limitation.

The project demonstrates not only technical skills in Python, SQL and Power BI, but also the importance of **data validation, critical interpretation and clear communication of analytical limitations**.
