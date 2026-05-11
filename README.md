# 📊 APS Failure Prediction with Tree-Based Models

## 📌 Overview

This project focuses on solving a **binary classification problem on an
imbalanced dataset**, using the APS Failure dataset.

The study explores: - Tree-based machine learning models
- The impact of **class imbalance**
- Techniques for improving minority class detection

This project emphasizes **practical implementation and performance
analysis**, rather than theoretical derivation.

------------------------------------------------------------------------

## 📖 Problem Description

The goal is to predict whether a system will fail based on sensor
measurements.

### 🔹 Key Challenges

-   Highly **imbalanced dataset**
-   Large number of missing values
-   Difficulty detecting rare failure events

------------------------------------------------------------------------

## 🧠 Methodology

### 🔹 Data Preprocessing

-   Missing value imputation (Median)
-   Missing indicator variables
-   Feature variability analysis (Coefficient of Variation)
-   Correlation analysis
-   Data visualization

#### 📌 Purpose

-   Improve data quality
-   Understand feature behavior

------------------------------------------------------------------------

### 🔹 Model 1: Random Forest (Baseline)

-   Trained on original dataset
-   Ensemble of decision trees

#### 📊 Evaluation

-   Training error
-   Test error
-   OOB (Out-of-Bag) error : 0.00608
    The OOB error is very close to the test error, which indicates that the model has good generalization ability.Although the training error is zero, this does not necessarily imply severe overfitting. Random forests are capable of fitting the training data very well due to their ensemble of deep decision trees.In addition, the class imbalance may make the classification task easier, as the majority class dominates the dataset. However, the low test error and high AUC suggest that the model is not simply exploiting the imbalance, but is able to generalize well to unseen data.

#### ⚠️ Limitation

-   Biased toward majority class

------------------------------------------------------------------------

### 🔹 Class Imbalance Handling

#### ⚠️ Problem

-   Failure cases are rare
-   Model tends to ignore minority class

#### ✅ Solution

-   **SMOTE (Synthetic Minority Over-sampling Technique)**
-   **Class Weight Balanced**

#### 📈 Effect

-   Balances class distribution
-   Generates synthetic minority samples

------------------------------------------------------------------------

### 🔹 Model 2: Random Forest + Class Weight Balanced

-   Trained on rebalanced dataset

#### 📊 Observations

-   Recall increases
-   More failures detected
-   False positives increase
-   AUC remains similar

------------------------------------------------------------------------

### 🔹 Model 3: XGBoost (BaseLine)

-   Gradient boosting model

#### 📊 Characteristics

-   Strong predictive performance
-   Sensitive to hyperparameters

------------------------------------------------------------------------

### 🔹 Model 4: XGBoost + SMOTE

-   Gradient boosting model combined with SMOTE for class balancing

#### 📊 Characteristics

-   Captures complex nonlinear relationships
-   Sensitive to hyperparameters and data distribution

------------------------------------------------------------------------

## ⚙️ Features

### 🔹 Model Capability

-   Handles **imbalanced classification problems**

### 🔹 Models Used

-   Random Forest
-   XGBoost

### 🔹 Evaluation Metrics

-   Accuracy
-   Precision
-   Recall
-   F1-score
-   AUC

------------------------------------------------------------------------

## 📂 Dataset

### 🔹 APS Failure Dataset

-   Industrial sensor data

#### 📊 Label Definition

-   `0` → Normal
-   `1` → Failure

#### 📌 Characteristics

-   Highly imbalanced
-   Contains many missing values

------------------------------------------------------------------------

## 📈 Results

### 🔹 Random Forest (Baseline)

-   High accuracy
-   Poor minority class detection

------------------------------------------------------------------------

### 🔹 Random Forest + SMOTE

-   Significant improvement in Recall
-   Better detection of failure cases
-   Increase in false positives
-   AUC remains similar

------------------------------------------------------------------------

### 🔹 Model Comparison

| Model               | Accuracy | Precision | Recall | F1-score | AUC |
|--------------------|----------|----------|--------|----------|-----|
| Random Forest       | **0.993**| **0.949**| 0.736  | **0.829**| XX  |
| RF + Class Weight   | 0.989    | 0.940    | 0.573  | 0.712    | XX  |
| RF + SMOTE          | 0.992    | 0.789    | **0.837** | 0.812  | XX  |
| XGBoost             | 0.991    | 0.904    | 0.704  | 0.791    | XX  |
| XGBoost + SMOTE     | 0.980    | 0.546    | **0.925** | 0.686  | XX  |

#### Insigit
Random Forest achieves the best overall performance, while SMOTE significantly improves recall. Among all methods, Random Forest with SMOTE provides the best balance between precision and recall.


------------------------------------------------------------------------

## 📊 Visualization

### 🔹 Correlation Matrix

![Correlation](images/correlation_matrix.png)

#### 📌 Insight

-   Some features are highly correlated
-   Tree models are less affected by multicollinearity

------------------------------------------------------------------------

### 🔹 Feature distribution / Feature vs class analysis

![Distribution : Example: co_000 vs cf_000](images/feature_distribution.png)

#### 📌 Insight

-   Severe class imbalance
-   Resampling is necessary

------------------------------------------------------------------------

### 🔹 Confusion Matrix (Before SMOTE)

![RF Train CM](images/RandomForest_Train_Confusion_Matrix.png)
![RF Test CM](images/RandomForest_Test_Confusion_Matrix.png)
![RF Balanced Train CM](images/RandomForest_balanced_Train_Confusion_Matrix.png)
![RF Balanced Test CM](images/RandomForest_balanced_Test_Confusion_Matrix.png)
![XGBoost Train CM](images/XGBoost_Train_Confusion_Matrix.png)
![XGBoost Test CM](images/XGBoost_Test_Confusion_Matrix.png)

------------------------------------------------------------------------

### 🔹 Confusion Matrix (After SMOTE)
![RF SMOTE Train CM](images/RandomForest_smote_Train_Confusion_Matrix.png)
![RF SMOTE Test CM](images/RandomForest_smote_Test_Confusion_Matrix.png)
![XGBoost SMOTE Train CM](images/XGBoost_smote_Train_Confusion_Matrix.png)
![XGBoost SMOTE CM](images/XGBoost_smote_Test_Confusion_Matrix.png)

#### 📌 Insight

-   Improved detection of failure cases

------------------------------------------------------------------------

### 🔹 ROC Curve Comparison

![RF ROC](images/RandomForest_ROC_Curve.png)
![RF Balanced ROC](images/RandomForest_balanced_ROC_Curve.png)
![RF SMOTE ROC](images/RandomForest_smote_ROC_Curve.png)
![XGBoost ROC](images/XGBoost_ROC_Curve.png)
![XGBoost SMOTE ROC](images/XGBoost_smote_ROC_Curve.png)

#### 📌 Insight

-   Similar AUC across models
-   AUC alone is insufficient for imbalanced data

------------------------------------------------------------------------

## 🔍 Key Insights

-   Class imbalance significantly affects model performance\
-   Accuracy is not reliable for imbalanced datasets\
-   SMOTE improves Recall but reduces Precision\
-   Trade-off between false positives and false negatives is important

------------------------------------------------------------------------

## 📌 Summary

  Aspect             Observation
  ------------------ ----------------------------
  Imbalance Impact   Significant
  Strength           Recall improvement (SMOTE)
  Weakness           Increased false positives
  Evaluation         Must include Recall & AUC

------------------------------------------------------------------------

## 🚀 How to Run

``` bash
pip install numpy pandas scikit-learn imbalanced-learn matplotlib xgboost
jupyter notebook Hsu_WenYen_HW6.ipynb
```

------------------------------------------------------------------------

## 🧩 Notes

-   Tree-based models are robust to:
    -   Outliers
    -   Correlated features
-   SMOTE may introduce noise
-   Model choice depends on application needs

------------------------------------------------------------------------

## 📂 Project Structure

├── Hsu_WenYen_HW6.ipynb
├── README.md
├── images/
│   ├── correlation_matrix.png
│   ├── feature_distribution.png
│   ├── RandomForest_ROC_Curve.png
│   ├── RandomForest_Train_Confusion_Matrix.png
│   ├── RandomForest_Test_Confusion_Matrix.png
│   ├── RandomForest_balanced_ROC_Curve.png
│   ├── RandomForest_balanced_Train_Confusion_Matrix.png
│   ├── RandomForest_balanced_Test_Confusion_Matrix.png
│   ├── XGBoost_ROC_Curve.png
│   ├── XGBoost_Train_Confusion_Matrix.png
│   ├── XGBoost_Test_Confusion_Matrix.png
│   ├── XGBoost_smote_ROC_Curve.png
│   ├── XGBoost_smote_Train_Confusion_Matrix.png
│   └── XGBoost_smote_Test_Confusion_Matrix.png
------------------------------------------------------------------------

## 👨‍💻 Author

Wen-Yen (Hank) Hsu

------------------------------------------------------------------------

## ⭐ Project Summary

A study on handling imbalanced classification using tree-based models
and SMOTE on the APS Failure dataset.
