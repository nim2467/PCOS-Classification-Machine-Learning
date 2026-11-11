# PCOS Classification Using Machine Learning

[**English**](README.md) | [Deutsch](README.de.md)

## Project Overview

This project investigates the classification of polycystic ovary syndrome (PCOS) using clinical and lifestyle-related features. The work compares several supervised learning algorithms and evaluates how well they distinguish observations labeled `PCOS (Y/N)`.

**Goal:** Build and compare reproducible binary classification models, paying particular attention to recall, precision, F1-score and ROC-AUC for the positive PCOS class. The analysis is exploratory and must not be used to make clinical decisions.



## Methodology

1. **Cleaning:** Standardize column names, inspect missing data and duplicates, remove identifiers and selected features
2. **Feature engineering:** Combine left/right follicle measurements into maximum-value features
3. **Exploration:** Explore distributions, relationships and potential outliers using descriptive statistics and visualizations
4. **Training:** Use a stratified 80/20 split and five-fold stratified cross-validation on the training set
5. **Models:** Compare Logistic Regression, Decision Tree, Random Forest and XGBoost, plus a dummy baseline
6. **Optimization:** Tune hyperparameters using GridSearchCV or RandomizedSearchCV with ROC-AUC as the selection metric. Address class imbalance through class weighting or XGBoost's `scale_pos_weight`
7. **Evaluation:** Evaluate ROC-AUC, PR-AUC, precision, recall, specificity, F1 and additional diagnostics on the held-out test split

## Results

Results below are **taken from saved notebook outputs**, not from an independent rerun. Models were selected/tuned using training cross-validation; the table reports held-out test performance with a 0.5 decision threshold.

| Model | Test ROC-AUC | Precision (PCOS) | Recall (PCOS) | F1-score |
|---|---:|---:|---:|---:|
| Random Forest | **0.9547** | **0.9667** | 0.8056 | **0.8788** |
| XGBoost | 0.9486 | 0.8857 | **0.8611** | 0.8732 |
| Logistic Regression | 0.9326 | 0.7750 | **0.8611** | 0.8158 |
| Decision Tree | 0.9422 | 0.7949 | **0.8611** | 0.8267 |

**Selected model:** Random Forest, based on the highest training cross-validation ROC-AUC (0.9595). Its held-out test ROC-AUC was 0.9547. XGBoost attained a higher recall (0.8611 versus 0.8056), highlighting a relevant trade-off for screening-oriented use cases.

## Interpretation and Limitations

- The dataset is relatively small and reflects a specific collection process; generalization to other populations is uncertain
- Results come from one held-out test split and have not been externally validated
- Feature importance provides an indication of predictive association, **not causality**
- In a health-related task, missed positive cases matter. A different classification threshold could change the recall/precision balance; it has not been established as clinically appropriate
- This project is for learning and methodological demonstration only, **not clinical diagnosis**
