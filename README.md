# Bank Marketing Dataset – Classification Analysis

## 🎯 Objective
This project was conducted as part of the technical assessment for the **Business Analytics - Business Strategy & Intelligence** position at **Bank Islam Malaysia Berhad**. The goal is to demonstrate proficiency in **Python, Machine Learning, and Data Analytics** through hands-on processing, modelling, and analysis using the Bank Marketing dataset from Kaggle.

## 📦 Dataset Overview
- **Source**: [Bank Marketing Dataset (Kaggle)]
- **Shape**: (11162, 17)
- **Target Variable**: `deposit` (Binary: True = Yes, False = No)
- **No missing values** were detected during preprocessing.

---

## 🔍 Exploratory Data Analysis (EDA)

### 1. **Class Balance**
- `deposit = True`: 5289
- `deposit = False`: 5873  
✅ The dataset is balanced — no need for resampling.

### 2. **Demographic Insights**
- **Job**: Most depositors are from *management* and *blue-collar* jobs.
- **Education**: *Secondary education* dominates among depositors.
- **Duration**: Longer call duration has a strong positive correlation with deposit (target variable).

---

## 🧪 Data Preprocessing

### 1. **Feature Segmentation**
- Separated features into:
  - **Numerical**: `age`, `balance`, `day`, `duration`, `campaign`, etc.
  - **Categorical**: `job`, `marital`, `education`, `contact`, `poutcome`, etc.

### 2. **Anomaly & Outlier Detection**
- Outliers detected in `balance` via boxplot, but retained due to business logic (income variation).

### 3. **Normalization**
- **StandardScaler** used on numerical features for variance stabilization and model compatibility.

### 4. **Feature Engineering**
- **Removed**: `pdays` (redundant with `previous`)
- **Created Cluster**:
  - `previous_cluster`: 
    - `0` = never contacted
    - `1` = contacted before

### 5. **Encoding**
- **One-Hot Encoding**: For categorical features with no hierarchy (e.g. `job`, `marital`, `contact`)
- **Label Encoding**: For ordinal features (e.g. `education`)

> Total number of features after encoding: **41**

---

## 🧠 Multicollinearity Analysis

Used **Variance Inflation Factor (VIF)** to detect multicollinearity:

| Feature               | VIF        |
|-----------------------|------------|
| previous_cluster_0    | inf        |
| previous_cluster_1    | inf        |
| poutcome_unknown      | 1062.52    |

- Dropped `previous_cluster_0` (redundant)
- Dropped `poutcome_unknown` (extremely high VIF)

---

## 💡 Feature Importance (Random Forest)

| Feature   | Importance |
|-----------|------------|
| duration  | 0.3502     |
| balance   | 0.0854     |
| age       | 0.0825     |
| day       | 0.0745     |
| campaign  | 0.0370     |

---

## 🧪 Model Building

### Algorithms Used:
- **Logistic Regression**
- **Random Forest Classifier**  
*(No hyperparameter tuning due to time constraints)*

### Performance Metrics:

#### Logistic Regression

| Metric        | Value |
|---------------|-------|
| Accuracy      | 81%   |
| Precision (1) | 81%   |
| Recall (1)    | 78%   |
| F1-score (1)  | 80%   |

#### Random Forest

| Metric        | Value |
|---------------|-------|
| Accuracy      | 84%   |
| Precision (1) | 81%   |
| Recall (1)    | 85%   |
| F1-score (1)  | 83%   |

### Confusion Matrix (Random Forest)

|               | Pred: No | Pred: Yes |
|---------------|----------|-----------|
| **Actual: No**|   958    |   208     |
| **Actual: Yes**|  162    |   905     |

> ✅ **Random Forest performed best** with 84% accuracy. Model is not overfitting and provides balanced prediction.

---

## ⏳ Limitations

Due to limited time (~1 day with work constraints and travel), some advanced tasks were not performed:
- No hyperparameter tuning (e.g. GridSearchCV)
- No anomaly removal or feature selection refinement
- Task 1 (DuckDB Normalization) and Task 2 (Streamlit Dashboard) were not attempted

---

## 📁 Files & Deliverables

| File                      | Description                                   |
|---------------------------|-----------------------------------------------|
| `notebook.ipynb`           | Full analysis in Jupyter notebook             |
| `README.md`                | Documentation (this file)                     |
| `Slide`                    | Report                                        |

---

## 💬 Conclusion

Despite time constraints, the model shows promising performance in predicting deposit conversion. Proper feature engineering, normalization, and encoding significantly improved the model's ability to generalize. With further enhancements such as hyperparameter tuning, anomaly detection, and explainable AI tools, the performance could be further improved.

---

## 🔎 Highlight of Findings and Assumptions:

### Customer Demographics and Deposit Subscription:
- **Job**: The majority of deposit subscribers come from *management* and *blue-collar* job types. This suggests that these groups may be more financially stable and have a higher propensity to engage with bank deposit products.
- **Education**: A significant proportion of deposit subscribers have *secondary education*, which could indicate that customers with this level of education may be more inclined to save or invest in bank deposit products.

### Influence of Call Duration:
- Longer call durations have a **strong positive correlation** with deposit subscriptions. This indicates that more extensive customer engagement or consultations during calls are effective in persuading customers to subscribe to deposit products.

### Feature Importance and Predictive Accuracy:
- The key features influencing deposit subscription include **duration**, **balance**, and **age**. Longer call interactions, higher balance, and customer age are the most important predictors.
- **Random Forest** achieved an accuracy of **84%**, making it the best performing model in this analysis, and showcasing its ability to predict deposit subscriptions based on these features.

### Feature Redundancy and Preprocessing:
- **Redundancy**: Features like `pdays` and `previous` were found to be redundant. These were simplified or clustered to improve the model's efficiency.
- **Preprocessing**: Feature scaling and encoding techniques, such as **StandardScaler** and **One-Hot Encoding**, helped improve the model's predictive performance.

### Time-Based Features:
- Features like **day**, **month**, and **duration** played a crucial role in predicting the likelihood of deposit subscriptions, highlighting the importance of timing in customer behavior.

### Assumption:
- The correlation between **long call durations** and **deposit subscriptions** assumes that more meaningful customer engagement during longer calls increases the likelihood of customers subscribing to deposit products.

---

