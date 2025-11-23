# 🏥 Survival Analysis of Chlorhexidine Trial Outcomes Using Python

![Banner](Projectbanner/banner.png)

---

<p align="center">
  <strong>👩‍⚕️ Author:</strong> Dr Vaishnavi K R &nbsp; • &nbsp; <strong>🧪 Type:</strong> Clinical Survival Analysis &nbsp; • &nbsp; <strong>🧭 Notebook:</strong> [Colab Notebook](https://colab.research.google.com/drive/1b5pE58pYSHCVcbzj_wTYR3OQu6fqv9Ew?authuser=0)
</p>

[![GitHub Repo stars](https://img.shields.io/github/stars/DrVaishnaviKR/chlorhexidine-survival-analysis?style=for-the-badge)](https://github.com/DrVaishnaviKR/chlorhexidine-survival-analysis)
[![Forks](https://img.shields.io/github/forks/DrVaishnaviKR/chlorhexidine-survival-analysis?style=for-the-badge)]
[![Last commit](https://img.shields.io/github/last-commit/DrVaishnaviKR/chlorhexidine-survival-analysis?style=for-the-badge)]
[![Repo size](https://img.shields.io/github/repo-size/DrVaishnaviKR/chlorhexidine-survival-analysis?style=for-the-badge)]
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge)]

---

## 🚀 Quick overview

This repository presents a complete survival analysis workflow on a Chlorhexidine clinical trial dataset. It explores how treatment, age, APACHE II score, and baseline characteristics influence patient survival. The analysis includes KM curves, Cox PH modeling, diagnostics, and clear visual interpretation — designed for healthcare researchers.

**Key techniques used:** Kaplan–Meier estimation, Log-Rank tests, Cox Proportional Hazards models, Schoenfeld residual diagnostics, and informative visualisations.

## 📌 Project structure

```
├── Projectbanner/
│   └── banner.png
├── data/
│   ├── raw/
│   └── cleaned/
├── results/
│   ├── Basic structure of Data.png
│   ├── KM model.png
│   ├── Survival Curves by Treatment Group.png
│   ├── Adjusted Survival Curves APACHE II (partial effects).png
│   ├── Adjusted Survival Curves Treatment Group.png
│   ├── Cox model Hazard Ratios (HR).png
│   ├── Log-Rank Test.png
│   └── proportional hazards checks/*.png
├── notebooks/
│   └── survival_analysis.ipynb  (or open the Colab link above)
├── document/
│   └── paper_presentation.pdf
├── requirements.txt
└── README.md
```

---

## 🎯 Research questions

* **Does Chlorhexidine reduce the hazard of death?**
* **Do survival probabilities differ between treatment groups?**
* **Which baseline variables (age, APACHEII, TLC_D1) significantly affect hazard?**
* **Is the Cox Proportional Hazards assumption satisfied?**

---

## 🎓 Objectives

* Clean and prepare time-to-event data
* Visualise cohort & event structure
* Estimate KM survival functions & compare groups (Log-Rank)
* Fit Cox PH models and report hazard ratios (with 95% CI)
* Perform PH diagnostics (Schoenfeld residuals)
* Deliver clinical interpretation and recommendations

---

## 🧭 How to run (local)

1. Clone the repo

```bash
git clone https://github.com/DrVaishnaviKR/chlorhexidine-survival-analysis.git
cd chlorhexidine-survival-analysis
```

2. Install dependencies

```bash
pip install -r requirements.txt
```

3. Run the notebook (Jupyter) or open the Colab link above

**Notebook cells of interest**

* `01_data_prep` — load, clean, create `duration` & `event`
* `02_eda` — cohort summaries & distributions
* `03_km_logrank` — Kaplan–Meier & log-rank test
* `04_cox` — Cox PH model and diagnostics
* `05_results` — figures and clinical interpretation

---

## 🧪 Dataset description

A structured overview of variables used in the analysis:

Variable	Description
time_to_event	Follow-up duration in days
event	1 = death, 0 = censored
treatment_group	Chlorhexidine / Control
age	Age of patient
gender	Male / Female
APACHEII	Severity score on admission
TLC_D1	Total Leukocyte Count on Day 1



---

## 📈 Key visualisations (embedded)

> Click images to enlarge — all figures are stored in `results/`.

### Primary figures

<div align="center">

**Kaplan–Meier model preview**

<div align="center">
  <img src="results/km model.png" width="600" alt="Overall KM">
</div>

**Survival curves: treatment groups**

[![Survival Curves by Treatment Group](results/Survival Curves by Treatment Group.png)](results/Survival Curves by Treatment Group.png)

</div>

### Additional diagnostics & figures

* **Basic data structure:** <div align="center">
  <img src="results/km_model.png" width="600" alt="Overall KM">
</div>
* **Adjusted survival (APACHE II):** `results/Adjusted Survival Curves APACHE II (partial effects).png`
* **Adjusted survival (Treatment):** `results/Adjusted Survival Curves Treatment Group.png`
* **Cox HR plot:** `results/Cox model Hazard Ratios (HR).png`
* **Log-Rank test plot:** `results/Log-Rank Test.png`
* **PH checks (Schoenfeld):** `results/proportional hazards check age.png`, `results/proportional hazards check APACHEII.png`, `results/proportional hazards check TCL1.png`, `results/proportional hazards check treatment grp.png`

---

## 🔬 Results (summary template)

> Replace the template values with the exact numeric outputs from the notebook.

* **Point estimate (treatment effect):** Chlorhexidine shows a lower hazard of mortality — *HR = 0.XX (95% CI: 0.XX–0.XX), p = 0.XXX*.
* **Predictors:** Age and APACHEII were associated with increased hazard (per-unit HR > 1).
* **Log-Rank:** Significant difference between groups (χ² = X.XX, p = 0.XXX).
* **PH:** Global PH test p = 0.XXX — individual covariate checks mostly satisfied / exceptions noted.

---

## 🩺 Clinical discussion (short)

* The intervention suggests potential mortality benefit; effect size and CIs determine clinical relevance.
* APACHEII and age are expected prognosticators — results align with clinical knowledge.
* Limitations: censoring patterns, sample size, unmeasured confounding, potential informative censoring.

---

## 🧭 Recommended next steps

1. Fit **time-varying Cox** if PH violated for any covariate.
2. Test **parametric models** (Weibull, Exponential) for better predictive performance.
3. Apply **machine learning survival methods** (Random Survival Forests, CoxBoost) for exploratory signal detection.
4. Validate findings on an external dataset (temporal or geographic validation).

---

## 📂 Files to check / commit

* `results/*.png` — visual outputs that should be included in your final repo
* `document/paper_presentation.pdf` — link from README
* `notebooks/survival_analysis.ipynb` or Colab link — interactive analysis

---

## ✉️ Contact & citation

If you use this work, please cite the notebook and contact:
**Dr Vaishnavi K R** — GitHub: `@DrVaishnaviKR` — Email: (vaishnavirajeshshyni@gmail.com)

---

*Made with ❤️ — survival analysis with Python (pandas, lifelines, matplotlib).*
