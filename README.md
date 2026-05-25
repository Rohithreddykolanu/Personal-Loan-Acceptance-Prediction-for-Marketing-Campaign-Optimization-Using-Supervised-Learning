<h1 align="center">Personal Loan Acceptance Prediction for Marketing Campaign Optimization</h1>

<p align="center"><i>Using Supervised Learning</i></p>

<p align="center">
  <img alt="Python" src="https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white">
  <img alt="pandas" src="https://img.shields.io/badge/pandas-2.2-150458?logo=pandas&logoColor=white">
  <img alt="NumPy" src="https://img.shields.io/badge/NumPy-2.0-013243?logo=numpy&logoColor=white">
  <img alt="scikit-learn" src="https://img.shields.io/badge/scikit--learn-1.6-F7931E?logo=scikitlearn&logoColor=white">
  <img alt="Matplotlib" src="https://img.shields.io/badge/Matplotlib-3.10-11557C">
  <img alt="seaborn" src="https://img.shields.io/badge/seaborn-0.13-4C72B0">
</p>

## Overview

AllLife Bank is a mid sized and fast growing financial institution in the United States that offers savings and checking accounts, fixed deposits, and personal loans. The bank holds a large base of liability customers (depositors) but has comparatively few asset customers (borrowers). To grow interest income, it wants to convert existing depositors into personal loan customers. A pilot campaign last year reached a 9 percent conversion rate, which validated the strategy but also highlighted the need for a more data driven approach to targeting. This project builds a supervised classification model that predicts which liability customers are most likely to accept a personal loan, so the marketing team can target the right segments, reduce wasted spend, and improve conversion.

## Problem Statement

The goal is to develop a predictive classification model that identifies the demographic and behavioural factors driving personal loan adoption among existing liability customers. By understanding these drivers, the bank can move from broad outreach to precise segmentation, raise campaign conversion rates, optimize marketing spend, and grow a higher quality loan portfolio.

## Dataset

The dataset contains **5,000 customers** across **14 columns**, with no missing values. The target variable is `Personal_Loan`, and it is heavily imbalanced with an acceptance rate of roughly **9.6 percent** (about a 9 to 1 class ratio).

| Column | Description |
| --- | --- |
| `ID` | Customer ID |
| `Age` | Customer age in completed years |
| `Experience` | Years of professional experience |
| `Income` | Annual income in thousands of dollars |
| `ZIPCode` | Home address ZIP code |
| `Family` | Family size of the customer |
| `CCAvg` | Average monthly credit card spending in thousands of dollars |
| `Education` | Education level (1: Undergrad, 2: Graduate, 3: Advanced or Professional) |
| `Mortgage` | Value of house mortgage if any, in thousands of dollars |
| `Personal_Loan` | Did the customer accept the personal loan in the last campaign? (0: No, 1: Yes) |
| `Securities_Account` | Does the customer hold a securities account? (0: No, 1: Yes) |
| `CD_Account` | Does the customer hold a certificate of deposit account? (0: No, 1: Yes) |
| `Online` | Does the customer use internet banking? (0: No, 1: Yes) |
| `CreditCard` | Does the customer use a credit card from another bank? (0: No, 1: Yes) |

## Approach

1. **Data understanding.** Reviewed the shape, data types, and missing values, and confirmed a clean dataset with no imputation required.
2. **Exploratory data analysis.** Studied univariate distributions and bivariate relationships between each feature and loan acceptance, including a correlation analysis that revealed Age and Experience are almost perfectly correlated.
3. **Data preparation.** Dropped the redundant Experience feature, handled skewed variables such as Income, CCAvg, and Mortgage, and encoded categorical fields for modelling.
4. **Modelling.** Trained Decision Tree classifiers and compared four strategies: a default unpruned tree, a pre pruned tree, and two post pruned trees optimized through cost complexity pruning.
5. **Evaluation.** Compared models on accuracy, precision, recall, and F1 score, with emphasis on recall and F1 because of the class imbalance.
6. **Recommendations.** Translated feature importance and segment behaviour into targeting and cross sell actions for the marketing team.

## Key Findings

- **Income is the strongest predictor** of loan acceptance across all models, with relative importance between 0.37 and 0.44. Acceptors are concentrated in the 100 to 200 income range, while non acceptors cluster below 90, and acceptance rises sharply above roughly 107k.
- **CD account holders accept loans at about 47 percent**, which is nearly six to seven times the rate of non holders, making it the strongest binary signal found in EDA.
- **Education levels 2 and 3** customers are more than twice as likely to accept a loan as level 1 customers, and they rank as the second most important feature group.
- **Higher credit card spenders** (CCAvg above 2.5 to 3) accept more often, with acceptors showing a median CCAvg near 3.8 versus about 1.5 for non acceptors.
- **Family size 3** shows the highest acceptance rate at about 13 percent, while single customers show the lowest at about 7 percent.
- **Age, ZIP code, online banking, and outside credit card ownership** show little to no relationship with acceptance.
- The **post pruned Decision Tree** delivered the best balance on the test set with an F1 score of **88.05 percent** and recall of **85.37 percent**, while precision stayed high across all models between 90 and 94 percent.

## Recommendations

- Focus campaigns on customers earning above 107k, since income is the single most decisive factor in acceptance.
- Prioritize customers with education levels 2 and 3, who are far more likely to convert.
- Use CCAvg above 2.5 to 3 as a secondary targeting filter.
- Treat family size 3 customers as a priority segment.
- Run a dedicated loan offer campaign for CD account holders, the highest value cross sell group.
- Treat the large base of customers without an outside credit card as a separate cross sell opportunity for card products.
- Deploy the post pruned tree for production scoring and keep the simpler pre pruned tree as an interpretable model for explaining decisions to stakeholders and regulators.
- Report recall and F1 score rather than accuracy, given the 9 to 1 class imbalance.

## Repository Structure

```
loan-acceptance-prediction/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   └── Personal_Loan_Modelling.csv     # not committed (see .gitignore)
├── notebooks/
│   └── loan_acceptance_prediction.ipynb
└── reports/
    └── loan_acceptance_prediction.html  # exported notebook
```

## Getting Started

```bash
# clone
git clone https://github.com/<your-username>/loan-acceptance-prediction.git
cd loan-acceptance-prediction

# (optional) create a virtual environment
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

# install dependencies
pip install -r requirements.txt

# launch the notebook
jupyter notebook notebooks/loan_acceptance_prediction.ipynb
```

## Tech Stack

Python, pandas, NumPy, scikit-learn, Matplotlib, seaborn, Jupyter
