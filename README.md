# Customer Churn Prediction

**Intern ID:** CITS8439 | **Author:** Nithyashree S

End-to-end churn analysis and prediction on a telecom customer dataset: Excel cleaning, Python EDA, and machine learning models.

## Goal
Find out which customers are likely to leave and why, so the company can act early.

## Dataset
- Telco Customer Churn (Kaggle): 7,043 customers × 21 columns
- Target: Churn (Yes/No). 26.5% of customers churned (1,869 Yes, 5,174 No)

## Tools
Excel (cleaning) → Python: pandas, matplotlib, seaborn, scikit-learn (EDA and modelling)

## Data cleaning (Excel)
- 7,043 rows × 21 columns, 0 empty cells, 0 duplicate customerIDs
- 11 TotalCharges values contained a space (all customers with tenure 0); set to 0 and converted to numeric
- Ranges checked: tenure 0 to 72, MonthlyCharges 18.25 to 118.8, TotalCharges 0 to 8,685, no negatives

## Analysis steps (Python)
1. Load and validate the data
2. Overall churn rate
3. Churn by contract type
4. Tenure and monthly charges
5. Other segments (internet service, payment method, tech support, paperless billing, senior citizens)
6. Data preparation: one-hot encoding, 80/20 stratified split, scaling fitted on training data only
7. Model comparison: Logistic Regression and Random Forest (both with balanced class weights)
8. Confusion matrices
9. Feature importance
10. Business recommendations

## Key EDA findings
- Month-to-month contracts churn at about 43%, versus about 11% (one year) and 2.8% (two year).
- Customers who left had an average tenure of 18.0 months (37.6 for those who stayed) and higher monthly charges (74.4 vs 61.3).
- Higher churn for fiber optic (about 42%), electronic check (about 45%), no tech support (about 42%), paperless billing (about 33%) and senior citizens (41.7%).

![Churn rate by contract type](Customer%20churn%20prediction%20project/churn_by_contract.png)

![Churn rate by customer segments](Customer%20churn%20prediction%20project/churn_by_segments.png)

## Model results (test set: 1,409 customers, 374 churners)

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---|---|---|---|---|
| Logistic Regression | 0.738 | 0.504 | 0.783 | 0.614 | 0.842 |
| Random Forest | 0.776 | 0.569 | 0.642 | 0.603 | 0.827 |

![Confusion matrices](Customer%20churn%20prediction%20project/confusion_matrix.png)

**Final model: Logistic Regression.** It catches 293 of 374 churners (78%), against 240 (64%) for Random Forest. Missing a churner usually costs more than an unneeded retention offer, and the model is easier to explain. Accuracy alone is misleading here, since predicting "stays" for everyone would score about 73.5%.

## Top drivers
- Toward staying: two-year contract, longer tenure, one-year contract, tech support and online security
- Toward leaving: fiber optic internet, electronic check, streaming services, paperless billing

![Logistic Regression feature importance](Customer%20churn%20prediction%20project/feature_importance.png)

## Recommendations
1. Offer incentives to move new month-to-month customers onto longer contracts.
2. Use the model to rank customers by churn risk and target retention offers at the highest-risk ones.
3. Review fiber optic pricing, reliability and support.
4. Encourage automatic payment methods.
5. Promote tech support and online security add-ons (test first, since this is an association).

## Limitations
- One snapshot of customers; no information on why each customer left.
- The models show associations, not causes. Tenure, MonthlyCharges and TotalCharges overlap, so individual coefficients should not be over-read.
- Precision is about 0.50, so about half of the flagged customers would not actually have left.
- Results come from a single 80/20 split; cross-validation would give a steadier estimate.

## Files
All files are in the `Customer churn prediction project` folder:
- `Customer_churn_prediction_project.ipynb`: full analysis notebook
- `Telco-Customer-Churn - cleaned_dataset.csv`: cleaned dataset
- `churn_by_contract.png`, `churn_by_segments.png`, `confusion_matrix.png`, `feature_importance.png`: charts used in this README

## How to run
Download the notebook and the cleaned CSV into the same folder, check the file name in the loading cell, and run all cells.
