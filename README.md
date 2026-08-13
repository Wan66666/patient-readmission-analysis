# Patient Readmission Prediction

A predictive analysis project identifying which diabetic patients are most likely to be readmitted to hospital within 30 days of discharge, using a real-world clinical dataset of 100,000+ patient encounters.

## Project Overview

This project builds and evaluates classification models to predict 30-day hospital readmission risk, featuring:
- Real-world clinical data cleaning with leakage-prevention (deduplication to one encounter per patient)
- Comparison of three modeling approaches: Logistic Regression, Random Forest, and XGBoost
- Statistical hypothesis testing to confirm key findings
- An actionable risk-tiering system translating model output into a usable prioritization tool
- Interactive summary page presenting results for a non-technical audience

## Features

### Data Analysis
- **Data Cleaning**: Missing value handling, patient-level deduplication, exclusion of non-meaningful outcomes
- **Feature Engineering**: Age grouping, medication load, prior-visit history
- **Exploratory Analysis**: Readmission rate patterns by age, prior admissions, length of stay
- **Statistical Testing**: Chi-square, two-proportion z-test, and ANOVA to confirm EDA findings
- **Predictive Modeling**: Logistic Regression, Random Forest, and XGBoost, compared via ROC-AUC and 5-fold cross-validation
- **Risk Stratification**: Low/Medium/High patient risk tiers for operational use

### Interactive Visualizations
- Readmission rate by age group and prior admission history
- Length of stay and medication changes vs readmission outcome
- Random Forest feature importance ranking
- Risk tier gauge with capture-rate callout

## Technologies Used

- **Language**: Python
- **Data & Modeling**: pandas, scikit-learn, XGBoost, SciPy
- **Visualization**: matplotlib, seaborn
- **Notebook Environment**: Jupyter
- **Summary Page**: HTML5, CSS3 (self-contained, no external dependencies)
- **Fonts**: Google Fonts (Fraunces, IBM Plex Sans, IBM Plex Mono)

## Project Structure

```
patient-readmission-analysis/
├── index.html                            # Interactive summary page (live dashboard)
├── Patient_Readmission_Prediction.ipynb  # Full analysis notebook
└── README.md
```

## Live Demo

Visit the live summary page: [Patient Readmission Prediction](https://wan66666.github.io/patient-readmission-analysis/)

## Key Findings

- **Prior Admission History**: Patients with a prior inpatient stay are readmitted at nearly 2x the rate of those without one (15.4% vs 8.2%, p < 0.001)
- **Age**: Senior patients (60+) show a meaningfully higher readmission rate (~10.0%) than younger groups (~7.2–7.3%)
- **Model Performance**: All three algorithms (Logistic Regression, Random Forest, XGBoost) converge on a similar ROC-AUC ceiling (~0.63–0.64), suggesting the limitation is in available features rather than modeling technique
- **Risk Tiering**: The top 20% highest-risk patients account for 32.8% of all actual 30-day readmissions

## Local Development

1. Clone the repository:
   ```bash
   git clone https://github.com/Wan66666/patient-readmission-analysis.git
   cd patient-readmission-analysis
   ```

2. View the summary page locally:
   ```bash
   python -m http.server 8000
   ```
   Then open `http://localhost:8000` in your browser.

3. To run the notebook, install dependencies and launch Jupyter:
   ```bash
   pip install pandas scikit-learn xgboost scipy matplotlib seaborn jupyter
   jupyter notebook Patient_Readmission_Prediction.ipynb
   ```

## Data Source

- [Diabetes 130-US Hospitals for Years 1999–2008](https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008), UCI Machine Learning Repository
- 101,766 raw hospital encounters across 130 US hospitals, cleaned to 67,112 unique patients
- Variables: demographics, admission/discharge details, lab results, medications, diagnoses

## Analysis Methodology

1. **Data Cleaning**: Handled missing values, removed duplicate patient encounters to prevent train/test leakage, excluded death/hospice discharges
2. **Feature Engineering**: Age grouping, medication counts, prior-visit history features
3. **Exploratory Analysis**: Identified prior inpatient history and age as strong readmission signals
4. **Statistical Testing**: Confirmed key findings with chi-square, two-proportion z-test, and ANOVA (all p < 0.001)
5. **Modeling**: Compared three algorithms using ROC-AUC (not just accuracy, given ~9% class imbalance), validated with 5-fold cross-validation
6. **Risk Stratification**: Translated model output into a Low/Medium/High risk framework for operational use

## Data Limitations

- Historical dataset (1999–2008); patterns may not reflect current clinical practice
- Diagnosis codes (`diag_1/2/3`) excluded from modeling for simplicity — likely a source of unused predictive signal
- Model performance is modest (ROC-AUC ~0.63); consistent with published benchmarks on this dataset, but leaves room for improvement
- Single-year-per-patient snapshot; no longitudinal tracking beyond the recorded encounters

## Results Summary

| Model | Accuracy | ROC-AUC (5-fold CV) |
|---|---|---|
| Logistic Regression | 65.7% | 0.643 ± 0.004 |
| Random Forest | 71.4% | 0.633 ± 0.006 |
| XGBoost | 69.0% | 0.638 ± 0.002 |

## Author

- **Ethan Wan** - [Wan66666](https://github.com/Wan66666)

## Acknowledgments

- Dataset provided by the UCI Machine Learning Repository
- Built with guidance and pair-analysis support from Claude (Anthropic)

---

*Created as a data analytics portfolio project to demonstrate end-to-end analysis: data cleaning, statistical testing, predictive modeling, and business-oriented communication of results.*
