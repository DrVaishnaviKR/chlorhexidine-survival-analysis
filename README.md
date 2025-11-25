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
    --c1:#059669;      /* green */
    --c2:#0ea5e9;      /* blue */
    --dark:#0f172a;
    --muted:#64748b;
    --bg:#ffffff;
    --card:#f8fffb;
    --wide:1100px;
    --font: "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  }
  body{
    margin:0; padding:0;
    background:linear-gradient(120deg,#eefdf8 0%,#f5faff 100%);
    font-family:var(--font); color:var(--dark);
    display:flex; justify-content:center;
  }
  .page{
    width:100%; max-width:var(--wide);
    padding:30px;
  }

  h1{ font-size:32px; margin-bottom:6px; }
  h2{ margin-top:20px; font-size:24px; }
  h3{ font-size:18px; }

  .badge{
    display:inline-block;
    background:linear-gradient(90deg,var(--c1),var(--c2));
    color:white;
    padding:6px 12px;
    border-radius:20px;
    font-weight:600; font-size:14px;
    text-decoration:none;
  }

  /* Cards */
  .card{
    background:var(--card);
    padding:18px 20px;
    border-radius:12px;
    box-shadow:0 4px 18px rgba(0,0,0,0.05);
    border-left:5px solid var(--c1);
    margin-bottom:20px;
  }

  /* Horizontal flow containers */
  .flow-row{
    display:flex;
    gap:20px;
    flex-wrap:wrap;
    align-items:flex-start;
  }
  .flow-col{
    flex:1 1 calc(50% - 20px);
    min-width:320px;
  }

  ul{ margin:8px 0 14px 20px; }
  table{
    width:100%; border-collapse:collapse;
    margin-top:10px; font-size:14px;
  }
  th,td{
    padding:8px 10px; border-bottom:1px solid #e5e7eb;
    text-align:left;
  }
  th{ background:#fff; }

  img{
    width:100%; border-radius:10px;
    box-shadow:0 2px 12px rgba(0,0,0,0.05);
  }

  .img-grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(280px,1fr));
    gap:18px;
    margin-top:10px;
  }

  .footer{
    margin-top:40px; padding-top:20px; border-top:1px solid #e2e8f0;
    display:flex; justify-content:space-between; flex-wrap:wrap;
  }

</style>
</head>

<body>
<div class="page">

  <!-- Header -->
  <header>
    <h1>Survival Analysis — Chlorhexidine Trial</h1>
    <a class="badge" href="LICENSE">MIT License</a>
  </header>
  <p style="color:var(--muted); margin-top:6px;">Kaplan–Meier • Log-Rank • Cox PH • Schoenfeld Diagnostics</p>


  <!-- Project Summary -->
  <section class="card">
    <h2>📌 Project Summary</h2>
    <p>
      This project evaluates whether <strong>0.20% chlorhexidine</strong> reduces the hazard and incidence of
      Ventilator-Associated Pneumonia (VAP) compared to <strong>0.12%</strong> among ICU patients.
      Using Python survival analysis (Kaplan–Meier, Log-Rank, Cox PH, Schoenfeld tests),
      we found high survival in both groups, with a slight but <em>non-significant</em> advantage for 0.20%.
    </p>
  </section>


  <!-- Dataset -->
  <section class="card">
    <h2>📊 Dataset Description</h2>
    <p style="margin-bottom:12px;">Files: <code>/data/Chlorhexidine Trials.xlsx</code>, <code>/document/Publication.pdf</code></p>

    <table>
      <thead><tr><th>Variable</th><th>Description</th><th>Type</th></tr></thead>
      <tbody>
        <tr><td>time</td><td>Days until VAP or censoring</td><td>Continuous</td></tr>
        <tr><td>event</td><td>1 = VAP, 0 = censored</td><td>Binary</td></tr>
        <tr><td>Age</td><td>Patient age</td><td>Continuous</td></tr>
        <tr><td>Gender</td><td>Male/Female</td><td>Categorical</td></tr>
        <tr><td>chest_xray, culture, ulcer</td><td>Clinical indicators</td><td>Binary</td></tr>
        <tr><td>apache_score, tlc_score, microbial_load</td><td>Severity & infection markers</td><td>Continuous</td></tr>
        <tr><td>treatment_arm</td><td>1 = 0.12%, 2 = 0.20%</td><td>Categorical</td></tr>
      </tbody>
    </table>

  </section>


  <!-- Problem Statement + Objectives -->
  <section class="flow-row">
    <div class="flow-col card">
      <h2>❓ Problem Statement</h2>
      <p>
        Does 0.20% chlorhexidine reduce VAP risk more effectively than 0.12%?
        Which clinical variables influence <strong>time to VAP</strong>?
      </p>
    </div>

    <div class="flow-col card">
      <h2>🎯 Objectives</h2>
      <ul>
        <li>Compare VAP-free survival (0.12% vs 0.20%)</li>
        <li>Perform Log-Rank significance testing</li>
        <li>Model hazard ratios using Cox PH</li>
        <li>Check PH assumptions using Schoenfeld residuals</li>
        <li>Visualize clinical risk patterns</li>
      </ul>
    </div>
  </section>


  <!-- Methodology Horizontal Flow -->
  <section class="card">
    <h2>🧪 Methodology (Horizontal Flow)</h2>

    <div class="flow-row">
      <div class="flow-col card">
        <h3>6.1 Data Preparation</h3>
        <ul>
          <li>Import dataset</li>
          <li>Clean & rename columns</li>
          <li>Encode categorical variables</li>
          <li>Create survival objects (time, event)</li>
        </ul>
      </div>

      <div class="flow-col card">
        <h3>6.2 Exploratory Data Analysis</h3>
        <ul>
          <li>Events vs censored distribution</li>
          <li>Summary statistics</li>
          <li>Histograms & boxplots</li>
        </ul>
      </div>

      <div class="flow-col card">
        <h3>6.3 Survival Modelling</h3>
        <ul>
          <li>⭐ Kaplan–Meier curves</li>
          <li>⭐ Life tables</li>
          <li>⭐ Log-Rank test</li>
          <li>⭐ Cox PH model</li>
          <li>⭐ Schoenfeld PH diagnostics</li>
        </ul>
      </div>

      <div class="flow-col card">
        <h3>6.4 Model Evaluation</h3>
        <ul>
          <li>Hazard ratios & confidence intervals</li>
          <li>P-values</li>
          <li>Clinical significance</li>
        </ul>
      </div>
    </div>

  </section>


  <!-- Python Implementation Structure -->
  <section class="card">
    <h2>🖥️ Python Implementation Structure</h2>
    <p class="small">Key files & folders from the repository:</p>

    <table>
      <thead><tr><th>Path</th><th>Description</th></tr></thead>
      <tbody>
        <tr><td><code>/data/*.xlsx</code></td><td>Raw and cleaned clinical data</td></tr>
        <tr><td><code>/document/Publication.pdf</code></td><td>Trial study reference</td></tr>
        <tr><td><code>/results/*.png</code></td><td>All plots (KM, HR, Schoenfeld)</td></tr>
        <tr><td><code>Chlorhexidine_Survival_Analysis.ipynb</code></td><td>Main notebook</td></tr>
        <tr><td><code>requirements.txt</code></td><td>Dependencies</td></tr>
      </tbody>
    </table>

    <h3>📸 Visual Outputs</h3>
    <div class="img-grid">
      <img src="results/km_overall.png" alt="KM overall">
      <img src="results/km_trail_arm.png" alt="KM by arm">
      <img src="results/cox_forest_hr.png" alt="Forest HR">
      <img src="results/correl_heatmap.png" alt="Heatmap">
    </div>

  </section>


  <!-- Footer -->
  <div class="footer">
    <a class="badge" href="LICENSE">MIT License</a>
    <a class="badge" href="/mnt/data/interpretation_of_survival_analysis.docx">Download Interpretation Doc</a>
  </div>

</div>
</body>
</html>


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


 

