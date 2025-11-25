<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Survival Analysis — Chlorhexidine Trial</title>
<style>
  :root{
    --c1:#0ea5a3;    /* teal */
    --c2:#06b6d4;    /* cyan */
    --dark:#0f172a;
    --muted:#64748b;
    --bg:#ffffff;
    --card:#f7fffb;
    --wide:1150px;
    --font: "Inter", "Segoe UI", Roboto, Arial, sans-serif;
  }
  body{
    margin:0; padding:28px;
    background:linear-gradient(180deg,#f0fdfa 0%, #ffffff 100%);
    font-family:var(--font); color:var(--dark);
    display:flex; justify-content:center;
  }
  .page{
    width:100%; max-width:var(--wide);
  }
  header{
    display:flex; justify-content:space-between; align-items:flex-start; gap:16px;
  }
  h1{ font-size:30px; margin:0; }
  .subtitle{ color:var(--muted); margin-top:6px; font-size:13px; }
  .badge{
    display:inline-block;
    background:linear-gradient(90deg,var(--c1),var(--c2));
    color:#fff; padding:8px 12px; border-radius:20px; text-decoration:none; font-weight:700;
  }

  .row{ display:flex; gap:18px; flex-wrap:wrap; margin-top:18px; }
  .col{ flex:1 1 48%; min-width:300px; }

  .card{
    background:var(--card);
    border-left:6px solid var(--c1);
    padding:16px 18px; border-radius:12px;
    box-shadow:0 6px 20px rgba(2,6,23,0.05);
  }
  h2{ margin:8px 0 10px; font-size:20px; }
  h3{ margin:6px 0; font-size:16px; color:var(--dark); }
  ul{ margin:8px 0 12px 18px; }
  table{ width:100%; border-collapse:collapse; margin-top:10px; font-size:14px; }
  th,td{ text-align:left; padding:8px 10px; border-bottom:1px solid #e6eef1; }
  th{ font-weight:700; background:transparent; }

  .flow{
    display:flex; gap:12px; align-items:stretch; margin-top:12px; flex-wrap:wrap;
  }
  .flow > div{ flex:1 1 calc(25% - 12px); min-width:200px; background:#fff; padding:12px; border-radius:10px; border:1px solid rgba(6,95,70,0.06);}
  .flow-title{ font-weight:700; margin-bottom:6px; color:var(--c1); }

  .images{ display:grid; grid-template-columns:repeat(auto-fit,minmax(220px,1fr)); gap:12px; margin-top:12px; }
  .imgwrap{ border-radius:10px; overflow:hidden; background:#fff; padding:8px; border:1px solid #eef6f5; }
  img{ width:100%; height:auto; display:block; border-radius:6px; }

  .footer{ margin-top:22px; padding-top:16px; border-top:1px dashed #e6eef1; display:flex; justify-content:space-between; flex-wrap:wrap; gap:12px; }
  .linkbtn{ background:var(--c2); color:white; padding:8px 12px; border-radius:10px; text-decoration:none; font-weight:700; }

  @media (max-width:880px){
    .col{ flex-basis:100%; }
    .flow > div{ flex-basis:100%; }
  }
</style>
</head>
<body>
  <div class="page">
    <header>
      <div>
        <h1>Survival Analysis — Chlorhexidine Trial</h1>
        <div class="subtitle">Kaplan–Meier • Log-Rank • Cox PH • Schoenfeld diagnostics</div>
      </div>
      <div style="text-align:right">
        <a class="badge" href="LICENSE">MIT License</a>
      </div>
    </header>

    <!-- Top summary -->
    <div class="row" style="margin-top:18px;">
      <div class="col card">
        <h2>Project Summary</h2>
        <p>
          Analysis of a clinical trial comparing <strong>0.12% vs 0.20% chlorhexidine</strong> mouthwash for prevention of Ventilator-Associated Pneumonia (VAP).
          Workflow implements Kaplan–Meier estimation, Log-Rank comparison, multivariable Cox Proportional Hazards modelling, Schoenfeld residual checks, and presentation-ready plots.
        </p>
        <ul>
          <li>Events observed were few (7 events in the analysis set), limiting statistical power.</li>
          <li>0.20% arm shows a small visual advantage but the difference is not statistically significant (log-rank p = 0.16).</li>
        </ul>
      </div>

      <div class="col card">
        <h2>Quick Links</h2>
        <p style="margin:6px 0 12px;">Key files in this repository (see folders shown in repo view):</p>
        <table>
          <thead><tr><th>Path</th><th>Purpose</th></tr></thead>
          <tbody>
            <tr><td>/data/Chlorhexidine Trials.xlsx</td><td>Cleaned dataset</td></tr>
            <tr><td>/document/Publication.pdf</td><td>Original study paper</td></tr>
            <tr><td>/results/</td><td>All plots & CSV tables</td></tr>
            <tr><td>Chlorhexidine_Survival_Analysis.ipynb</td><td>Jupyter analysis notebook</td></tr>
          </tbody>
        </table>
        <p style="margin-top:10px;">
          <a class="linkbtn" href="/mnt/data/interpretation_of_survival_analysis.docx">Download interpretation doc</a>
          <!-- Cite the interpretation doc included in repo -->
          <div style="font-size:12px;color:var(--muted);margin-top:8px;">Full interpretation document included. :contentReference[oaicite:0]{index=0}</div>
        </p>
      </div>
    </div>

    <!-- Dataset & Problem / Objectives -->
    <div class="row" style="margin-top:18px;">
      <div class="col card">
        <h2>Dataset Description</h2>
        <table>
          <thead><tr><th>Column</th><th>Description</th><th>Type</th></tr></thead>
          <tbody>
            <tr><td>time</td><td>Days until VAP or censoring</td><td>Continuous</td></tr>
            <tr><td>event</td><td>1 = VAP, 0 = censored</td><td>Binary</td></tr>
            <tr><td>Age</td><td>Patient age (years)</td><td>Numeric</td></tr>
            <tr><td>Gender</td><td>Male / Female</td><td>Categorical</td></tr>
            <tr><td>chest_xray, culture, ulcer</td><td>Clinical indicators</td><td>Binary</td></tr>
            <tr><td>apache_score, tlc_score, microbial_load</td><td>Severity & infection markers</td><td>Numeric</td></tr>
            <tr><td>treatment_arm</td><td>1 = 0.12% | 2 = 0.20%</td><td>Categorical</td></tr>
          </tbody>
        </table>
      </div>

      <div class="col card">
        <h2>Problem Statement & Objectives</h2>
        <h3>Problem</h3>
        <p>Does 0.20% chlorhexidine reduce the incidence and hazard of VAP compared to 0.12%? Which baseline factors influence time-to-VAP?</p>
        <h3>Objectives</h3>
        <ul>
          <li>Compare VAP-free survival across arms (KM + Log-Rank).</li>
          <li>Estimate hazard ratios via Cox PH for clinical predictors.</li>
          <li>Validate PH assumption (Schoenfeld residuals).</li>
          <li>Produce adjusted survival curves and forest plots for interpretation.</li>
        </ul>
      </div>
    </div>

    <!-- Methodology horizontal flow -->
    <section style="margin-top:18px;">
      <div class="card">
        <h2>Methodology — Horizontal Flow</h2>
        <div class="flow" role="list">
          <div role="listitem">
            <div class="flow-title">6.1 Data Preparation</div>
            <div>Import dataset, clean & rename columns, encode categories, create survival objects (time, event), impute missing numeric values (median).</div>
          </div>
          <div role="listitem">
            <div class="flow-title">6.2 Exploratory Data Analysis</div>
            <div>Distribution of events vs censored, summary statistics, histograms, boxplots, correlation heatmap.</div>
          </div>
          <div role="listitem">
            <div class="flow-title">6.3 Survival Modelling</div>
            <div>Kaplan–Meier (overall & by arm), life tables, Log-Rank test, Cox PH model, Schoenfeld diagnostics.</div>
          </div>
          <div role="listitem">
            <div class="flow-title">6.4 Model Evaluation</div>
            <div>Hazard ratios, 95% CI, p-values, forest plots, adjusted survival curves, interpret clinical relevance and limitations.</div>
          </div>
        </div>
      </div>
    </section>

    <!-- Implementation structure and images -->
    <div class="row" style="margin-top:18px;">
      <div class="col card">
        <h2>Implementation Structure</h2>
        <p class="small">Main code & outputs (see repo):</p>
        <table>
          <thead><tr><th>File / Folder</th><th>Purpose</th></tr></thead>
          <tbody>
            <tr><td>/data/Chlorhexidine Trials.xlsx</td><td>Cleaned raw data</td></tr>
            <tr><td>/document/Publication.pdf</td><td>Original article</td></tr>
            <tr><td>/results/*.png</td><td>Plot outputs (KM, Schoenfeld, HR)</td></tr>
            <tr><td>Chlorhexidine_Survival_Analysis.ipynb</td><td>Notebook of analysis</td></tr>
          </tbody>
        </table>

        <h3 style="margin-top:12px;">Selected Visuals</h3>
        <div class="images">
          <div class="imgwrap"><img src="results/km_overall.png" alt="KM overall"><div style="font-size:13px;color:var(--muted);margin-top:6px;">km_overall.png (Overall KM)</div></div>
          <div class="imgwrap"><img src="results/km_trail_arm.png" alt="KM by arm"><div style="font-size:13px;color:var(--muted);margin-top:6px;">km_trail_arm.png (By trial arm)</div></div>
          <div class="imgwrap"><img src="results/correl_heatmap.png" alt="Correlation heatmap"><div style="font-size:13px;color:var(--muted);margin-top:6px;">correl_heatmap.png</div></div>
          <div class="imgwrap"><img src="results/cox_forest_hr.png" alt="Forest plot"><div style="font-size:13px;color:var(--muted);margin-top:6px;">cox_forest_hr.png (Hazard ratios)</div></div>
        </div>
      </div>

      <div class="col card">
        <h2>Key Results & Interpretation</h2>
        <ul>
          <li>Overall survival remained high; small decline between days 2–6; survival ≈ 0.92 at day 10.</li>
          <li>KM by arm: 0.20% trends better but <strong>log-rank p = 0.16</strong> (not significant).</li>
          <li>Cox PH: wide CIs, no significant predictors — limited by low events (7).</li>
          <li>PH diagnostics: Schoenfeld residuals p-values > 0.05 for all covariates (PH assumption satisfied).</li>
        </ul>

        <h3 style="margin-top:8px;">Files of interest</h3>
        <ul>
          <li><code>results/logrank_two_arm_table.csv</code> — Log-Rank test table</li>
          <li><code>results/cox_hr_table_final.csv</code> — Cox summary (HR, CI, p)</li>
          <li><code>results/ss_r_*.png</code> — Schoenfeld residual plots per variable</li>
        </ul>
      </div>
    </div>

    <!-- Discussion, Conclusion, Future Work -->
    <div class="row" style="margin-top:18px;">
      <div class="col card">
        <h2>Discussion</h2>
        <p style="margin-top:6px;">
          The analysis indicates similar VAP-free survival across both chlorhexidine concentrations in the 10-day window. Low event count reduces ability to detect moderate effects — results should be interpreted conservatively.
        </p>
      </div>

      <div class="col card">
        <h2>Conclusion & Future Work</h2>
        <ul>
          <li>No statistically significant difference between 0.12% and 0.20% in this dataset.</li>
          <li>Recommend larger, multi-centre studies or longer follow-up to increase events and power.</li>
          <li>Future: time-varying covariates, parametric survival models, and machine-learning survival methods.</li>
        </ul>
      </div>
    </div>

    <!-- Footer -->
    <div class="footer">
      <div>
        <a class="linkbtn" href="/mnt/data/interpretation_of_survival_analysis.docx">Open interpretation doc</a>
      </div>
      <div style="display:flex;gap:12px;align-items:center;">
        <a class="badge" href="LICENSE">MIT License</a>
        <div style="color:var(--muted);font-size:13px;">Report prepared by: Vaishnavi K R — PGDM (AI & Data Science), IIHMR Bangalore</div>
      </div>
    </div>

  </div>
</body>
</html>
