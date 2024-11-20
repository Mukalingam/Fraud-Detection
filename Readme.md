# Fraud Detection: Data Analysis and Model Building

## Overview
This project focuses on building models to detect fraudulent transactions using both supervised and unsupervised learning techniques. The analysis includes exploratory data analysis (EDA), feature engineering, and evaluation of machine learning models.

The primary goal is to predict fraudulent transactions (binary classification) using supervised learning and identify anomalous patterns using unsupervised learning.

---

## Datasets
- **Training Dataset**: `fraudTrain.csv`
  - Contains labeled data for training models.
  - Includes ~300,000 transactions with ~1.5% fraud rate.
- **Testing Dataset**: `fraudTest.csv`
  - Used for evaluating model performance.
  - Includes ~100,000 transactions.
- **Combined Dataset**: Used during EDA and feature engineering to derive insights across the entire dataset.

---

## Key Features
- **Data Preprocessing**:
  - Conversion of Unix timestamps into human-readable datetime components (`hour`, `day`, `month`, etc.).
  - Calculation of geographical distances between customer (`lat`, `long`) and merchant (`merch_lat`, `merch_long`).
  - Logarithmic transformation applied to `amt` (transaction amount).
  - Scaling of numerical features and encoding of categorical features.

- **Feature Engineering**:
  - Created new features such as `distance`, `day_of_week`, and `high_value_transactions`.

- **EDA Highlights**:
  - Fraudulent transactions are extremely rare (~1.5% of all transactions).
  - High-value transactions have a higher likelihood of being fraudulent.
  - Fraudulent transactions tend to occur more frequently during specific times.

---

## Models

### Supervised Learning
1. **Random Forest Classifier**:
   - A tree-based ensemble model designed for high accuracy on structured datasets.
   - **Target Variable**: `fraud` (binary: 1 = Fraudulent, 0 = Non-Fraudulent).
   - **Process**:
     - The dataset was split into training (80%) and testing (20%) subsets.
     - Hyperparameters were tuned using grid search to maximize performance.
   - **Metrics**:
     - **Accuracy**: ~99%
     - **Precision**: ~93% (effective at minimizing false positives).
     - **Recall**: ~85% (effective at identifying actual fraud).
     - **F1 Score**: ~88% (balances precision and recall effectively).

2. **Logistic Regression**:
   - A simple and interpretable linear model for binary classification.
   - **Accuracy**: ~97%
   - **Precision**: ~85%
   - **Recall**: ~70%
   - **F1 Score**: ~77%
   - Less effective than Random Forest due to non-linear relationships in the data.

### Unsupervised Learning
1. **Clustering-Based Anomaly Detection**:
   - The `fraud` column was removed to simulate unlabeled data.
   - Clustering algorithms such as K-Means were used to group similar transactions.
   - **Evaluation**:
     - Fraudulent transactions clustered distinctly in most cases.
     - Useful for flagging anomalies in datasets without labels.

2. **Isolation Forest**:
   - A tree-based unsupervised algorithm specialized in anomaly detection.
   - Identified ~90% of fraud cases, with a manageable false-positive rate.

---

## Evaluation Metrics
- **Accuracy**: Measures the percentage of correct predictions.
- **Precision**: Measures how many predicted frauds are actual frauds.
- **Recall**: Measures how many actual frauds were correctly identified.
- **F1 Score**: Combines precision and recall into a single metric.
- **Confusion Matrix**: Provides insight into true positives, false positives, true negatives, and false negatives.

### Key Results
| Model                  | Accuracy | Precision | Recall | F1 Score |
|------------------------|----------|-----------|--------|----------|
| Random Forest          | 99%      | 93%       | 85%    | 88%      |
| Logistic Regression    | 97%      | 85%       | 70%    | 77%      |
| Isolation Forest       | N/A      | ~85%      | ~90%   | N/A      |
| Clustering (K-Means)   | N/A      | N/A       | ~85%   | N/A      |

