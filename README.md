# Survival Analysis of Chlorhexidine Trial Outcomes Using Python

![Project Banner: Survival Analysis of Chlorhexidine Trial Outcomes Using Python](assets/project-banner.png)

  <h2>👩‍⚕️ <b>Dr. Vaishnavi K R</b></h2>
  🎓 PGDM — Artificial Intelligence & Data Science (Healthcare)
</p>

<p align="center">
  <a href="https://github.com/DrVaishnaviKR/chlorhexidine-survival-analysis"><img src="https://img.shields.io/github/stars/DrVaishnaviKR/chlorhexidine-survival-analysis?style=flat&color=yellow" /></a>
  <a href="https://github.com/DrVaishnaviKR/chlorhexidine-survival-analysis"><img src="https://img.shields.io/github/forks/DrVaishnaviKR/chlorhexidine-survival-analysis?style=flat&color=orange" /></a>
  <a href="https://github.com/DrVaishnaviKR/chlorhexidine-survival-analysis"><img src="https://img.shields.io/github/repo-size/DrVaishnaviKR/chlorhexidine-survival-analysis?color=blue" /></a>
  <a href="https://github.com/DrVaishnaviKR/chlorhexidine-survival-analysis"><img src="https://img.shields.io/github/last-commit/DrVaishnaviKR/chlorhexidine-survival-analysis?color=brightgreen" /></a>
  <a href="https://www.python.org/"><img src="https://img.shields.io/badge/Python-3.10-blue?logo=python" /></a>
  <a href="https://colab.research.google.com/drive/1siiXPXCzPmw7i8jXARGoBufek39MiU8T"><img src="https://img.shields.io/badge/Open%20in-Colab-yellow?logo=googlecolab" /></a>
</p>

---

## 🧪 **Project Title**

### **Survival Analysis of Chlorhexidine Trial Outcomes Using Python**

---

## 📘 **Project Summary**

This project performs a full **survival analysis** on a randomized clinical trial comparing **0.12% vs 0.20% Chlorhexidine** in ventilated ICU patients. The aim is to:

* Understand mortality/VAP risk and treatment effectiveness
* Analyze **time-to-event outcomes** with censoring
* Apply survival techniques: Kaplan–Meier, Cox PH, Log-Rank
* Interpret hazard ratios clinically

This repository is fully reproducible using **Python, Lifelines, and Google Colab**.

---

## 📊 **Dataset Description** <a name="dataset"></a>

The dataset contains patient demographics, clinical markers, treatment arm, microbial findings, and survival outcomes.

### Includes:

* **Continuous variables:** Age, APACHE II, TLC, CPIS, Microbial load
* **Categorical variables:** Gender, TreatmentArm, Organism_Present
* **Time variable:** `time_to_event`
* **Event indicator:** `event` (1 = event occurred)

### 📁 Dataset Files

* **Raw data:** `/data/raw_data.xlsx`
* **Cleaned data:** `/data/cleaned_data.xlsx`
* **Cox model variables table:** `/data/cox_model_variables.xlsx`
* **Research article:** `/docs/V7N3_e4a9253f-6b0b-4153-a4a4-7ef730d0ac80.pdf`

### 📑 Mini Data Dictionary

| Variable      | Meaning                 | Type        |
| ------------- | ----------------------- | ----------- |
| time_to_event | Days until event/censor | Numeric     |
| event         | Outcome indicator       | Binary      |
| TreatmentArm  | 0.12% vs 0.20%          | Categorical |
| Age           | Age in years            | Numeric     |
| APACHEII      | Severity score          | Numeric     |

---

## 🎯 **Problem Statement**

* Does 0.20% chlorhexidine reduce VAP or mortality risk?
* Are survival rates different between gender or age groups?
* Which physiological markers predict hazard risk?
* Does microbial growth influence hazard?

---

## 🎯 **Objectives**

* Perform EDA
* Plot Kaplan–Meier curves
* Run Log-Rank test
* Fit Cox PH model
* Check PH assumptions
* Interpret hazard ratios clinically

---

## 🔬 **Methodology**

### 🧩 Data Preparation

* Handle missing values
* Encode categorical variables
* Create survival objects

### 📊 Exploratory Data Analysis

* Summary statistics
* Event vs censored distribution
* Histograms, boxplots

### 📈 Survival Modelling

* Kaplan–Meier estimator
* Life tables
* Log-Rank test
* Cox proportional hazards model
* PH assumption diagnostics

### 🩺 Interpretation

* Hazard ratios
* P-values
* Clinical relevance

---

## 🛠️ **Python Project Structure**

```
├── src
│   ├── data_preprocessing.py
│   ├── eda.py
│   ├── km_analysis.py
│   ├── logrank_test.py
│   ├── cox_model.py
│   └── plots.py
│
├── notebooks
│   └── survival_capstone.ipynb
│
├── data
│   ├── raw_data.xlsx
│   ├── cleaned_data.xlsx
│   └── cox_model_variables.xlsx
│
├── docs
│   └── V7N3_e4a9253f-6b0b-4153-a4a4-7ef730d0ac80.pdf
│
├── results
│   ├── km_overall.png
│   ├── km_by_treatment.png
│   ├── cumulative_hazard.png
│   ├── cox_forest_plot.png
│   └── schoenfeld_residuals.png
│
└── README.md
```

---

## 📈 **Key Visualizations** <a name="results"></a>

* Kaplan–Meier survival curves (overall & by treatment)
* Cumulative hazard plots
* Cox PH forest plot
* Schoenfeld residual diagnostics
* Event distribution charts

---

## 📊 **Results & Interpretation**

* Survival probabilities at 30, 60, and 90 days
* Which treatment arm shows better survival
* Significant predictors in Cox model
* Clinical interpretation of hazard ratios

---

## 🧠 **Discussion**

* Clinical implications
* Biases & censoring concerns
* How findings relate to literature

---

## 🏁 **Conclusion**

* Does chlorhexidine concentration influence survival?
* Most important predictors
* Role of survival modelling in clinical decision-making

---

## 🚀 **Future Work**

* Time-varying Cox models
* Parametric survival models
* Machine learning survival models
* External dataset validation

---

<p align="center">
  <b>✨ Prepared by: Dr. Vaishnavi K R</b><br>
  <i>PGDM AI & Data Science in Healthcare</i>
</p>
