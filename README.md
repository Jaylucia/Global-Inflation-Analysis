    # Global Inflation Analysis 2000–2024

## 📌 Project Overview

*Which economies are thriving, which are struggling, and why?*

This project analyses Consumer Price Index (CPI) inflation data across **16 countries and 4 regions** from 2000 to 2024, a period that includes the 2008 global financial crisis, the 2016 Nigerian recession, and the 2021–2023 post-COVID inflation surge.

The analysis is built on a complete data pipeline: raw World Bank data is cleaned and reshaped in Python, stored and queried in SQL, visualised through exploratory analysis, and presented as an interactive Tableau dashboard.

This project holds personal significance. As a Nigerian economist living and studying in Turkey, two countries at the centre of this analysis, the data reflects not just numbers but lived experience.

---

## 🌍 Live Dashboard

👉 **[View the Interactive Tableau Dashboard](https://public.tableau.com/app/profile/chidinma.okoro1296/vizzes)**

The dashboard contains two pages:
- **Global Overview** — World map and regional trend lines with year filter
- **Africa & Personal Story** — Africa decade comparison and the Nigeria–Turkey dual story

---

## 📂 Repository Structure

```
inflation-analysis/
│
├── data/
│   ├── inflation_raw.csv          # Original World Bank download
│   └── inflation_clean.csv        # Cleaned, reshaped analysis file
│
├── notebooks/
│   └── inflation_analysis.ipynb   # Full analysis notebook
│
├── charts/
│   ├── chart1_timeseries.png      # Inflation trajectories by region
│   ├── chart2_heatmap.png         # Full inflation heatmap all countries
│   ├── chart3_correlation.png     # Country correlation matrix
│   ├── chart4_boxplot.png         # Distribution by region
│   └── chart5_worst_episodes.png  # Top 20 worst inflation episodes
│
└── README.md
```

---

## 🌐 Countries & Regions

| Region | Countries |
|--------|-----------|
| **Africa** | Nigeria, Ghana, Kenya, Egypt, South Africa |
| **Emerging Markets** | Turkey, Brazil, India, South Korea, Pakistan |
| **Developed** | USA, Germany, France |
| **Special Cases** | Zimbabwe, Japan, Ethiopia |

### On Country Selection

Three countries originally selected - Argentina, Venezuela, and Zimbabwe — had significant data gaps. Argentina (18 out of 25 years missing) was removed due to a combination of absent data and documented government manipulation of inflation statistics, for which Argentina was formally censured by the IMF between 2007 and 2015. Venezuela (17 missing years) was removed as its government ceased publishing credible economic data from 2014 onwards amid political and economic collapse.

Zimbabwe was retained despite 12 missing years because its hyperinflation episode, the most extreme in this dataset, remains analytically significant even with gaps. Its worst recorded value of 557% in 2020 represents a second wave of instability following the 2009 currency abandonment.

Argentina was replaced with **South Korea**, a compelling emerging market stability story. Venezuela was replaced with **Pakistan**, a complete dataset with chronic high inflation relevant to the Global South narrative. **Ethiopia** was added to the Special Cases group to provide an African counterpoint to Zimbabwe, representing rapid growth alongside significant inflation pressure.

---

## 🛠️ Tools & Pipeline

```
World Bank API (CSV)
        ↓
Google Colab
  • pandas — cleaning, reshaping, EDA
  • matplotlib & seaborn — visualisation
        ↓
SQLite
  • 6 analytical SQL queries
  • Window functions, self joins, CASE WHEN
        ↓
Tableau Public
  • 2 interactive dashboards
  • 4 sheets with filters and reference lines
```

---

## 📓 Notebook Structure

The analysis notebook is organised into three phases:

### Phase 1 — Data Cleaning
- Loaded raw World Bank CSV (266 countries, 71 columns)
- Dropped irrelevant columns (Indicator Name, Indicator Code)
- Filtered to 16 selected countries
- Reshaped from wide format (one column per year) to long format (one row per country per year) using `pd.melt()`
- Handled missing values — documented and justified per country
- Added region classifications and clean display names
- Exported to `inflation_clean.csv` and `inflation.db`

### Phase 2 — SQL Analysis

Six queries written against the SQLite database, each answering a specific analytical question:

| Query | Question | Concepts Used |
|-------|---------|---------------|
| A | Which country had the highest inflation each year? | ROW_NUMBER() window function, subquery |
| B | How do African countries compare across decades? | CASE WHEN, GROUP BY decade |
| C | Which countries maintained inflation below 5% most consistently? | Aggregation, filtering |
| D | Which countries breached the 20% danger threshold and how often? | COUNT, MAX, MIN |
| E | Turkey vs Nigeria year by year — who was higher? | Self JOIN |
| F | How did each country perform relative to its regional average? | AVG() OVER (PARTITION BY region, Year) |

### Phase 3 — EDA & Visualisation

Five charts built using matplotlib and seaborn:

**Chart 1 — Inflation Trajectories**
Line chart showing all 16 countries split into 4 regional panels. Consistent country colours carried through all subsequent visuals.

**Chart 2 — Global Inflation Heatmap**
Countries as rows, years as columns, colour intensity representing inflation rate. Sorted by average inflation. Y-axis capped at 50% to preserve contrast — Zimbabwe's extreme values extend beyond the visible range.

**Chart 3 — Correlation Matrix**
Pearson correlation between every country pair. 
Key finding: Germany and France correlate at 0.92, reflecting shared Eurozone monetary policy. Nigeria correlates more strongly with Turkey (0.55) than with most African peers, suggesting structural economic similarity beyond geographic proximity. Zimbabwe shows near-zero or negative correlation with almost all countries, its crisis operated outside normal global economic cycles entirely.

**Chart 4 — Box Plot by Region**
Inflation distribution per region. The Developed economies box is so tight that their post-COVID inflation spike registers as a mild statistical outlier, the same magnitude that would not even reach outlier status in African or Emerging Market economies where volatility is already embedded in the normal range.

**Chart 5 — Worst Episodes**
Annotated scatter plot of the top 20 worst country-year combinations. Zimbabwe owns the top 4. Turkey appears 6 times across two completely separate eras, 2000–2002 and 2022–2024, two distinct crises separated by nearly two decades of relative stability. Nigeria's 2024 entry at position 17 represents the country's highest inflation rate in the entire dataset, making this not just historical analysis but a live finding.

---

## 🔍 Key Findings

**1. The 2008 and 2022 crises were genuinely global**
Both events appear as dark bands cutting across nearly every country in the heatmap simultaneously, confirming these were external shocks absorbed by all economies rather than country-specific failures.

**2. Three out of five African countries had significantly higher inflation in the 2020s than in any previous decade**
Ghana, Nigeria, and Egypt all show their worst decade average in the 2020s. Kenya and South Africa show relative improvement. Africa's inflation story is not uniform.

**3. Zimbabwe's correlation problem**
Zimbabwe's hyperinflation was so disconnected from global patterns that it shows near-zero or negative correlation with almost every other country. Its crisis did not move with the world, it moved in its own dimension of economic collapse.

**4. Nigeria's official CPI understates lived economic experience**
Nigeria's inflation numbers appear moderate relative to Turkey for much of the dataset. However, fuel subsidies historically suppressed energy prices in the CPI basket. The 2023 subsidy removal made the true inflationary pressure immediately visible. Nigeria's 2024 rate of 33.2% is the highest in the dataset and still rising at the time of analysis.

**5. Germany and France move as one**
A 0.92 correlation between two Eurozone members confirms that shared monetary policy, one central bank, one interest rate, produces near-identical inflation trajectories. This is monetary union working as designed.

**6. The median tells a more honest story than the mean**
The global mean inflation rate of 10.68% is meaningfully skewed by Zimbabwe and Turkey. The median rate is significantly lower, a more representative measure of the typical country's inflation experience across this period.

---

## ⚠️ Data Notes & Limitations

- **Source:** World Bank Open Data — Indicator FP.CPI.TOTL.ZG (Consumer Price Index, annual %)
- **Coverage:** 2000–2024. Some countries have missing values in certain years, documented in the notebook.
- **Zimbabwe cap:** The colour scale in heatmap visuals is capped at 50% to preserve readability. Zimbabwe's worst years (up to 557%) extend beyond this range.
- **2024 data:** Partial year data for some countries. Treated as available and included without adjustment.
- **CPI limitations:** Official CPI measures may not fully capture lived inflation experience, particularly in economies with price controls, currency distortions, or subsidy regimes. Nigeria is specifically noted in the analysis.

---

This project was built as part of a deliberate portfolio development journey — learning SQL, Python EDA, and Tableau through real data on real economic questions.

- 📧 jennifa.chidinma@gmail.com
- 💼 [LinkedIn]([https://linkedin.com/in/chidinma-j-okoro](https://www.linkedin.com/in/jennifer-chidinma/))
- 📊 [Tableau Public](https://public.tableau.com/app/profile/chidinma.okoro1296/vizzes)


---

## 📄 Data Citation

World Bank Open Data. *Inflation, consumer prices (annual %)* — Indicator FP.CPI.TOTL.ZG.
Retrieved from https://data.worldbank.org/indicator/FP.CPI.TOTL.ZG

---

*This project was completed in May 2026.*

    

