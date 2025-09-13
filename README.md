
---

# Advancing Statistical Models for Addressing Missing Data in HIV/AIDS Surveys  

![R](https://img.shields.io/badge/R-Advanced-blue?logo=r)  
![Python](https://img.shields.io/badge/Python-Supplementary-lightgrey?logo=python)  
![Machine Learning](https://img.shields.io/badge/ML-Random%20Forest%20+%20Decision%20Tree-orange)  
![Statistics](https://img.shields.io/badge/Statistics-Heckman%20Model%20+%20Imputation-red)  
![Public Health](https://img.shields.io/badge/Domain-HIV%2FAIDS%20Epidemiology-purple)  
![Accuracy](https://img.shields.io/badge/Accuracy-96.7%25%20(Random%20Forest)-green)

## Key Insights & Public Health Implications

### 1. Model Performance: Random Forest Dominates
| Model             | Accuracy | Sensitivity | Specificity | Precision | Business/Public Health Value                     |
|-------------------|----------|-------------|-------------|-----------|--------------------------------------------------|
| **Random Forest** | **96.7%**| 96.68%      | 97.22%      | 99.69%    | Best for clinical decision support — minimizes false negatives (missed HIV cases) |
| Decision Tree     | 97.65%   | 97.68%      | 97.42%      | 99.63%    | High accuracy + interpretability — good for policy |
| K-Means           | 97.41%   | 97.51%      | 96.95%      | 99.52%    | Unsupervised alternative when labels are scarce  |
| Heckman Model     | 95.54%   | 95.93%      | 95.66%      | 99.36%    | Corrects for selection bias — valuable for survey design |
| Mean/Median       | 97.38%   | 97.68%      | 95.23%      | 99.32%    | Baseline — outperformed by ML in specificity     |

> **Health Policy Takeaway**: “Use Random Forest for imputing HIV status and testing variables — its high sensitivity ensures no at-risk individual is missed.”

---

### 2. Domain Intelligence: You Speak Clinical + Data
- **Logical Data Cleaning**: Set `everpregnant = "Not Applicable"` for male records — preventing biologically impossible imputations.
- **Variable Understanding**: Mapped 20+ variables to domains:
  - **Clinical**: `hivstatusfinal`, `hivtstever`, `mcstatus` (male circumcision)
  - **Demographic**: `age_group`, `gender`, `province`
  - **Socioeconomic**: `wealthquintile`, `education`
  - **Behavioral**: `sexever`, `avoidpreg`, `curmar` (current marital status)
- **Missingness Patterns**: Found highest missingness in `hivstatusfinal` (critical outcome) and `mcstatus` (gender-specific) — prioritized these for imputation.

---

### 3. Exploratory Data Analysis (EDA) — Uncovering Health Disparities
- **Gender Imbalance**: 13,290 women vs. 9,461 men — critical for weighting and bias correction.
- **Rural Bias**: 3x more men and 2.4x more women from rural vs. urban areas — impacts generalizability.
- **Wealth Disparity**: “Lowest” wealth quintile most represented — suggests HIV programs must target low-income groups.
- **Education**: 97% of men and 90% of women attended school — high baseline, but missingness was negligible.

> **Program Design Insight**: “HIV interventions in Zimbabwe must prioritize rural, low-income populations — they’re overrepresented in surveys but may have least access to care.”

---

### 4. Advanced Methodology: Beyond Basic Imputation
#### ➤ Heckman Selection Model (Econometric Rigor)
- **Why Used**: To correct for **sample selection bias** — e.g., healthier individuals more likely to consent to HIV testing.
- **Two-Stage Process**:
  1. **Selection Equation**: Modeled probability of HIV test participation.
  2. **Outcome Equation**: Modeled HIV status, correcting for selection bias.
- **Result**: 95.5% Accuracy — lower than RF but methodologically vital for unbiased population estimates.

#### ➤ MCAR/MAR Diagnosis
- **MCAR (Missing Completely at Random)**: No pattern — e.g., data entry error.
- **MAR (Missing at Random)**: Pattern based on observed data — e.g., men less likely to report circumcision status.
- **Action**: Used MAR-aware models (RF, Heckman) — avoided naive listwise deletion.

#### ➤ Clinical Evaluation Metrics
- **Sensitivity (Recall)**: % of true HIV+ cases correctly identified — critical to avoid false negatives.
- **Specificity**: % of true HIV- cases correctly identified — reduces false positives.
- **Precision**: % of predicted HIV+ cases that are truly positive — builds trust in model.

> **Data Quality Insight**: “Don’t just use Accuracy — in healthcare, Sensitivity and Specificity are non-negotiable.”

---

## Technical Stack & Methodologies

| Area                  | Tools & Techniques                                                                 | Public Health Value                              |
|-----------------------|------------------------------------------------------------------------------------|--------------------------------------------------|
| **Machine Learning**  | Random Forest, Decision Trees, K-Means Clustering, Hyperparameter Tuning (n_estimators=500) | High-accuracy imputation for clinical variables  |
| **Advanced Statistics**| Heckman Selection Model, MCAR/MAR Diagnostics, Confusion Matrix Analysis          | Bias correction, survey representativeness       |
| **Data Engineering**  | Domain-aware cleaning (e.g., gender-specific logic), missing data detection, R/Python pipelines | Ensures biologically plausible imputations       |
| **Public Health Analytics** | HIV care continuum mapping, wealth/education disparity analysis, rural/urban stratification | Program targeting, resource allocation           |
| **Tool Proficiency**  | R (tidyverse, randomForest, tree, psych, ggplot2), Python (scikit-learn — implied) | Reproducible research, production deployment     |
| **Research & Ethics** | Reproducibility, documentation, ethical implications of imputation (e.g., false negatives) | Regulatory compliance, responsible AI            |

---

## Repository Structure

```
├── ADVANCING STATISTICAL MODELS FOR ADDRESSING MISSING DATA.pdf  # Full thesis (7,951 words)
├── code/
│   ├── data_cleaning.R             # Domain-aware cleaning (e.g., male pregnancy = "Not Applicable")
│   ├── eda_gender_wealth.R        # EDA: gender, wealth, rural/urban disparities
│   ├── imputation_rf_dt.R         # Random Forest + Decision Tree imputation
│   ├── imputation_heckman.R       # Heckman Selection Model implementation
│   ├── imputation_kmeans.R        # K-Means clustering for unsupervised imputation
│   └── model_evaluation.R         # Calculate Accuracy, Sensitivity, Specificity, Precision
├── data/
│   └── zimphia_2020.csv           # ZIMPHIA 2020 survey data (22,751 individuals, 20+ variables)
├── screenshots/
│   ├── model_comparison_table.png # RF 96.7% Accuracy vs. Heckman 95.5%
│   ├── rural_urban_barplot.png    # 3x more rural men, 2.4x more rural women
│   ├── wealth_quintile_chart.png  # "Lowest" quintile most represented
│   └── missingness_heatmap.png    # Highest missingness in hivstatusfinal, mcstatus
└── README.md                      # You are here!
```

---

## How to Run

1. Clone this repo:
   ```bash
   git clone https://github.com/chinonso-okoroafor/hiv-missing-data-imputation.git
   cd hiv-missing-data-imputation
   ```

2. Install R dependencies:
   ```r
   install.packages(c("tidyverse", "randomForest", "tree", "psych", "ggplot2"))
   ```

3. Run analysis scripts:
   ```r
   source("code/data_cleaning.R")
   source("code/eda_gender_wealth.R")
   source("code/imputation_rf_dt.R")
   source("code/imputation_heckman.R")
   source("code/model_evaluation.R")
   ```

> Data sourced from PHIA Project (ZIMPHIA 2020).

## References & Tools

- **Dataset**: Population-based HIV Impact Assessment (PHIA) Project — ZIMPHIA 2020  
- **ML Algorithms**:  
  - Random Forest — Breiman, L. (2001)  
  - Heckman Model — Heckman, J. (1979) — *Sample Selection Bias as a Specification Error*  
- **R Packages**: `randomForest`, `tree`, `psych`, `ggplot2`, `tidyverse`  
- **Public Health Frameworks**: UNAIDS 95-95-95 Targets, HIV Care Continuum  
- **Ethics**: GDPR/HIPAA-aware imputation, false negative minimization

---

## Connect & Collaborate

👤 **Author**: [Chinonso Okoroafor]  
📧 **Email**: [chinonso.okoroafor@outlook.com]  
💼 **LinkedIn**: [https://www.linkedin.com/in/chinonso-okoroafor-57086a284]  
🎓 **Program**: MSc Data Science and Business Analytics, University of Plymouth  
🌍 **Thesis Supervisor**: Dr. Malgorzata Wojtys
