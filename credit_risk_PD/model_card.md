
   Model Card – Retail Loan PD Model

     1. Model Details

- **Model type:** Binary classification (Probability of Default)
- **Algorithms:**
  - Logistic Regression (baseline, interpretable)
  - Random Forest (non-linear comparator for higher AUC)
- **Primary metrics (hold-out test set):**
  - Logistic Regression AUC: 0.853
  - Random Forest AUC: 0.930

     2. Intended Use and Scope

- **Intended use:** Estimating PD for retail loan applications to support credit risk
  decisions and portfolio-level risk management.
- **Intended users:** Credit risk teams, model risk management, AI governance teams.
- **Out-of-scope:** Fully automated approvals/declines without human oversight; use on
  populations materially different from the training data.

     3. Data

- **Source:** Tabular loan-level dataset with demographic and loan characteristics.
- **Key features:** Age, income, loan amount, loan grade/intent, interest rate,
  home ownership, credit history length, prior default flag.
- **Preprocessing:** Categorical variables one-hot encoded; numeric variables used
  at native scale (no standardisation in this version).
- **Data quality checks:** Basic missing-value and distribution checks performed
  prior to modelling. Imputation applied for missing numeric values using median. 

     4. Evaluation and Validation

- **Metrics:** AUC, confusion matrix, precision/recall, and PD calibration curves.
- **Calibration:** Calibration curves were examined for both models; deviations from
  the diagonal would trigger recalibration or model redesign.
- **Threshold analysis:** Different PD cut-offs were explored to balance default
  recall vs overall accuracy.

     5. Explainability

- **Logistic Regression coefficients:** Used to interpret the direction and strength
  of each feature's effect on PD.
- **SHAP (TreeExplainer) for Random Forest:**
  - Case-level explanation generated to identify which features increased or
    decreased PD for a specific loan applicant.
  - Global summary plots used to identify the most influential features.
  - Dependence plots used to show how changes in key features affect predicted PD.


     6. Fairness and Ethical Considerations

- **Proxy sensitive attribute analysed:** Age, grouped into <30, 30–60, >60.
- **Metrics per group:** Default rate, predicted high-risk rate (PD > 0.50),
  false positive rate (FPR), and false negative rate (FNR).
- **Observations:** Any persistent gaps between age groups are treated as potential
  disparate impact and require further investigation (e.g. threshold tuning, feature
  review, or model simplification).
- **Limitations:** Only age was analysed here; a full assessment would cover more
  protected characteristics and intersectional groups, subject to data availability
  and legal constraints.


     7. Limitations and Next Steps

- **Scope limitations:** Single dataset, limited fairness dimensions, no stress
  testing of extreme scenarios.
- **Planned enhancements:**
  - Broader fairness analysis across additional attributes.
  - No drift monitoring and automation of the KRI dashboard.
  - Missing Governance aspects such as versioning, access controls, and audit trails.
  - Alignment with evolving AI regulations and internal AI governance standards.
