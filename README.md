# Term Deposit Subscription Prediction (Bank Marketing)

## **Problem Statement**

Banks spend heavily on marketing campaigns to promote term deposits, but not every customer subscribes. Targeting the wrong customers wastes resources and lowers campaign efficiency.


This project aims to **predict which customers are most likely to subscribe**, enabling smarter marketing and cost savings.


## **Objective**

* Predict customer subscription to term deposits (`yes` / `no`).
* Build and compare multiple classification models.
* Evaluate model performance with F1-score, ROC-AUC, and other metrics.
* Explain predictions using **Explainable AI (SHAP/LIME)**.
* Provide actionable insights for marketing strategy.


## **Dataset Description**

* **Source:** UCI Machine Learning Repository
* **Type:** Structured tabular data
* **Rows:** 45,211 | **Columns:** 17
* **Target Variable:** `y` (term deposit subscription)
* **Features:**

  * **Demographic:** age, job, marital status, education
  * **Financial:** balance, housing loan, personal loan
  * **Campaign-related:** contact, day, month, duration, campaign, previous contacts, previous outcome (`poutcome`)

**Key Observations:**

* Most customers did **not subscribe** (12% subscription rate).
* Customers are mainly **blue-collar, married, with secondary education**.
* Majority contacted via **cellular** few via telephone.
* Seasonal trends: most activity in **May to August**, least in winter/early spring.


## **Data Cleaning & Preprocessing**

* No missing values ready for analysis.
* Categorical features encoded using **Label Encoding**.
* Numerical features transformed using **Yeo–Johnson Power Transformation**.
* Outliers in balance clipped using **IQR method**.
* Train-test split: 80% train, 20% test stratified by target.


## **Exploratory Data Analysis (EDA)**

**Numerical Features:**

* **Age:** mostly 30–45, slight right skew.
* **Balance:** highly right-skewed, few extreme outliers.
* **Call Duration:** short calls dominate, few very long.
* **Campaign Frequency:** most customers contacted 1–3 times.

**Categorical Features:**

* **Job:** mostly blue-collar, management, technician, admin, services.
* **Marital Status:** mostly married.
* **Education:** majority secondary, some tertiary, fewer primary.
* **Contact:** majority via cellular.
* **Previous Outcome (`poutcome`):** mostly unknown/other, failures more than successes.

**Target Distribution:**

* Imbalanced: 88% `no`, 12% `yes`.

## **Model Building & Evaluation**

**Models Trained:**

* Logistic Regression
* Random Forest
* Gradient Boosting
* XGBoost

**Evaluation Metrics:**

| Model               | F1-Score | Precision | Recall | ROC-AUC |
| ------------------- | -------- | --------- | ------ | ------- |
| XGBoost             | 0.60     | 0.50      | 0.74   | 0.92    |
| Gradient Boosting   | 0.55     | 0.67      | 0.46   | 0.93    |
| Logistic Regression | 0.49     | 0.35      | 0.81   | 0.88    |
| Random Forest       | 0.46     | 0.68      | 0.34   | 0.93    |

**Best Model:** **XGBoost** – balances precision and recall while handling imbalanced data.


## **Model Explainability (SHAP)**

**Top Drivers of Subscription:**

* **Positive Influences:** `poutcome` (previous success), call `duration`, `day`, `month`, `age`, previous contacts (`pdays`).
* **Negative Influences:** `balance`, occasionally `housing`.

**Insights from Individual Predictions:**

* Positive past outcomes and longer calls increase subscription probability.
* Seasonal and day-of-month effects slightly influence likelihood.

**Decision Plot Summary:**

* `poutcome` is the strongest driver.
* Followed by duration, day, month, age, pdays, balance.
* Housing slightly reduces scores in some cases.



## **Business & Marketing Insights**

1. **Prioritize past positive responders (`poutcome`)** – most likely to subscribe again.
2. **Focus on longer calls** – meaningful conversations increase subscription chances.
3. **Target mid-month & May–August campaigns** – seasonal peaks perform better.
4. **Profile customers carefully** – age and past campaign interactions influence likelihood.
5. **Reduce wasted effort** – avoid customers with low balance or poor past outcomes.
   


**Overall:** XGBoost with SHAP provides a transparent actionable model to **optimize marketing campaigns improve targeting, and reduce costs**.

