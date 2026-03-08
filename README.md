# 🏎️ F1 World Championship Analysis (1950–2024)

> End-to-end data analysis of 74 years of Formula 1 racing — from exploratory analysis and SQL queries to machine learning predictions and an interactive Power BI dashboard.

---

## 📌 Project Overview

This project uses the [Formula 1 World Championship dataset (1950–2024)](https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020) from Kaggle to explore race results, driver and constructor performance, lap times, pit stop strategy, and predictive modelling.

The project is structured across 4 phases:

| Phase | Tool | Description |
|-------|------|-------------|
| 1 | Python | Exploratory Data Analysis (EDA) |
| 2 | SQL (SQLite) | Analytical queries on race data |
| 3 | Scikit-learn | Machine learning & predictions |
| 4 | Power BI | Interactive dashboard |

---

## 📁 Project Structure

```
f1-analysis/
├── notebooks/
│   ├── 01_eda.ipynb        # EDA & data cleaning
│   ├── 02_sql.ipynb        # SQL analysis via SQLite
│   └── 03_ml.ipynb         # ML models & exports
├── data/                   # Raw CSVs from Kaggle (not tracked)
├── exports/                # Processed CSVs for Power BI (not tracked)
├── .gitignore
└── README.md
```

---

## 🐍 Phase 1 — Exploratory Data Analysis

Loaded and cleaned 9 CSV files covering races, drivers, constructors, lap times, pit stops, qualifying and standings.

**Key steps:**
- Replaced Ergast null markers (`\N`) with `NaN`
- Parsed qualifying times from `mm:ss.sss` to milliseconds
- Merged year and circuit data into results
- Generated visualisations for driver wins, constructor eras, and qualifying vs race correlation

**Charts produced:**
- Top 20 all-time race winners
- Season points: Hamilton vs Schumacher
- Constructor wins by era (1950s–2024)
- Grid position vs race finish heatmap

---

## 🗄️ Phase 2 — SQL Analysis

Loaded all datasets into a local SQLite database and ran 5 analytical queries:

1. All-time driver wins leaderboard
2. Average pit stop duration by constructor (2011+)
3. Pole-to-win conversion rate by driver
4. Constructor win dominance per season
5. DNF rate by driver (modern era)

---

## 🤖 Phase 3 — Machine Learning

### Podium Prediction (Classification)
- **Model:** Gradient Boosting Classifier
- **Target:** Did the driver finish in the top 3?
- **Key features:** Grid position, qualifying time, rolling form, pit stop data
- **Result:** Strong ROC-AUC score on 2023–2024 test data

### Points Regression
- **Model:** Gradient Boosting Regressor
- **Target:** How many championship points did the driver score?
- **Result:**
  - R-Squared: **0.6719**
  - Adjusted R-Squared: **0.6682**
  - RMSE: **4.15 points**
  - MAE: **2.75 points**

### Championship Prediction
- **Model:** Random Forest Classifier
- **Target:** Will this driver win the championship?
- **Feature:** Mid-season points and standings (after race 10)
- **Result:** **99.5% accuracy** — by mid-season the leader almost always wins

### Key Insight
> Grid position and qualifying time are the most important predictors of race success — confirming that Saturday performance is the single biggest driver of Sunday results.

---

## 📊 Phase 4 — Power BI Dashboard

Built a 4-page interactive dashboard in Power BI Web using the enriched master dataset.

| Page | Focus | Visuals |
|------|-------|---------|
| 1 | Driver & Nationality Explorer | KPI cards, wins bar chart, races per year line, nationality treemap |
| 2 | Constructor Dynasty | Wins over time, all-time leaderboard, era treemap, year slicer |
| 3 | Race & Lap Time Analysis | Avg lap time by driver/constructor, fastest lap trend, circuit slicer |
| 4 | Performance & Predictions | Win probability by grid, podium rates, points trend |

---

## ⚙️ Setup & Installation

### Requirements
```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter ipykernel
```

### Getting the Data
1. Download the dataset from [Kaggle](https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020)
2. Unzip and place all CSVs in the `data/` folder

### Running the Notebooks
```bash
# Activate virtual environment
source venv/bin/activate  # Mac/Linux

# Launch Jupyter
jupyter notebook
```

Run notebooks in order:
1. `01_eda.ipynb`
2. `02_sql.ipynb`
3. `03_ml.ipynb`

---

## 🔍 Key Findings

- **Lewis Hamilton** leads all-time with **105 race wins**, followed by Michael Schumacher (91) and Max Verstappen (63)
- **British** drivers have the most wins by nationality (317), followed by German and Brazilian
- **F1 has grown** from ~8 races per season in the 1950s to 24 in 2024
- **Ferrari** dominates all-time constructor wins, with Mercedes and Red Bull dominating the modern era
- **Grid position is the strongest predictor** of race outcome — pole position has the highest win probability by far
- The **points regression model** explains 67% of variance in race points, with the remaining 33% attributed to unpredictable factors like safety cars, weather and mechanical failures

---

## 🛠️ Tools & Technologies

![Python](https://img.shields.io/badge/Python-3.13-blue)
![Pandas](https://img.shields.io/badge/Pandas-2.0-green)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-orange)
![SQLite](https://img.shields.io/badge/SQLite-Database-lightgrey)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow)

---

## 📄 Dataset

**Source:** [Formula 1 World Championship (1950–2024) — Kaggle](https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020)  
**Author:** Rohan Rao  
**Coverage:** All F1 races from 1950 to 2024

---

*Built by Tiziano Gallo*
