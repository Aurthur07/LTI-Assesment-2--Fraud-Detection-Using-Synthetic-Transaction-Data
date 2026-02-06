# Fraud Detection Using Synthetic Transaction Data  
### LTI Assessment 2

An end-to-end fraud detection project using **synthetic financial transaction data**.
The project covers exploratory data analysis, fraud pattern discovery, feature engineering,
machine learning modeling, evaluation, and explainability.

---

## 📍 Problem Statement

Financial fraud is a critical challenge in digital payment systems. Fraudulent transactions
are rare, highly imbalanced, and often follow **non-random behavioral patterns**.

The objective of this project is to:
- Understand transaction behavior
- Identify fraud patterns
- Engineer meaningful features
- Build and evaluate a machine learning model to detect fraudulent transactions

---

## 📊 Dataset Description

### Dataset Used
- **Name:** Synthetic Financial Datasets 
- **Source:** Kaggle  
- **Link:** 

### Why This Dataset?
- Fully **synthetic**, avoiding privacy issues
- Simulates **real mobile money transactions**
- Fraud injected using **behavioral rules**, making it ideal for analysis

### Key Columns
| Column | Description |
|------|------------|
| step | Time step of transaction |
| type | Transaction type |
| amount | Transaction amount |
| oldbalanceOrg / newbalanceOrig | Sender balance before / after |
| oldbalanceDest / newbalanceDest | Receiver balance before / after |
| isFraud | Target variable |
| isFlaggedFraud | Rule-based fraud flag |

---

## 🔍 Exploratory Data Analysis (EDA)

EDA was performed to understand transaction behavior, class imbalance, and fraud characteristics.

### Fraud vs Non-Fraud Distribution
Fraudulent transactions form a **very small fraction** of the dataset, highlighting
the severe class imbalance typical of real-world fraud problems.

### Fraud vs Non-Fraud Distribution
![Fraud vs Non Fraud Distribution](results/Fraud%20vs%20Non%20Fraud%20Distribution.png)


---

### Fraud Rate by Transaction Type
Fraud is **not uniformly distributed** across transaction types.

### Fraud Rate by Transaction Type
![Fraud Rate by Transaction Type](results/Fraud%20Rate%20by%20transaction%20type.png)


**Insight:**  
Fraud is concentrated primarily in **TRANSFER** and **CASH_OUT** transactions.

---

## 🧠 Fraud Pattern Discovery

The following non-random fraud patterns were identified:

- Fraudulent transactions often:
  - Drain the sender’s account balance
  - Involve large transaction amounts
  - Occur in specific transaction types
- Rule-based detection (`isFlaggedFraud`) fails to capture most fraud cases

These findings motivate the use of **machine learning-based approaches**.

---

## 🛠 Feature Engineering

Raw transaction attributes were transformed into behavioral features:

### Engineered Features
- Balance-based features:
  - `orig_balance_diff`
  - `dest_balance_diff`
- Behavioral indicators:
  - Amount-to-balance ratio
  - Zero balance after transaction
  - Large amount flag
- One-hot encoding of transaction types

Identifiers such as account IDs were removed to prevent **data leakage**.

---

## 🤖 Model Development

### Train–Test Strategy
- **Time-aware 80–20 split**
- Prevents future data leakage
- Simulates real-world deployment

### Models Used
- Logistic Regression (baseline)
- **Random Forest (final model)**

Random Forest was selected due to:
- Strong performance on tabular data
- Ability to capture non-linear fraud patterns
- Built-in feature importance for explainability

---

## 📈 Model Evaluation

### Confusion Matrix
Shows the model’s ability to correctly identify fraudulent transactions.

### Confusion Matrix
![Confusion Matrix](results/Confusion%20Matrix.png)


---

### ROC Curve Comparison
Demonstrates strong discrimination between fraudulent and legitimate transactions.

### ROC Curve Comparison
![ROC Curve Comparison](results/ROC%20Curve%20Comparison.png)


---

## 🔎 Model Explainability

Feature importance analysis reveals that the model relies primarily on **behavioral patterns**.

### Feature Importance
![Feature Importance](results/Feature%20Importance.png)


**Interpretation:**  
Transactions are flagged due to abnormal balance changes, high relative amounts,
and transaction types historically associated with fraud.

---

## 🏗 System Design (Conceptual)

In a real-world system:
1. Transactions are scored in real time
2. Fraud probability is generated
3. A threshold determines whether to approve, flag, or block the transaction
4. Feedback is used for periodic retraining

---

## 📌 Results Summary

- Fraud is highly imbalanced but predictable
- Behavioral features significantly improve detection
- Random Forest outperforms rule-based methods
- Model provides both performance and explainability

---

## ⚠ Limitations

- Dataset is synthetic
- No hyperparameter tuning performed
- SHAP explainability skipped due to environment constraints

---

## 🚀 Future Improvements

- Hyperparameter optimization
- Cost-sensitive learning
- Advanced explainability techniques
- Real-time API deployment

---

## 📂 Project Structure

LTI-Assesment-2--Fraud-Detection-Using-Synthetic-Transaction-Data/
├── data/
│ ├── raw/
│ └── processed/
├── results/
│ └── figures/
├── fraud_detection.ipynb
├── fraud_modeling.ipynb
└── README.md
