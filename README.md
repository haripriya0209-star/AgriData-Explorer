# 🌾 Agricultural Production Analytics (India)

This repository contains a complete workflow for analyzing **crop production trends in India** using Python (for data cleaning, preprocessing, and exploratory analysis) and **Power BI** (for interactive dashboards and evaluator-friendly insights).

---

## 📂 Project Structure

- `EDA.ipynb`  
  Jupyter notebook for cleaning, preprocessing, and exploratory analysis of agricultural datasets.
- `AgriData_Explorer.pptx`  
  Exported dashboard visuals and insights for evaluator review.
- `cleaned_agri.csv`  
  Final cleaned dataset used for analysis and dashboarding.
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
- **SQL**: Querying, Schema Design  
- **Power BI**: Interactive Dashboards, Slicers  
- **Visualization**: Correlation & Trend Analysis with Plotly and Seaborn

---

## 📁 Data Sources

**Dataset:** [ICRISAT – District Level Agricultural Data]  
Includes crop, district, and state-level statistics.

**Key Fields:**
- Crop name (Rice, Wheat, Maize, Oilseeds, Millets, etc.)  
- Area cultivated (1000 ha)  
- Production (1000 tons)  
- Yield (kg/ha)  
- Year, District, State identifiers

---

## 🧩 Project Architecture

1. **Data Collection & Cleaning**  
   - Imported raw CSV files.  
   - Removed irrelevant columns (e.g., safflower, linseed).  
   - Handled missing values (zeros → NaN → median imputation).  
   - Exported cleaned dataset (`cleaned_agri.csv`) for dashboard integration.

2. **Exploratory Data Analysis (`EDA.ipynb`)**  
   - Identified top crop-producing states and districts.  
   - Analyzed 50-year production trends (Rice, Wheat, Sugarcane, Millets).  
   - Correlation between **area cultivated vs production**.  
   - Yield efficiency comparisons across states.

3. **Database Design (SQL)**  
   - Normalized schema for crop, district, and state-level data.  
   - Query-based exploration for production/yield metrics.

4. **Visualization (Power BI & Plotly)**  
   - Interactive dashboards with slicers for **State, Crop, Year**.  
   - Charts: bar, pie, line, scatter, geographical heatmaps.

---

## 📊 Power BI Features

- **Interactive Filters:** Crop Type, Region, Year.  
- **Map Visuals:** Highlight yield disparities geographically.  
- **Trend Lines:** Analyze production growth over decades.

---

## 🧑‍🤝‍🧑 Target Users

- **Farmers:** Optimize crop selection based on yield efficiency.  
- **Policymakers:** Identify low-productivity regions & plan interventions.  
- **Researchers:** Study long-term agricultural trends and climate impacts.

---

## 📈 Project Deliverables

- `EDA.ipynb` — Python notebook for cleaning & EDA  
- SQL scripts for database creation & queries  
- Power BI dashboard (`AgriData_Explorer.pptx`)  
- `cleaned_agri.csv` — Final cleaned dataset  
- Documentation & project report

---

## 🛠️ Tech Stack

| Component     | Tool/Language                  |
|---------------|-------------------------------|
| Data Cleaning | Python (Pandas, NumPy)         |
| EDA           | Jupyter Notebook (`EDA.ipynb`) |
| Visualization | Power BI, Plotly, Seaborn      |
| Database      | MySQL                          |
| Documentation | Markdown (.md), PDF            |
| Analysis      | VSCode                         |

---

## 🚀 How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/haripriya0209-star/AgriData-Explorer.git
   cd AgriData-Explorer
   ```

2. Install dependencies:
   ```bash
   pip install pandas numpy seaborn matplotlib plotly
   ```

3. Open the notebook:
   ```bash
   jupyter notebook EDA.ipynb
   ```

4. The cleaned dataset (`cleaned_agri.csv`) is included — no separate cleaning step needed.
