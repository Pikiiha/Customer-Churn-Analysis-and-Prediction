# Customer-Churn-Analysis-and-Prediction
# 📉 Customer Churn Prediction

## 📌 Project Overview

Customer churn is a critical concern for subscription-based businesses like telecom providers. Retaining existing customers is far more cost-effective than acquiring new ones. This project focuses on identifying customers likely to churn using machine learning techniques and providing actionable insights for reducing churn rates.

---

## 🎯 Objectives

- Explore the customer data to identify trends and patterns related to churn.
- Preprocess and prepare the data for modeling.
- Train multiple classification models and compare their performance.
- Identify the best-performing model for churn prediction.
- Provide business recommendations based on model insights.

---

## 🗃️ Dataset Description

- **Source:** [Kaggle Telco Customer Churn Dataset](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
- **Records:** 7043 customers
- **Target Variable:** `Churn` (Yes / No)
- **Key Features:**
  - `tenure`, `MonthlyCharges`, `TotalCharges`
  - `Contract`, `InternetService`, `PaymentMethod`
  - `SeniorCitizen`, `Partner`, `Dependents`, etc.

---

## 📊 Exploratory Data Analysis (EDA)

### 🔹 Churn Distribution

![Churn Distribution](path/to/churn_distribution.png)
![tenure plot distribution](https://github.com/user-attachments/assets/2a8161db-2fc8-4217-be31-4383f3ea9fbc)


> Most customers do not churn, highlighting a class imbalance issue.

### 🔹 Tenure and Senior Citizen Analysis

![Tenure Distribution](path/to/tenure_plot.png)

> Customers with higher tenure are less likely to churn.  
> Senior citizens show a slightly lower churn rate, contrary to assumptions.

*More plots included in the full notebook.*

---

## ⚙️ Data Preprocessing

- Missing values imputed or removed
- Categorical variables encoded using One-Hot Encoding
- StandardScaler used for numerical features
- Train-test split (80/20)

---

## 🤖 Model Building and Evaluation

### 🔍 Models Compared:

- Logistic Regression  
- Random Forest  
- Gradient Boosting  
- XGBoost  
- LightGBM  

### 📈 Model Evaluation Summary:

| Model               | Accuracy | F1-Score | ROC-AUC |
|--------------------|----------|----------|---------|
| Logistic Regression| 0.7672   | 0.3051   | 0.8210  |
| Random Forest      | 0.7999   | 0.5552   | 0.8330  |
| Gradient Boosting  | 0.8013   | 0.5846   | 0.8466  |
| XGBoost            | 0.7857   | 0.5648   | 0.8212  |
| LightGBM           | 0.7885   | 0.5718   | 0.8359  |

### 📉 Confusion Matrix and Curves (Gradient Boosting):

![Confusion Matrix](path/to/confusion_matrix.png)  
![ROC Curve](path/to/roc_curve.png)  
![Precision-Recall Curve](path/to/precision_recall_curve.png)
![Gbm and roc and precision image](https://github.com/user-attachments/assets/7f95319c-63a2-4d65-b1f8-5196d0c0389c)


---

## 🧠 Key Findings

1. **Gradient Boosting performed the best**, with the highest accuracy (80.13%), F1-score (0.5846), and ROC-AUC (0.8466).
2. **F1-score is the most reliable metric** in this imbalanced setting. Logistic Regression performed poorly despite decent accuracy.
3. **Tenure, contract type, and monthly charges** are key drivers of churn.
4. **Random Forest, XGBoost, and LightGBM** are strong backups if training time or interpretability is a concern.

---

## 📌 Recommendations

- Deploy Gradient Boosting for churn prediction.
- Consider using SHAP for explainability in business dashboards.
- Experiment with SMOTE or class weighting to further improve recall.
- Target customers with low tenure and month-to-month contracts for retention strategies.

---

## 🚀 Feature Importance
Feature_importance.png
![Uploading Feature importance image.png…]()


🔝 Top Contributing Features
Feature	Importance	Interpretation
TotalCharges_20.2	0.483	🔥 Most important feature (48.3%). This likely represents a binned or encoded version of total charges, indicating that customers in this range have a high impact on churn prediction.
TotalCharges_45.3	0.124	Also a binned TotalCharges value. Suggests multiple thresholds in total charges are informative for predicting churn.
tenure	0.116	Customers’ time with the company significantly influences churn—shorter tenure often means higher churn.
InternetService_Fiber optic	0.059	Customers using fiber optic internet might be more likely to churn (often associated with dissatisfaction or pricing issues).
Contract_Two year	0.051	Longer contracts reduce churn likelihood—this feature strongly helps the model distinguish stable customers.
PaymentMethod_Electronic check	0.050	Often associated with higher churn—possibly due to lower commitment or ease of leaving.

📉 Moderate to Low Importance Features
Feature	Importance	Interpretation
Contract_One year	0.039	Still contributes, but less than two-year contracts. Reflects moderate stability.
PaperlessBilling_Yes	0.015	Slight impact—could be a behavioral indicator.
OnlineSecurity_Yes	0.0075	Security services slightly reduce churn risk.
TechSupport_Yes	0.0041	Also suggests support reduces churn, but effect is small.
MonthlyCharges	0.0041	Surprisingly low—possibly due to overlap with TotalCharges.
Dependents_Yes	0.0028	Minor—possibly correlates with contract length or stability.
StreamingMovies_Yes	0.0026	Very low impact on churn decisions.
OnlineSecurity_No internet service	0.0025	Suggests non-internet users are a small group and not heavily predictive.
TotalCharges_19.65	0.0024	Another total charge bin, but less influential.

🔍 Overall Insights
TotalCharges dominates:

The binned TotalCharges_20.2 alone contributes almost 48% to predictions.

This suggests a non-linear relationship between total charges and churn (certain ranges are more telling than others).

Contract and Tenure are crucial:

Customers with longer tenure or locked into longer contracts churn less—this aligns with expected business behavior.

Service-specific variables (like Internet type or Payment method) contribute meaningfully but are secondary.

Monthly charges have surprisingly low importance, likely because TotalCharges already encodes price + duration.

✅ Recommendations
Investigate bins like TotalCharges_20.2 and 45.3: What do these mean in business terms? Who are these customers?

Target retention strategies on high-churn segments:

Customers with short tenure.

Fiber optic internet users.

Customers using electronic check.

We can consider combining low-importance features or removing them to simplify the model, though ensemble models can handle this redundancy well

---- 

BUSINESS INSIGHTS & RECOMMENDATIONS



📊 Overall Churn Analysis:
   No: 73.46%
   Yes: 26.54%

🎯 High-Risk Segments:
     customerID:   ‘0004-TLHLJ’ ( 100.0% churn rate)
     gender:   ‘Female’ ( 26.9% churn rate)
     Partner:   ‘No’ ( 33.0% churn rate)

💡 KEY RECOMMENDATIONS:
   1. 🎯 Target Retention: Focus on high-risk segments identified above
   2. 📞 Proactive Outreach: Implement early warning system for at-risk customers
   3. 🎁 Incentive Programs: Design retention offers for high-value churning customers
   4. 📈 Feature Enhancement: Improve services related to top importance features
   5. 📊 Monitor KPIs: Track churn metrics weekly and adjust strategies accordingly

🔑 Focus Areas Based on Model:
   1. TotalCharges_20.2: High impact on churn prediction
   2. TotalCharges_45.3: High impact on churn prediction
   3. tenure: High impact on churn prediction

    💡 NEXT STEPS:
   1. Implement recommended retention strategies
   2. Set up automated churn prediction pipeline
   3. Monitor model performance over time
   4. Collect feedback and retrain models regularly
   5. A/B test retention strategies
  



  












## 📁 Repository Structure

---


---

## 🛠️ How to Run

1. Clone the repository  
2. Open the notebook `Churn_Prediction.ipynb`  
3. Run all cells to reproduce the analysis

```bash
git clone https://github.com/Pikiiha/Customer churn Analysis and prediction.git
cd churn-prediction
jupyter notebook


