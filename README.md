# Credit-Risk-Prediction-for-Small-Business-Loans
1. Project Overview

This project focuses on predicting the likelihood of default for small business loans using historical data from the U.S. Small Business Administration (SBA).
The objective is to build a credit risk model that can flag high-risk loans at the time of approval, enabling lenders to make informed decisions and reduce potential losses.

The project demonstrates the full pipeline from data exploration to feature engineering, model development, evaluation, and explainability.

2. Business Context

Small businesses play a critical role in economic growth. However, defaults on small business loans can lead to significant financial losses for lending institutions and impact broader economic stability.

Early identification of high-risk loans allows lenders to:

Adjust underwriting strategies

Price loans according to risk

Minimize non-performing assets

Strengthen portfolio quality

Business goal:
Predict whether a loan will be charged off (default) or paid in full at the time of approval, using available borrower, loan, and sector features.

3. Dataset Description

Source: U.S. SBA Loan Data (publicly available)
Records: Approximately 899,000
Columns: 27

Key variables:

GrAppv: Gross loan amount approved

SBA_Appv: Amount guaranteed by SBA

NAICS: Sector classification code

RevLineCr, LowDoc: Loan program flags

MIS_Status: Target variable – CHGOFF (default) or PIF (paid in full)

Borrower geography, bank information, dates of approval and disbursement.

4. Methodology

The project follows a structured workflow:

Exploratory Data Analysis (EDA)

Examined target distribution and sector-level default rates.

Identified patterns across states, urban vs. rural regions, loan sizes, and approval years.

Feature Engineering

Extracted sector from NAICS codes.

Derived key ratios:

loan_to_sba_ratio

disb_to_approved_ratio

disb_per_employee

Computed time-based features:

days_approval_to_disb

approval_year

Encoded categorical variables and handled missing values.

Modeling

Established a baseline with Logistic Regression.

Trained and tuned an XGBoost model with hyperparameter optimization.

Addressed class imbalance using scale_pos_weight.

Evaluation

Used AUC, Average Precision, precision, recall, and confusion matrix for assessment.

Compared model performance against the baseline.

Explainability

Used SHAP values to identify the most influential features driving default risk.

Generated both global and local explanations for interpretability.

5. Key Insights from EDA

Sectors such as food, retail, and accommodation exhibited higher default rates compared to others.

Urban borrowers showed slightly higher default rates than rural borrowers.

Loans approved during 2008–2010 had a noticeable increase in default rates, likely linked to the economic downturn.

Higher loan amounts were correlated with increased risk, but sector context had a significant influence.

6. Modeling Results
Model	AUC	Recall (Default)	Precision (Default)	Average Precision
Logistic Regression	0.819	0.83	0.37	0.465
XGBoost (Tuned)	0.9797	0.92	0.78	0.9216

The tuned XGBoost model significantly outperformed the baseline, achieving an AUC close to 0.98 and high recall on the default class. This means the model can flag most risky loans while maintaining strong precision.

7. Feature Importance and Explainability

Top features influencing default risk:

Gross approved loan amount (GrAppv)

SBA guarantee ratio (loan_to_sba_ratio)

Sector classification (sector2)

Urban vs rural indicator (UrbanRural)

Loan term (Term)

SHAP analysis confirmed that these features align with real-world lending risk factors, supporting the interpretability and potential deployability of the model.

8. Business Implications

The model can identify high-risk loans at the approval stage, enabling risk-based underwriting.

Even a small improvement in default prediction accuracy can translate into significant cost savings for lenders.

Explainability ensures the model can be reviewed by credit officers and meet regulatory expectations.

High recall ensures minimal missed defaults, while acceptable precision keeps the flagged loan pool manageable.
