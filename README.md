# 📈 Survival Analysis of Chlorhexidine Trial Outcomes Using Python

<p align="center">

  <!-- FULL BADGE COLLECTION -->
  <img src="https://img.shields.io/badge/Field-Clinical%20Data%20Science-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/Domain-Survival%20Analysis-orange?style=for-the-badge">
  <img src="https://img.shields.io/badge/Method-Kaplan--Meier%20%7C%20Cox%20PH-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/Data-Clinical%20Trial%20(VAP%20Study)-purple?style=for-the-badge">
  <img src="https://img.shields.io/badge/Source-Randomized%20Controlled%20Trial-red?style=for-the-badge">
  <img src="https://img.shields.io/badge/Python-3.10+-yellow?style=for-the-badge&logo=python">
  <img src="https://img.shields.io/badge/Libraries-lifelines%2C%20pandas%2C%20matplotlib-brightgreen?style=for-the-badge">
  <img src="https://img.shields.io/badge/Status-Completed-success?style=for-the-badge">
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge">


</p>

<hr>

This project is based on a real clinical trial case study titled:  
**“Effectiveness of Oral Hygiene with Chlorhexidine Mouthwash with 0.12% and 0.2% Concentration on Incidence of VAP”**  
Published in *Annals of International Medical and Dental Research (2021)*.  

The complete article is included in the repository at:  
📄[Article](/document/Publication.pdf)

This repository reproduces and interprets **time-to-VAP (Ventilator-Associated Pneumonia)** outcomes using classical Survival Analysis methods in Python.  
All results, tables, and plots are generated using the Python analysis script and Jupyter workflow.

---

<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Survival Analysis — Chlorhexidine Trial</title>
  <style>
    :root{
      --accent:#16a085;
      --accent-dark:#117a60;
      --muted:#6b7280;
      --bg:#ffffff;
      --card:#f7fffb;
      --maxw:900px;
      --font-sans: "Helvetica Neue", Arial, sans-serif;
    }
    body{
      font-family:var(--font-sans);
      background:linear-gradient(180deg,#fbfdfb 0%, #ffffff 100%);
      color:#111827;
      margin:0;
      padding:24px;
      display:flex;
      justify-content:center;
    }
    .container{
      width:100%;
      max-width:var(--maxw);
      background:var(--bg);
      box-shadow:0 6px 30px rgba(2,6,23,0.05);
      border-radius:10px;
      padding:28px;
    }
    header{
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:16px;
    }
    h1{ margin:0; font-size:28px; letter-spacing:-0.02em; }
    .subtitle{ color:var(--muted); margin-top:6px; font-size:13px; }
    .badge{
      background:linear-gradient(180deg,var(--accent) 0%, var(--accent-dark) 100%);
      color:white;
      padding:6px 10px;
      border-radius:6px;
      font-weight:600;
      font-size:13px;
      text-decoration:none;
    }
    .lead{
      margin:18px 0 22px;
      color:#334155;
      line-height:1.45;
    }
    section{ margin-top:18px; }
    .card{
      background:var(--card);
      border-left:4px solid var(--accent);
      padding:14px 16px;
      border-radius:8px;
      margin-bottom:12px;
    }
    h2{ margin:8px 0 10px; font-size:18px; }
    h3{ margin:6px 0; font-size:15px; color:#0f172a; }
    ul{ margin:8px 0 12px 20px; color:#1f2937; }
    table{
      width:100%;
      border-collapse:collapse;
      margin-top:8px;
      font-size:14px;
    }
    th, td{
      text-align:left;
      padding:8px 10px;
      border-bottom:1px solid #edf2f7;
    }
    th{ background:#ffffff; color:#0f172a; font-weight:700; }
    .images{
      display:grid;
      grid-template-columns:repeat(2,1fr);
      gap:12px;
      margin-top:12px;
    }
    .imgwrap{
      border-radius:8px;
      overflow:hidden;
      background:#fff;
      box-shadow:0 2px 12px rgba(2,6,23,0.04);
      padding:6px;
    }
    img{ width:100%; height:auto; display:block; }
    .small{ font-size:13px; color:var(--muted); margin-top:6px; }
    .footer{
      margin-top:18px;
      padding-top:12px;
      border-top:1px dashed #e6eef1;
      display:flex;
      justify-content:space-between;
      align-items:center;
      gap:12px;
      flex-wrap:wrap;
    }
    .license{
      display:inline-flex;
      gap:10px;
      align-items:center;
    }
    .btn{
      background:var(--accent);
      color:white;
      padding:8px 12px;
      border-radius:8px;
      text-decoration:none;
      font-weight:600;
      font-size:14px;
    }
    code{ background:#0f172a10; padding:2px 6px; border-radius:6px; font-family:monospace; }
    @media (max-width:720px){
      .images{ grid-template-columns: 1fr; }
      header{ flex-direction:column; align-items:flex-start; gap:10px; }
    }
  </style>
</head>
<body>
  <div class="container" role="main">
    <header>
      <div>
        <h1>Survival Analysis — Chlorhexidine Trial</h1>
        <div class="subtitle">Kaplan–Meier | Cox PH | Log-Rank | Schoenfeld diagnostics</div>
      </div>
      <div style="text-align:right">
        <a class="badge" href="LICENSE">MIT License</a>
      </div>
    </header>

    <p class="lead">
      This repository contains a full survival-analysis workflow for the clinical trial:
      <strong>Effectiveness of oral hygiene with chlorhexidine (0.12% vs 0.20%) on incidence of VAP.</strong>
      Results include KM curves, log-rank test, multivariable Cox model, Schoenfeld checks and forest plots.
    </p>

    <!-- Project Summary -->
    <section>
      <div class="card">
        <h2>Project Summary</h2>
        <p>
          A survival analysis of ICU patients receiving 0.12% or 0.20% chlorhexidine mouthwash.
          Analyses were performed in Python using the <code>lifelines</code> package. The dataset shows high VAP-free survival, few events (n=7), and no statistically significant difference between arms (log-rank p = 0.16).
        </p>
      </div>
    </section>

    <!-- Dataset Description -->
    <section>
      <h2>Dataset Description</h2>
      <div class="card">
        <p class="small">Files in the repository: <code>data/Chlorhexidine Trials.xlsx</code>, <code>data/Data form Chlorhexidine Trial (Raw).xlsx</code>, <code>document/Publication.pdf</code>, and analysis results in <code>results/</code>.</p>

        <table aria-label="Dataset variables">
          <thead>
            <tr><th>Variable</th><th>Description</th><th>Type</th></tr>
          </thead>
          <tbody>
            <tr><td><strong>time</strong></td><td>Days until VAP or censoring</td><td>Continuous</td></tr>
            <tr><td><strong>event</strong></td><td>Event indicator (1 = VAP, 0 = censored)</td><td>Binary</td></tr>
            <tr><td>Age</td><td>Patient age (years)</td><td>Continuous</td></tr>
            <tr><td>Gender</td><td>Male / Female</td><td>Categorical</td></tr>
            <tr><td>chest_xray, culture, ulcer</td><td>Clinical indicators (binary)</td><td>Binary</td></tr>
            <tr><td>apache_score, cpis, tlc_score, microbial_load</td><td>Severity & infection markers</td><td>Continuous</td></tr>
            <tr><td>treatment_arm</td><td>1 = 0.12% | 2 = 0.20%</td><td>Categorical</td></tr>
          </tbody>
        </table>

        <p class="small">Full data dictionary and transformation rules are included in the uploaded interpretation document: <a href="/mnt/data/interpretation_of_survival_analysis.docx">interpretation_of_survival_analysis.docx</a>.</p>
      </div>
    </section>

    <!-- Problem Statement & Objectives -->
    <section>
      <div class="card">
        <h2>Problem Statement</h2>
        <p>Does 0.20% chlorhexidine reduce the incidence and hazard of VAP compared with 0.12% in mechanically ventilated ICU patients? Which baseline factors influence time to VAP?</p>

        <h3>Objectives</h3>
        <ul>
          <li><strong>Primary:</strong> Compare VAP-free survival (0.12% vs 0.20%) and test significance (Log-Rank).</li>
          <li><strong>Secondary:</strong> Fit Cox PH model to estimate hazard ratios for age, APACHE II, TLC, microbial load, culture, and X-ray findings; validate PH assumption; and visualize results.</li>
        </ul>
      </div>
    </section>

    <!-- Methodology -->
    <section>
      <h2>Methodology</h2>
      <div class="card">
        <h3>6.1 Data Preparation</h3>
        <ul>
          <li>Import dataset and standardize column names.</li>
          <li>Handle missing values (median imputation for numeric predictors).</li>
          <li>Encode categorical variables (e.g., treatment_arm numeric codes).</li>
          <li>Create survival objects: <code>duration = time</code>, <code>event = event</code>.</li>
        </ul>

        <h3>6.2 Exploratory Data Analysis</h3>
        <ul>
          <li>Distribution of events vs censored observations.</li>
          <li>Summary statistics and clinical baseline checks.</li>
          <li>Visualizations: histograms, boxplots, correlation heatmap.</li>
        </ul>

        <h3>6.3 Survival Modelling</h3>
        <ul>
          <li>⭐ Kaplan–Meier estimator (overall and by treatment arm)</li>
          <li>⭐ Life tables and survival probabilities</li>
          <li>⭐ Log-Rank test for group comparison</li>
          <li>⭐ Cox Proportional Hazards Model (multivariable)</li>
          <li>⭐ PH assumption checks using Schoenfeld residuals</li>
        </ul>

        <h3>6.4 Model Evaluation & Interpretation</h3>
        <ul>
          <li>Report hazard ratios (HR), 95% CI and p-values.</li>
          <li>Interpret clinical significance and model limitations (low event count).</li>
        </ul>
      </div>
    </section>

    <!-- Implementation Structure -->
    <section>
      <h2>Python Implementation Structure</h2>
      <div class="card">
        <p class="small">Key files & folders (copy from your repo):</p>
        <table>
          <thead><tr><th>Path</th><th>Purpose</th></tr></thead>
          <tbody>
            <tr><td><code>/data/Chlorhexidine Trials.xlsx</code></td><td>Cleaned input dataset</td></tr>
            <tr><td><code>/document/Publication.pdf</code></td><td>Original published trial paper</td></tr>
            <tr><td><code>/results/*.png</code></td><td>Plots & diagnostics (KM, Schoenfeld, forest plots)</td></tr>
            <tr><td><code>Chlorhexidine_Survival_Analysis.ipynb</code></td><td>Main notebook with analysis cells</td></tr>
            <tr><td><code>requirements.txt</code></td><td>Python dependencies</td></tr>
          </tbody>
        </table>

        <h3>Preview of key visuals</h3>
        <div class="images" aria-hidden="false">
          <div class="imgwrap"><img src="results/km_overall.png" alt="KM overall"><div class="small">Overall Kaplan–Meier</div></div>
          <div class="imgwrap"><img src="results/km_trail_arm.png" alt="KM by arm"><div class="small">KM by treatment arm</div></div>
          <div class="imgwrap"><img src="results/correl_heatmap.png" alt="Correlation heatmap"><div class="small">Correlation heatmap</div></div>
          <div class="imgwrap"><img src="results/cox_forest_hr.png" alt="Forest plot"><div class="small">Forest plot (HR)</div></div>
        </div>
      </div>
    </section>

    <!-- Key findings -->
    <section>
      <h2>Key Findings (short)</h2>
      <div class="card">
        <ul>
          <li>Overall survival remained high; small decline between days 2–6; survival ≈ 0.92 by day 10.</li>
          <li>0.20% arm had slightly better VAP-free survival visually, but <strong>log-rank p = 0.16</strong> (not significant).</li>
          <li>Cox model showed wide CIs and no significant predictors—limited by low number of events (n=7).</li>
          <li>Schoenfeld residual diagnostics: all covariates satisfied PH assumption (p &gt; 0.05).</li>
        </ul>
      </div>
    </section>

    <!-- Links and license -->
    <div class="footer">
      <div>
        <a class="btn" href="/mnt/data/interpretation_of_survival_analysis.docx" title="Interpretation document">Open interpretation doc</a>
      </div>
      <div class="license">
        <div style="font-size:13px;color:var(--muted)">License:</div>
        <a class="badge" href="LICENSE">MIT</a>
      </div>
    </div>

  </div>
</body>
</html>
 

---

# 📚 Citation  
Original Trial Paper: *Vyas et al., 2021*  
Notebook / Script: `survival_analysis_of_chlorhexidine_trial_patients.py`  
PDF: `/document/Publication.pdf`

---

# 📄 License  
This project is licensed under the **MIT License**.  
You are free to use, modify, and distribute with attribution.
[MIT LICENSE](LICENSE)

---

<p align="center">
  <img src="https://img.shields.io/badge/Author-Dr.%20Vaishnavi%20K%20R%20%7C%20AI%20%26%20Data%20Science%20in%20Healthcare-blue?style=for-the-badge">
</p>


---

**End of README**  


 

