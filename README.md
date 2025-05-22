# 🏦 Bank Customer Churn Prediction

This project aims to predict whether a bank customer will leave the bank or not based on their demographic and behavioral data.

## 🎯 Objective
To build a machine learning model using supervised learning techniques that can predict customer churn. The ultimate goal is to help banks take preventive action to reduce customer loss.

---

## 📦 Dataset

- **Source:** [Kaggle – Churn Modelling Dataset](https://www.kaggle.com/datasets/shubhendra7/customer-churn-prediction)
- **Total Samples:** 10,000+
- **Features:**
  - Credit Score, Geography, Gender, Age, Tenure, Balance, Products Used, Has Credit Card, Is Active Member, Estimated Salary
- **Target:**
  - `Exited` (1 = churned, 0 = retained)

---

## 🔍 Exploratory Data Analysis (EDA)

- Distribution of churned vs. retained customers (pie chart, bar plot)
- Relationship between churn and:
  - Geography
  - Gender
  - Credit card usage
  - Active membership
- Correlation heatmap between numerical features

---

## 🛠️ Data Preprocessing

- Dropped irrelevant columns: `RowNumber`, `CustomerId`, `Surname`
- Converted categorical variables using `pd.get_dummies()`
- Scaled numeric features using `StandardScaler`
- Split dataset into training and test sets (80/20)

---

## 🤖 Models Used

Three supervised learning algorithms were trained and compared:

- Logistic Regression
- Random Forest Classifier
- XGBoost Classifier ✅

---

## 📈 Model Performance Comparison

| **Model**             | **Accuracy** | **Recall (Churn)** | **Precision (Churn)** | **F1 Score (Churn)** |
|-----------------------|--------------|---------------------|------------------------|------------------------|
| Logistic Regression   | 0.808        | 0.19                | 0.59                   | 0.28                   |
| Random Forest         | 0.860        | 0.46                | 0.78                   | 0.58                   |
| **XGBoost (Final)**   | 0.850        | **0.49**            | **0.70**               | **0.58**               |

---

## 📊 Bonus Insights

### 💡 Feature Importance (XGBoost)

Top influential features:
- Age
- IsActiveMember
- Geography_Germany

### 📐 ROC Curve

XGBoost’s AUC score demonstrates its ability to differentiate churned customers from retained ones.

---

## ✅ Conclusion

XGBoost was selected as the final model due to its balance between precision and recall, and its ability to better identify customers at risk of churn.

This model can help banks retain valuable customers by triggering early interventions based on churn risk predictions.

---

## 🔗 Kaggle Notebook

👉 [Click here to view the full Kaggle notebook](YOUR_KAGGLE_NOTEBOOK_LINK_HERE)

---


