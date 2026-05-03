# 🌾 Agricultural Production Analytics (India)

This repository contains a complete workflow for analyzing **crop production trends in India** using Python (for data cleaning, preprocessing, and exploratory analysis), **SQL** (for query-based exploration), and **Power BI** (for interactive multi-page dashboards).

---

## 📂 Project Structure

- `EDA.ipynb`  
  Jupyter notebook for cleaning, preprocessing, and exploratory analysis of agricultural datasets.
- `Cleaned_Agri.csv`  
  Final cleaned dataset (wide format) used for SQL analysis.
- `ICRISAT-District Level Data - ICRISAT-District Level Data.csv`  
  Raw source dataset from ICRISAT.
- `sql_agri.sql`  
  SQL scripts for database creation and 10 analytical queries.
- `README.md`  
  Documentation for project overview, workflow, and usage.

---

## 📘 Project Overview

AgriData Explorer is an end-to-end **data analytics and visualization project** designed to explore **Indian agricultural data** across states and districts.  
It combines **Python (EDA.ipynb), SQL queries, and Power BI dashboards** to deliver actionable insights into **crop production, yield efficiency, and cultivated area trends**.

---

## 🎯 Problem Statement

India's agricultural data is often **fragmented, inconsistent, and difficult to interpret**, making it challenging for **farmers, policymakers, and researchers** to make informed decisions.  
AgriData Explorer solves this by:
- Cleaning and integrating datasets.  
- Performing **Exploratory Data Analysis (EDA)**.  
- Building **interactive dashboards** for evaluator-friendly insights.

---

## 🚜 Goals

- Perform **district and state-level crop analysis** for production and yield efficiency.  
- Build an interactive **Power BI dashboard** for agricultural metrics.  
- Use **Python and SQL** for data cleaning, transformation, and query-based exploration.  
- Provide **data-driven recommendations** for crop planning and resource allocation.

---

## 🧠 Key Skills Gained

- **Python**: Data Cleaning, Transformation, EDA  
- **SQL**: Querying, Aggregations, CTEs, Window Functions  
- **Power BI**: Data Modeling, Power Query (M), DAX Measures, Interactive Dashboards, Slicer Sync  
- **Visualization**: Correlation & Trend Analysis with Plotly and Seaborn

---

## 📁 Data Sources

**Dataset:** [ICRISAT – District Level Agricultural Data]  
Includes crop, district, and state-level statistics across India from **1966 to 2017**.

**Key Fields:**
- Crop name (Rice, Wheat, Maize, Oilseeds, Millets, Cotton, etc.)  
- Area cultivated (1000 ha)  
- Production (1000 tons)  
- Yield (kg/ha)  
- Year, District, State identifiers

---

## 🧩 Project Architecture

### 1. Data Collection & Cleaning
- Imported raw ICRISAT CSV files.
- Removed irrelevant columns and handled missing values (`-1` → excluded from analysis).
- Exported cleaned dataset (`Cleaned_Agri.csv`) for SQL and dashboard integration.

### 2. Exploratory Data Analysis (`EDA.ipynb`)
- Identified top crop-producing states and districts.
- Analyzed 50-year production trends (Rice, Wheat, Sugarcane, Millets).
- Correlation between **area cultivated vs production**.
- Yield efficiency comparisons across states.

### 3. Database Design (SQL — `sql_agri.sql`)
- Loaded cleaned data into MySQL (`agriculture_dataset` database).
- 10 analytical queries answering key business questions:
  1. Year-wise Trend of Rice Production Across States (Top 3)
  2. Top 5 Districts by Wheat Yield Increase Over the Last 5 Years
  3. States with the Highest Growth in Oilseed Production (5-Year Growth Rate)
  4. District-wise Correlation Between Area and Production for Major Crops
  5. Yearly Production Growth of Cotton in Top 5 Cotton Producing States
  6. Districts with the Highest Groundnut Production in 2017
  7. Annual Average Maize Yield Across All States
  8. Total Area Cultivated for Oilseeds in Each State
  9. Districts with the Highest Rice Yield
  10. Compare the Production of Wheat and Rice for the Top 5 States Over 10 Years

### 4. Power BI Data Transformation (Power Query)
The raw wide-format CSV was reshaped into a **long (unpivoted) format** inside Power Query using the following steps:
- Selected identifier columns (`Dist Code`, `Year`, `State Code`, `State Name`, `Dist Name`) and used **Unpivot Other Columns** to melt all crop columns into rows.
- Extracted `crop` using a custom column formula (correctly handles multi-word crops like `KHARIF SORGHUM`, `PEARL MILLET`, `FINGER MILLET`):
  ```m
  if Text.Contains([Attribute], " AREA") then Text.BeforeDelimiter([Attribute], " AREA")
  else if Text.Contains([Attribute], " PRODUCTION") then Text.BeforeDelimiter([Attribute], " PRODUCTION")
  else if Text.Contains([Attribute], " YIELD") then Text.BeforeDelimiter([Attribute], " YIELD")
  else [Attribute]
  ```
- Extracted `metric` (AREA / PRODUCTION / YIELD) using a separate custom column.
- Removed the original `Attribute` column.
- Changed `Value` data type to **Decimal Number**.
- Filtered out rows where `Value < 0` to exclude missing data encoded as `-1`.

**Final table structure (8 columns):**

| Dist Code | Year | State Code | State Name | Dist Name | Value | crop | metric |
|---|---|---|---|---|---|---|---|
| 1 | 1966 | 14 | Chhattisgarh | Durg | 548 | RICE | AREA |
| 1 | 1966 | 14 | Chhattisgarh | Durg | 185 | RICE | PRODUCTION |
| 1 | 1966 | 14 | Chhattisgarh | Durg | 337.59 | RICE | YIELD |

### 5. Power BI DAX Measures
Custom measures created for chart accuracy:

```dax
Wheat Yield Increase =
CALCULATE(
    MAX('agriculture_dataset cleaned_agri'[Value]) - MIN('agriculture_dataset cleaned_agri'[Value]),
    'agriculture_dataset cleaned_agri'[crop] = "WHEAT",
    'agriculture_dataset cleaned_agri'[metric] = "YIELD",
    'agriculture_dataset cleaned_agri'[Year] >= 2013,
    'agriculture_dataset cleaned_agri'[Year] <= 2017
)

Oilseed Growth Rate =
DIVIDE(
    CALCULATE(SUM('agriculture_dataset cleaned_agri'[Value]), 'agriculture_dataset cleaned_agri'[Year]=2017) -
    CALCULATE(SUM('agriculture_dataset cleaned_agri'[Value]), 'agriculture_dataset cleaned_agri'[Year]=2013),
    CALCULATE(SUM('agriculture_dataset cleaned_agri'[Value]), 'agriculture_dataset cleaned_agri'[Year]=2013)
) * 100

Crop Area = CALCULATE(SUM('agriculture_dataset cleaned_agri'[Value]), 'agriculture_dataset cleaned_agri'[metric]="AREA")

Crop Production = CALCULATE(SUM('agriculture_dataset cleaned_agri'[Value]), 'agriculture_dataset cleaned_agri'[metric]="PRODUCTION")
```

### 6. Power BI Dashboard (3 Pages)

#### Page 12 — Trends
Line charts showing production and yield trends over time:
- Year-wise Trend of Rice Production (Top 3 States)
- Annual Average Maize Yield Across All States
- Yearly Production Growth of Cotton in Top 5 Cotton Producing States

#### Page 13 — Bar Charts
Bar charts for district and state-level comparisons:
- Top 5 Districts by Wheat Yield Increase Over the Last 5 Years
- States with the Highest Growth in Oilseed Production (5-Year Growth Rate)
- Districts with the Highest Rice Yield
- Districts with the Highest Groundnut Production in 2017
- Total Area Cultivated for Oilseeds in Each State
- Production of Wheat and Rice for the Top 5 States Over 10 Years

#### Page 14 — Correlation
- District-wise Correlation Between Area and Production for Major Crops (RICE, WHEAT, MAIZE) — Scatter chart

---

## 📊 Power BI Features

- **Unpivoted Data Model:** Long-format table with `crop`, `metric`, `Value` columns enabling dynamic cross-filtering.
- **Visual-level Filters:** Each chart is independently filtered by `crop` and `metric` (e.g., Rice chart locked to `crop=RICE`, `metric=PRODUCTION`).
- **Interactive Slicers:** Year (range slider), State Name, Dist Name, Crop, Metric — all synced across all 3 pages.
- **Slicer Sync:** View → Sync Slicers used to synchronize all slicers across Pages 12, 13, 14.
- **Edit Interactions:** Charts on the same page are set to **Filter** mode so clicking a state/district filters all other visuals.
- **Top N Filters:** Applied on State Name / Dist Name fields to show Top 3 / Top 5 / Top 10 automatically.
- **DAX Measures:** Custom measures for yield increase and growth rate calculations.
- **KPI Cards:** Total Production, Total Area, Average Yield displayed at the top of the dashboard.

---

## 🧑‍🤝‍🧑 Target Users

- **Farmers:** Optimize crop selection based on yield efficiency.  
- **Policymakers:** Identify low-productivity regions & plan interventions.  
- **Researchers:** Study long-term agricultural trends and climate impacts.

---

## 📈 Project Deliverables

- `EDA.ipynb` — Python notebook for cleaning & EDA  
- `sql_agri.sql` — SQL scripts for database creation & 10 analytical queries  
- Power BI dashboard (3-page interactive report)  
- `Cleaned_Agri.csv` — Final cleaned dataset  
- `README.md` — Project documentation

---

## 🛠️ Tech Stack

| Component        | Tool / Language                          |
|------------------|------------------------------------------|
| Data Cleaning    | Python (Pandas, NumPy)                   |
| EDA              | Jupyter Notebook (`EDA.ipynb`)           |
| Database         | MySQL                                    |
| Data Modeling    | Power Query (M Language)                 |
| DAX Measures     | Power BI DAX                             |
| Visualization    | Power BI, Plotly, Seaborn                |
| Documentation    | Markdown (.md)                           |
| IDE              | VS Code                                  |

---

## 🚀 How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/haripriya0209-star/AgriData-Explorer.git
   cd AgriData-Explorer
   ```

2. Install Python dependencies:
   ```bash
   pip install pandas numpy seaborn matplotlib plotly
   ```

3. Open the notebook:
   ```bash
   jupyter notebook EDA.ipynb
   ```

4. Load SQL data:
   - Import `Cleaned_Agri.csv` into MySQL as the `cleaned_agri` table.
   - Run `sql_agri.sql` for all queries.

5. Open Power BI:
   - Connect to the MySQL `agriculture_dataset` database.
   - Power Query transformations (unpivot, crop/metric extraction) are already applied.
   - Slicers and interactions are pre-configured across all 3 dashboard pages.
