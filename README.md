# 🛒 SmartKart Retention Intelligence

### Predictive Customer Churn Analytics & Risk Scoring

An end-to-end **Machine Learning solution for customer churn prediction** designed to help SmartKart identify customers who are likely to leave and prioritize them for proactive retention.

The project transforms a messy customer dataset into actionable business intelligence through **data cleaning, outlier treatment, feature selection, feature standardization, Logistic Regression, model evaluation, and customer risk scoring**.

---

## 📌 Project Overview

Customer churn is a major business challenge in retail. Losing customers can directly impact revenue and increase the cost of acquiring new customers.

**SmartKart Retention Intelligence** uses historical customer information to predict churn risk and generate a ranked list of customers requiring retention attention.

### 🎯 Business Objective

> **Predict which SmartKart customers are likely to churn so that the retention team can intervene before the customer leaves.**

The model uses three key customer attributes:

* **Age**
* **Monthly Spend**
* **Complaints**

`Customer_ID` is retained for identification but excluded from model training because it is an identifier rather than a predictive feature.

---

## 🚀 Key Features

* 🧹 Real-world dirty data cleaning
* 🔍 Data quality inspection
* ♻️ Duplicate record removal
* 🧩 Missing-value treatment
* 🚨 Invalid-value detection
* 📊 IQR-based outlier treatment
* 🎯 Business-focused feature selection
* ⚖️ Feature standardization
* 🤖 Logistic Regression classification
* 📈 Churn probability prediction
* 📋 Confusion Matrix
* 📊 Accuracy, Precision, Recall & F1-Score
* 🔎 Model coefficient interpretation
* 🚦 Customer churn-risk classification
* 📑 Business-ready customer risk report

The complete workflow follows a **15-step ML pipeline**, from data collection through final business output.

---

## 🧠 Machine Learning Approach

### Problem Type

**Supervised Learning → Binary Classification**

The target variable is:

| Value | Meaning  |
| ----- | -------- |
| `0`   | No Churn |
| `1`   | Churn    |

Because the target contains two possible outcomes, **Logistic Regression** was selected as the classification algorithm. It also provides churn probabilities, which are useful for ranking customers according to their risk level.

---

## 🔄 ML Pipeline

```text
Raw Customer Data
        ↓
Data Understanding
        ↓
Data Cleaning
        ↓
Outlier Detection & Treatment
        ↓
Feature Selection
        ↓
Target Definition
        ↓
Target Encoding Verification
        ↓
Train-Test Split
        ↓
Feature Standardization
        ↓
Logistic Regression
        ↓
Model Training
        ↓
Prediction
        ↓
Model Evaluation
        ↓
Model Interpretation
        ↓
Customer Risk Report
```

---

## 📊 Dataset

The original dataset contains **100 customer records and 5 columns**:

| Column          | Description                      |
| --------------- | -------------------------------- |
| `Customer_ID`   | Unique customer identifier       |
| `Age`           | Customer age                     |
| `Monthly_Spend` | Customer's monthly spending      |
| `Complaints`    | Number of customer complaints    |
| `Churn`         | Target variable indicating churn |

The dataset intentionally contains real-world-style data quality issues such as **duplicates, missing values, invalid ages, negative spending, text-formatted numbers, and extreme outliers**.

---

## 🧹 Data Cleaning

The raw dataset was intentionally messy, so several preprocessing techniques were applied.

### Cleaning operations

* Removed duplicate customer records
* Removed unnecessary whitespace
* Converted `Age` from text to numeric
* Corrected `"thirty"` to `30`
* Identified invalid ages
* Identified negative monthly spending
* Replaced invalid values with missing values
* Filled missing numerical values using the **median**

## Five duplicate rows were removed, reducing the dataset from **100 to 95 records**.

## 🚨 Outlier Treatment

The project uses the **Interquartile Range (IQR)** method to identify extreme values.

Instead of deleting affected customers, outliers are **capped (winsorized)** so that useful customer information is retained.

Examples from the dataset include:

* `Monthly_Spend = 99,999` → extreme outlier
* `Complaints = 50` → extreme outlier

These values are capped using IQR boundaries.

---

## 🎯 Feature Selection

The model uses:

```text
Age
Monthly_Spend
Complaints
```

`Customer_ID` is not used as a model feature because it does not contain meaningful behavioral information for predicting churn.

---

## ⚙️ Train-Test Strategy

The cleaned dataset is divided into:

* **80% Training Data**
* **20% Testing Data**

The split uses **stratification** to maintain a similar churn/non-churn distribution in both datasets.

## Feature scaling is performed using `StandardScaler`, with the scaler fitted only on the training data to avoid test-data leakage.

## 🤖 Model

### Logistic Regression

Logistic Regression was selected because churn is a binary classification problem.

The model learns the relationship between:

```text
Age
Monthly Spend
Complaints
        ↓
     Churn Risk
```

It produces both:

* **Predicted Churn Class**
* **Probability of Churn**

The probability output allows customers to be ranked from highest to lowest risk.

---

## 📈 Model Evaluation

The model is evaluated using standard classification metrics:

* Accuracy
* Precision
* Recall
* F1-Score
* Confusion Matrix

The notebook reports approximately **89–95% accuracy** and **100% recall** on the test set, with precision around **83–91%**, depending on the resulting run/output.

> **Business perspective:** High recall is particularly valuable for churn prevention because missing a genuinely at-risk customer can result in customer loss.

---

## 🔎 Business Insights

The Logistic Regression coefficients provide interpretable insights into customer churn.

### 1. Complaints → Higher Churn Risk

A higher number of complaints is associated with increased churn probability.

**Business implication:** Improving customer support and complaint resolution can become an important retention strategy.

### 2. Monthly Spend → Lower Churn Risk

Higher monthly spending is associated with lower churn risk in this dataset.

**Business implication:** High-spending customers should receive special attention because they represent valuable customer relationships.

### 3. Age → Relatively Smaller Effect

Age has a comparatively smaller influence on churn than the other two selected features.

These insights are derived from the model's learned coefficients and should be interpreted as patterns in this dataset, not universal causal relationships.

---

## 🚦 Customer Risk Scoring

The final output converts model predictions into business-friendly categories:

```text
Churn Probability
        ↓
Risk Classification
        ↓
Retention Priority
```

### Risk Labels

* 🔴 **Likely to Churn**
* 🟢 **Not Likely to Churn**

The generated report contains **19 test-set customers**, ranked by churn probability. The uploaded report contains **12 customers classified as “Likely to Churn” and 7 as “Not Likely to Churn.”**

The top-risk customers can be prioritized for immediate retention campaigns.

---

## 📁 Project Structure

```text
SmartKart-Retention-Intelligence/
│
├── SmartKart_Churn_Prediction_ML_Pipeline.ipynb
│
├── SmartKart_dirty_100_rows.csv
│
├── smartkart_churn_risk_report.csv
│
└── README.md
```

### Files

**`SmartKart_Churn_Prediction_ML_Pipeline.ipynb`**
Complete end-to-end machine learning pipeline.

**`SmartKart_dirty_100_rows.csv`**
Original intentionally messy customer dataset.

**`smartkart_churn_risk_report.csv`**
Business-ready churn prediction output containing customer-level risk probabilities and labels.

---

## 🛠️ Technology Stack

* **Python**
* **Pandas** — Data manipulation
* **NumPy** — Numerical operations
* **Matplotlib** — Visualization
* **Seaborn** — Confusion matrix visualization
* **Scikit-learn** — Machine Learning
* **Google Colab / Jupyter Notebook** — Development environment

---

## 💼 Business Use Case

SmartKart can use this solution to:

1. Identify customers at high risk of churn.
2. Prioritize retention campaigns.
3. Target high-risk customers with personalized offers.
4. Investigate customers with frequent complaints.
5. Protect valuable high-spending customer relationships.
6. Support data-driven customer retention decisions.

The final output is designed as an **action list for a retention/marketing team**, rather than simply presenting technical model metrics.

---

## 📌 Example Business Workflow

```text
Customer Data
      ↓
ML Churn Prediction
      ↓
Churn Probability
      ↓
Risk Ranking
      ↓
High-Risk Customer Identification
      ↓
Targeted Retention Action
      ↓
Improved Customer Retention
```

---

## ⚠️ Project Limitations

This project is a demonstration of an end-to-end ML workflow using a **100-record retail dataset**.

The model currently uses only three predictive variables:

* Age
* Monthly Spend
* Complaints

For a production-grade deployment, additional features such as purchase frequency, tenure, transaction history, customer support interactions, product categories, discounts, and engagement data could potentially improve the model.

Model performance should also be validated on a larger and more representative dataset before being used for real customer decisions.

---

## 🔮 Future Improvements

* Add more customer behavioral features
* Test Random Forest, XGBoost and other classification models
* Perform cross-validation
* Hyperparameter tuning
* Build an interactive churn dashboard
* Introduce automated model retraining
* Add customer segmentation
* Develop real-time churn scoring
* Deploy the model using Streamlit or an API
* Monitor model performance and data drift

---

## 📊 Final Deliverable

The project produces:

> **A ranked customer churn-risk report that converts machine-learning predictions into actionable retention priorities.**

This bridges the gap between **Machine Learning and Business Decision-Making**.

---

## 👩‍💻 Project Skills Demonstrated

* Data Cleaning
* Exploratory Data Understanding
* Data Preprocessing
* Outlier Detection
* Feature Selection
* Feature Scaling
* Supervised Machine Learning
* Logistic Regression
* Classification
* Model Evaluation
* Business Analytics
* Predictive Analytics
* Customer Retention Analytics
* Business Interpretation of ML Results

---

## 📜 Project Summary

**SmartKart Retention Intelligence** demonstrates how a business can transform messy customer data into actionable churn insights using an end-to-end Machine Learning pipeline.

The solution moves from:

**Raw Data → Clean Data → ML Model → Churn Probability → Risk Ranking → Retention Action**

making it a practical example of applying **AI/ML to a real-world retail business problem**.
