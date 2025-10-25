# Anomaly-Prediction-using-Random-Forest

![Language](https://img.shields.io/badge/Language-Python%203.10-blue)
![Algorithm](https://img.shields.io/badge/Algorithm-Random%20Forest-green)
![Data%20Balance](https://img.shields.io/badge/Technique-SMOTE-orange)
![Visualization](https://img.shields.io/badge/Dashboard-Tableau-yellow)
![Category](https://img.shields.io/badge/Focus-Anomaly%20Detection-purple)
![Status](https://img.shields.io/badge/Status-Completed-success)


---

## 📘 Overview
Accurate gas flow measurement is essential for operational efficiency and financial reliability.  
This project demonstrates how **machine learning**—specifically the **Random Forest algorithm**—can be applied to **detect anomalies in customer gas meter data**.  
By identifying abnormal meter behavior early, operators can schedule maintenance proactively and prevent data or energy losses.

A complementary **interactive dashboard** was also built to visualize meter status, anomaly distribution, and maintenance recommendations.

---

## 🎯 Objectives
- Build a **binary classification model** to distinguish between normal and anomalous meter conditions.  
- Handle **imbalanced data** using the **Synthetic Minority Oversampling Technique (SMOTE)**.  
- Evaluate and compare the performance of Random Forest models with and without SMOTE.  
- Develop an **interactive Tableau dashboard** to monitor anomalies and support decision-making.

---

## ⚙️ Workflow & Methodology
### 🔹 1. Data Understanding  
The dataset consists of gas meter attributes collected from 2022 – 2025, including:  
- Brand and type of meter (Rotary, Turbine, Diaphragm)  
- Year of installation and usage duration  
- Meter size (G-Size) and pipe diameter  
- Maintenance notes and replacement reasons  

Total records: **84 meters**

---

### 🔹 2. Data Preprocessing  
- Converted categorical variables (`Brand`, `Meter Type`) to numerical using **One-Hot Encoding**.  
- Created a **binary target label**:  
  - `0` → Normal meter  
  - `1` → Anomalous meter (bouncing, macet, calibration issues, etc.)  
- Split dataset into **80% training** and **20% testing** subsets.  
- Removed duplicates and missing values for consistent input dimensions.

---

### 🔹 3. Handling Class Imbalance with SMOTE  
Initial distribution:  
- Normal : 41 samples  
- Anomaly : 22 samples  

Applied **SMOTE** (k-nearest neighbors) to oversample the minority class, generating synthetic points.  
After balancing, both classes contained **41 : 41** records — achieving a 50 : 50 ratio.

---

### 🔹 4. Model Development  
Two experiments were conducted:

| Experiment | Description |
|-------------|--------------|
| **Model 1** | Random Forest (baseline, no SMOTE) |
| **Model 2** | Random Forest + SMOTE (oversampled training set) |

Hyperparameter tuning performed using **GridSearchCV** with 5-fold stratified cross-validation.

**Best parameters found:**
max_depth = 8
max_features = 0.5
min_samples_leaf = 2
n_estimators = 300
class_weight = 'balanced'
random_state = 42
