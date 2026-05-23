# Fraud-Analysis-Project

An end-to-end machine learning pipeline and risk-scoring engine designed to identify fraudulent activity in highly imbalanced mobile money transaction data. By combining behavioral heuristics with an optimized XGBoost classifier, this system isolates high-risk `TRANSFER` and `CASH_OUT` events while minimizing customer friction.

Dataset: https://www.kaggle.com/datasets/ealaxi/paysim1?utm_source=chatgpt.com

## 🚀 Key Insights & Features

PPT: https://docs.google.com/presentation/d/1xvcd5CjYg5KPbT8iPwecOk0PktNeQsR6TbOSu1DGTTQ/edit?pli=1&slide=id.p3#slide=id.p3

* **Behavioral Risk Engine:** Implements a composite scoring algorithm tracking account-draining patterns (where sender balances are completely depleted).
* **Imbalanced Data Optimization:** Tuned specifically for low-prevalence target classes (0.129% baseline fraud rate) using PR-AUC rather than standard accuracy metrics.
* **Production-Ready Benchmarking:** Evaluates Logistic Regression, Random Forests, and XGBoost to find the optimal threshold balancing fraud capture (Recall) and false alarms (Precision).

---

## 📊 Model Performance Summary

| Model | Precision | Recall | F1 Score | PR-AUC |
| :--- | :---: | :---: | :---: | :---: |
| Logistic Regression | 0.029 | 0.922 | 0.057 | 0.571 |
| Random Forest | 0.081 | 0.990 | 0.149 | 0.900 |
| **XGBoost (Selected)** | **0.634** | **0.959** | **0.764** | **0.959** |

## 📐 Risk Scoring Logic:
The behavioral engine pre-filters transactions using a deterministic heuristic algorithm before sending high-risk payloads to the ML pipeline:
Risk\_Score = (LargeAmt\_Flag \times 30) + (HighRiskType\_Flag \times 40) + (AccountDrained\_Flag \times 30) 
High Risk (>70): Trigger immediate multi-factor authentication (2FA) or route to the manual review queue.
Low Risk (<30): White-listed for instant automated processing.

Notebook 1: EDA + Fraud Insights
Notebook 2: ML Modeling
