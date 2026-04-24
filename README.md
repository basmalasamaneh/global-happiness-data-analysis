# World Happiness & Population — Data Wrangling Project

> A complete, end-to-end data wrangling and exploratory analysis project investigating the relationship between national population size and happiness scores across 150+ countries from 2015 to 2019.

---

## Project Overview

This project was completed as part of a data wrangling course and demonstrates a full professional data pipeline — from raw data collection to cleaned, merged datasets and insightful visualizations. The central research question explored is:

> **Does a country's population size correlate with its national happiness score?**

Two real-world datasets were gathered using two different methods, assessed for quality and tidiness issues, cleaned systematically, merged into a single analysis-ready dataset, and used to answer the research question through descriptive statistics and visualizations.

---

## Datasets

### Dataset 1 — World Happiness Report (2015–2019)
| Attribute | Details |
|-----------|---------|
| **Source** | [Kaggle — World Happiness Report](https://www.kaggle.com/datasets/unsdsn/world-happiness) |
| **Gathering Method** | Manual Download |
| **Records** | 430+ country-year observations across 5 files |
| **Key Variables** | `Country`, `Happiness_Score`, `GDP_per_Capita`, `Year` |

### Dataset 2 — World Population by Countries
| Attribute | Details |
|-----------|---------|
| **Source** | [World Bank Open Data — SP.POP.TOTL](https://data.worldbank.org/indicator/SP.POP.TOTL) |
| **Gathering Method** | Programmatic Download via HTTP API |
| **Records** | 150+ countries × 5 years |
| **Key Variables** | `Country Name`, `Country Code`, `[Year columns]` → `Population` |

---

## Data Issues Identified & Resolved

### Quality Issues
| # | Issue | Pillar | Resolution |
|---|-------|--------|-----------|
| 1 | Column names differ across yearly happiness files (e.g. `"Happiness Score"` vs `"Score"`) | Consistency | Standardized via rename mapping before concatenation |
| 2 | Missing values in `Happiness_Score` and `GDP_per_Capita` | Completeness | Dropped rows missing the primary score; imputed GDP with per-year median |

### Tidiness Issues
| # | Issue | Rule Violated | Resolution |
|---|-------|--------------|-----------|
| 1 | Happiness data spread across 5 separate CSV files | Rule 3 — one observational unit per table | Concatenated into a single unified DataFrame |
| 2 | Population data in wide format — years as columns | Rule 1 — each variable forms a column | Reshaped using `pd.melt()` to long format |

---

## Key Findings

- **Weak negative correlation (r ≈ −0.20)** between log population size and happiness score — more populous countries tend to score slightly lower on average.
- **GDP per capita is a far stronger predictor** of happiness (r ≈ +0.77) than population size.
- **All top 10 happiest countries** are small-to-medium nations in Northern/Western Europe with high economic output.
- **All bottom 10 least happy countries** are in Sub-Saharan Africa, with varying population sizes — confirming that population alone does not determine well-being.

### Visualizations

| Chart | Description |
|-------|-------------|
| Scatter Plot | Log₁₀ Population vs. Happiness Score with regression line and GDP colour coding |
| Bar Chart | Top 10 vs. Bottom 10 happiest countries with population-shaded bars |
| Correlation Heatmap | Pearson correlations among Happiness Score, GDP per Capita, and Log Population |

---

## Technologies Used

| Tool | Purpose |
|------|---------|
| `Python 3.8+` | Core language |
| `pandas` | Data manipulation and wrangling |
| `numpy` | Numerical operations and log transforms |
| `matplotlib` | Base plotting |
| `seaborn` | Statistical visualizations |
| `requests` + `zipfile` | Programmatic data download |
| `Jupyter Notebook` | Interactive analysis environment |

---

## Final Dataset Schema

The cleaned merged dataset (`cleaned_data_merged.csv`) contains **5 variables**:

| Column | Type | Description |
|--------|------|-------------|
| `Country` | string | Country name |
| `Year` | int | Survey year (2015–2019) |
| `Happiness_Score` | float | National average life evaluation score (0–10) |
| `GDP_per_Capita` | float | GDP per capita contribution to happiness score |
| `Population` | int | Total national population (World Bank) |

---

## Future Work

- Extend the time range to 2020–2023 to examine the impact of COVID-19 on national happiness
- Incorporate additional World Bank indicators (Gini coefficient, life expectancy, education access) for multivariate regression analysis
- Apply fuzzy string matching to reduce country-name mismatches and minimize data loss during the merge
- Explore regional sub-group analysis (Sub-Saharan Africa, Europe, Southeast Asia) to assess whether population-happiness dynamics differ by geography

