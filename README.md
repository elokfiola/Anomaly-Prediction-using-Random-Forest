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

---

### 🔹 5. Evaluation Metrics  
Evaluation was performed using standard classification metrics:  
- **Accuracy** – overall correctness  
- **Precision / Recall / F1-Score** – classification quality for minority class  
- **AUC-ROC** – separation capability  
- **G-Mean** – balance between sensitivity and specificity  
- **Youden’s Index** – overall classification strength  

---

## 🧠 Results & Analysis
| Model | Accuracy | Precision | Recall | F1-Score | G-Mean | Youden’s Index | AUC |
|:------|:---------:|:----------:|:-------:|:---------:|:--------:|:---------------:|:----:|
| Random Forest | **76.2%** | **75%** | **71.5%** | **72%** | **74.9%** | **0.50** | **0.724** |
| RF + SMOTE | 66.7% | 50% | 57.1% | 53% | 64% | 0.29 | 0.714 |

📊 **Key Findings:**
- The **baseline Random Forest** outperformed the oversampled model across all metrics.  
- SMOTE slightly degraded recall, suggesting synthetic samples introduced mild noise.  
- Despite class imbalance, the baseline achieved strong AUC > 0.70 — indicating a reliable separation between normal and anomaly classes.  
- **Training time:**  
  - RF = 17 min  
  - RF + SMOTE = 9 min → ≈ 47% faster, but less accurate.

---

## 📊 Visualization Dashboard
A **Tableau interactive dashboard** was developed to translate model outputs into actionable insights.

### 🔸 1. Meter Overview Dashboard
- Annual summary of meter status (Normal vs Anomaly).  
- Breakdown by **meter type** (Rotary, Turbine, Diaphragm).  
- Aggregated charts showing number of active, calibrated, or faulty meters.

### 🔸 2. Customer Detail Dashboard
- View individual customer records with **usage duration** and **accuracy score**.  
- Displays **maintenance recommendations** (e.g., calibration or replacement).  
- Interactive filters: by meter type, year, or anomaly category.  
- Hover tooltips show **serial number, G-size, and last maintenance date**.

![Dashboard Overview](docs/dashboard_overview.png)

---

## 💡 Insights
- Random Forest remains robust even with limited and imbalanced industrial data.  
- Dashboard analytics enable preventive maintenance by flagging meters with rising anomaly risk.  
- Visualization and model integration provide an explainable approach for technical operators.  
- Future work may include **time-series modeling** or **real-time streaming dashboards**.

---

## 🧩 Tech Stack
| Component | Tool / Library |
|------------|----------------|
| **Programming Language** | Python 3.10 |
| **Libraries** | pandas, numpy, scikit-learn, imbalanced-learn |
| **Visualization** | matplotlib, seaborn, Tableau |
| **Environment** | Jupyter Notebook, Excel |
| **Version Control** | GitHub |

---

## 📂 Repository Structure
