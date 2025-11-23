# 🌟 **Survival Analysis of Chlorhexidine Trial Outcomes Using Python**

![Project Banner](https://via.placeholder.com/1200x300.png?text=Survival+Analysis+of+Chlorhexidine+Trial+Outcomes)

<p align="center">

## 👩‍⚕️ **Author: Dr. Vaishnavi K R**

### 🎓 *PGDM in Artificial Intelligence & Data Science (Healthcare)*

<p align="center">
<a href="https://www.linkedin.com"><img src="https://img.shields.io/badge/Author-Dr.Vaishnavi%20K%20R-purple?logo=githubpages"/></a>
<a href="#"><img src="https://img.shields.io/badge/AI%20%26%20Data%20Science-PGDM-blue?logo=googlescholar"/></a>
<a href="#"><img src="https://img.shields.io/badge/Healthcare-Analytics-green?logo=heartbeat"/></a>
</p>

<p align="center">
<a href="https://colab.research.google.com/drive/1siiXPXCzPmw7i8jXARGoBufek39MiU8T"><img src="https://img.shields.io/badge/Run%20on-Colab-yellow?logo=googlecolab"/></a>
<a href="https://www.python.org/"><img src="https://img.shields.io/badge/Python-3.10-blue?logo=python"/></a>
<a href="#dataset"><img src="https://img.shields.io/badge/Dataset-Available-green?logo=data"/></a>
</p>
</p>

---

## 🎯 **Project Title**

### 🧪 *Survival Analysis of Chlorhexidine Trial Outcomes Using Python*

---

## 📘 **Project Summary**

This capstone project demonstrates a full end‑to‑end *survival analysis workflow* on a randomized clinical trial comparing **0.12% vs 0.20% chlorhexidine** in mechanically ventilated ICU patients.

You will learn and implement:

* 📈 **Kaplan–Meier survival estimation**
* 🔍 **Log‑Rank hypothesis testing**
* ⚕️ **Cox Proportional Hazards modelling**
* 📊 **Clinical interpretation + diagnostics**

> 🚀 Fully reproducible using Python + Colab Notebook.

---

## 📦 Files Provided

* 📓 `/notebooks/survival_capstone.ipynb` — full Colab notebook
* ⚙️ `/src/` — modular Python scripts
* 📁 `/data/Chlorhexidine Trials Data Cleaned.xlsx` — cleaned dataset
* 📊 `/results/` — plots, tables, visual outputs
* 📄 `requirements.txt`

---

## 📚 **Short Summary**

This repository contains a full survival analysis pipeline performed on Chlorhexidine ICU trial data. The goal is to evaluate whether chlorhexidine concentration affects hazard of VAP or mortality using modern survival analysis techniques.

---

## 📊 **Dataset Description**

**Source:** Chlorhexidine Trial Study — ICU patients receiving oral care.

🔑 **Key Variables:**

* `time_to_event` – days until event/censor
* `event` – 1 = event occurred, 0 = censored
* `TreatmentArm` – 0.12% or 0.20% solution
* Clinical covariates: `Age`, `Gender`, `APACHEII`, `TLC_D1`, `Tracheostomy`, `CPIS`, `Oral_Microbial_Load`

### 🔗 **Download Dataset Files**

* 📥 **Raw Data:** /mnt/data/Data form Chlorhexidine Trial.xlsx
* 🧹 **Cleaned Data:** /mnt/data/Chlorhexidine Trials Data Cleaned.xlsx
* 🧾 **Data Dictionary:** *(see table below)*
* 🎯 **Dependent Variable:** `time_to_event`, `event`
* 🧩 **Independent Variables:** All clinical + demographic predictors

---

## 📑 **Data Dictionary**

| Column Name           | Description                               | Type        |
| --------------------- | ----------------------------------------- | ----------- |
| `time_to_event`       | Days from enrollment until event/censor   | Numeric     |
| `event`               | Event indicator (1 = event, 0 = censored) | Binary      |
| `TreatmentArm`        | 0.12% vs 0.20% chlorhexidine              | Categorical |
| `Age`                 | Patient age in years                      | Numeric     |
| `Gender`              | Male/Female                               | Categorical |
| `APACHEII`            | Severity score at admission               | Numeric     |
| `TLC_D1`              | Total leukocyte count Day 1               | Numeric     |
| `Tracheostomy`        | Whether patient had tracheostomy          | Binary      |
| `CPIS`                | Clinical Pulmonary Infection Score        | Numeric     |
| `Oral_Microbial_Load` | Colony count/organism load                | Numeric     |

---

## 🔍 Problem Statement

This repository contains a capstone project implementing survival analysis on a randomized clinical trial comparing chlorhexidine 0.12% vs 0.20% in mechanically ventilated patients. The analysis demonstrates Kaplan–Meier estimation, Log-Rank testing, and Cox Proportional Hazards modelling with reproducible Python code (notebook + scripts).

## Files Provided

* `/notebooks/survival_capstone.ipynb` — full analysis runnable in Colab
* `/src` — modular Python scripts (data_preprocessing.py, eda.py, km_analysis.py, logrank_test.py, cox_model.py, plots.py)
* `/data/Chlorhexidine Trials Data Cleaned.xlsx` — cleaned dataset (sensitive data excluded from public repo if necessary)
* `/results` — generated plots and tables
* `requirements.txt` — environment dependencies

## Data description

* **Source:** Chlorhexidine clinical trial dataset (randomized, parallel-arm) — cleaned files included with project.
* **Key variables:**

  * `time_to_event` — duration in days from randomisation to event or censoring
  * `event` — event indicator (1 = event occurred, 0 = censored)
  * `TreatmentArm` — 0.12% vs 0.20% chlorhexidine
  * `Age`, `Gender`, `APACHEII`, `TLC_D1`, `Tracheostomy`, `CPIS`, `Oral_Microbial_Load`

> Add a short data dictionary here describing each column (students should fill exact definitions and data types).

## Problem Statement (3–5 questions)

1. Does Chlorhexidine 0.20% reduce the hazard of VAP/death compared to 0.12%?
2. Are there survival differences by age groups or gender?
3. Which clinical covariates (APACHE II, tracheostomy, TLC) significantly influence hazard rates?

## Objectives

1. Perform EDA and data cleaning
2. Estimate survival curves (Kaplan–Meier)
3. Compare groups (Log-Rank)
4. Fit Cox PH model and report hazard ratios
5. Check PH assumptions and provide diagnostic plots
6. Produce clear visualisations and clinical interpretations

## Methodology (workflow)

1. **Data preparation** — load, impute/handle missing values, encode categorical variables, create `duration` & `event` columns.
2. **EDA** — event/censor distribution, baseline table, descriptive plots.
3. **Survival modelling** — Kaplan–Meier curves, Log-Rank tests, Cox PH modelling, Schoenfeld residuals test and plots.
4. **Evaluation** — hazard ratios, p-values, survival probabilities at 30/60/90 days, clinical interpretation.

## How to reproduce (Colab)

1. Open the Colab notebook: `https://colab.research.google.com/drive/1siiXPXCzPmw7i8jXARGoBufek39MiU8T` (provided).
2. Upload `data/Chlorhexidine Trials Data Cleaned.xlsx` to the Colab session or mount Google Drive.
3. Run `!pip install -r requirements.txt` (or `!pip install lifelines pandas matplotlib seaborn openpyxl`).
4. Run the notebook cells sequentially. The notebook has sections for data prep, KM plots, Log-Rank tests, Cox modelling, PH checks, and result export.

## Key Visualisations (saved under `/results`)

* Kaplan–Meier survival curves (overall and by treatment)
* Cumulative hazard functions
* Schoenfeld residual plots (PH diagnostics)
* Forest plot of hazard ratios
* Event distribution bar charts

## Results (what to report)

* Survival probabilities at 30, 60, and 90 days
* Which groups show better survival
* Hazard ratios with 95% CI and p-values
* Clinical interpretation (effect size and relevance)

## Discussion points to include

* Clinical implications and comparison to literature
* Limitations: CPIS diagnostic sensitivity, low event rates, LAMA censoring, missingness, confounding
* Suggested future work: time-varying covariates, parametric survival models, external validation

## Citation & References

* Original trial and background literature included in `references/` (see `Vyas et al., Annals of International Medical and Dental Research, 2021` PDF).

## Licence

Specify licence (e.g., MIT) and data usage notes. Remove or redact any PHI before publishing.

