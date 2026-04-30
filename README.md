# Codveda Technology — Business Analytics Internship

> **Track:** Business Analytics  
> **Duration:** 15-day internship  
> **Levels completed:** 3 of 3  
> **Tasks completed:** 6 of 6

---

## Repository Structure

```
codveda-business-analytics/
│
├── data/
│   ├── churn-bigml-80.csv          ← Telecom churn training set (raw)
│   ├── churn-bigml-20.csv          ← Telecom churn test set (raw)
│   ├── churn_cleaned.csv           ← Merged, cleaned churn dataset (output of Level 1)
│   ├── 1__iris.csv                 ← Iris flower dataset
│   ├── iris_cleaned.csv            ← Cleaned iris dataset
│   ├── 3__Sentiment_dataset.csv    ← Social media sentiment dataset
│   ├── 4__house_Prediction_Data_Set.csv  ← Boston housing (raw)
│   └── house_cleaned.csv           ← Boston housing (parsed, named columns)
│
├── Level_1/                        ← Basic Analytics
│   ├── Task2_Data_Cleaning.ipynb
│   ├── Task3_EDA.ipynb
│   └── charts/                     ← All saved visualisations
│
├── Level_2/                        ← Intermediate Analytics
│   ├── Task2_SQL_Analytics.ipynb
│   ├── Task3_Statistical_Analysis.ipynb
│   └── charts/
│
├── Level_3/                        ← Advanced Analytics
│   ├── Task1_Predictive_ML.ipynb
│   ├── Task2_Risk_Fraud_Detection.ipynb
│   └── charts/
│
└── README.md
```

---

## Quick Start

```bash
# 1. Clone
git clone https://github.com/bra-charles/codveda-business-analytics.git
cd codveda-business-analytics

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn scipy jupyter

# 3. Launch Jupyter
jupyter notebook

# 4. Run notebooks in order:
#    Level_1/Task2 → Level_1/Task3 → Level_2/Task2 → Level_2/Task3 → Level_3/Task1 → Level_3/Task2
```

> **Note:** Level 1 Task 2 generates `churn_cleaned.csv` and `iris_cleaned.csv` which are used by all subsequent notebooks. Run it first.

---

## Level 1 — Basic Analytics

### Task 2: Data Collection & Cleaning
**Datasets:** Churn (train + test merged), Iris  
**Techniques:** Missing value imputation (median/mode by dtype), IQR outlier capping (Winsorization), StandardScaler + MinMaxScaler, Label Encoding + One-Hot Encoding

**Reusable functions built:**
- `audit_dataframe()` — full data quality report
- `handle_missing_values()` — dtype-aware imputation
- `detect_outliers_iqr()` / `cap_outliers_iqr()` — outlier handling
- `scale_features()` — multi-scaler comparison
- `encode_categoricals()` — label + one-hot encoding

**Charts:** missing_values_treatment, outlier_boxplots, scaling_distributions

---

### Task 3: Exploratory Data Analysis
**Datasets:** Churn (cleaned), Iris (cleaned)  
**Techniques:** Descriptive statistics (mean/median/mode/skew/kurtosis), distribution analysis, correlation heatmaps, trend analysis, anomaly detection, linear regression

**Key findings:**
| Finding | Detail |
|---------|--------|
| Churn rate | 14.5% of customers churned |
| Service calls | 4+ calls = sharp churn spike |
| International plan | Churn rate ~3× higher vs non-subscribers |
| Day charge linearity | R² ≈ 1.0 (deterministic pricing formula) |
| Iris separability | Petal features cleanly separate species |

**Charts:** churn_distribution, churn_histograms, iris_pairplot, scatter_churn, usage_trends, anomaly_detection, correlation_heatmaps (×2), regression_day_minutes, iris_species_boxplots

---

## Level 2 — Intermediate Analytics

### Task 2: SQL for Business Analytics
**Dataset:** Churn  
**Techniques:** SQLite in-memory database (3 normalised tables), SELECT/WHERE/GROUP BY/HAVING, multi-table JOINs (2-table + 3-table), subqueries, CTEs, window functions (RANK + running totals), query optimisation with indexes

**KPIs extracted:**
| KPI | Value |
|-----|-------|
| Total customers | 3,333 |
| Churn rate | 14.49% |
| Total revenue | $198,169 |
| Revenue lost to churn | $31,554 |

**Charts:** churn_by_state, service_calls_churn, bi_dashboard

---

### Task 3: Statistical Analysis
**Datasets:** Churn, Sentiment  
**Techniques:** Probability distributions (Normal, Poisson, Exponential), Welch's t-tests, Chi-Square tests, A/B testing with lift calculation, 95% confidence intervals, binomial risk modelling

**Key results:**
| Test | Variables | p-value | Significant? |
|------|-----------|---------|-------------|
| t-test | Day minutes vs churn | < 0.0001 | ✅ Yes |
| t-test | Day charge vs churn | < 0.0001 | ✅ Yes |
| t-test | Account length vs churn | 0.2556 | ❌ No |
| Chi-Square | International plan vs churn | < 0.0001 | ✅ Yes |
| Chi-Square | Voicemail plan vs churn | < 0.0001 | ✅ Yes |

**Charts:** distributions, ttest_distributions, chi2_test, ab_test_results, confidence_intervals, sentiment_analysis, churn_risk_distribution

---

## Level 3 — Advanced Analytics

### Task 1: Predictive Analytics & Machine Learning
**Datasets:** Boston Housing (regression), Churn (classification + clustering)

#### Regression — House Price Prediction
| Model | R² | RMSE |
|-------|-----|------|
| Linear Regression | 0.6688 | $4,929 |
| Ridge Regression | 0.6685 | $4,931 |
| Random Forest | 0.8921 | $2,813 |
| **Gradient Boosting** | **0.9153** | **$2,492** |

Top price drivers: LSTAT (lower-status %), RM (avg rooms), PTRATIO (pupil-teacher ratio)

#### Classification — Churn Prediction
| Model | Accuracy | ROC-AUC |
|-------|----------|---------|
| Logistic Regression | 85.76% | 0.7771 |
| Gradient Boosting | 94.00% | 0.9096 |
| **Random Forest** | **95.65%** | **0.9212** |

Top churn predictors: Total day minutes, International plan, Customer service calls

#### Clustering — Customer Segmentation (K-Means, k=4)
| Segment | Profile | Recommended Action |
|---------|---------|-------------------|
| Light Users | Low usage across all periods | Upsell campaigns |
| Heavy Day Users | Very high day minutes & charge | Retention priority |
| Balanced Users | Moderate all-round usage | Standard service |
| High Support Seekers | Many service calls | Proactive support outreach |

**Charts:** regression_comparison, feature_importance_regression, classification_results, feature_importance_churn, cluster_optimal_k, customer_segmentation, segment_radar

---

### Task 2: Risk Analysis & Fraud Detection
**Dataset:** Churn

#### Anomaly Detection
| Method | Anomalies Found | Approach |
|--------|----------------|----------|
| Z-Score | Low (>3σ) | Univariate, simple |
| IQR | Moderate | Univariate, robust |
| **Isolation Forest** | **167 (5.0%)** | **Multivariate ML — best method** |

#### Risk Scorecard (Weighted Rules, 0–100)
6 business rules mapping to churn probability — Very High Risk tier shows highest actual churn rate, validating the approach.

#### Fraud Detection ML
| Model | ROC-AUC | Avg Precision |
|-------|---------|--------------|
| **Gradient Boosting** | **0.9400** | **0.9138** |
| Random Forest | 0.9333 | 0.9114 |
| Logistic Regression | 0.8025 | 0.4337 |

#### Threshold Optimisation
- Optimal F1 threshold: **0.27** (vs default 0.5)
- Min business-cost threshold: **0.27** (FP=$5, FN=$50 model)
- Result: 471 customers flagged, 100% precision, **$30,845** revenue at risk identified

**Charts:** anomaly_detection_ml, risk_scorecard, fraud_detection_models, threshold_optimisation, risk_management_strategy

---

## Tools & Libraries

| Tool | Version | Purpose |
|------|---------|---------|
| Python | 3.10+ | Core language |
| pandas | latest | Data manipulation |
| numpy | latest | Numerical computing |
| matplotlib / seaborn | latest | Visualisations |
| scikit-learn | latest | ML models, preprocessing, metrics |
| scipy | latest | Statistical testing |
| SQLite (stdlib) | built-in | SQL analytics |
| Jupyter | latest | Interactive notebooks |

---

## Notes

- Each notebook is **self-contained** with full comments and docstrings on all reusable functions
- `SimpleImputer(strategy='median')` is applied before scaling in Level 3 notebooks — the cleaned CSV retains a small number of NaNs from Level 1's synthetic injection
- Charts auto-save as `.png` in each level's `charts/` subfolder
- Run notebooks **in order within each level**: Task 2 always before Task 3, Level 1 before Level 2 before Level 3

---


