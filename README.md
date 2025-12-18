# Census Income Prediction – Data Science Technical Assessment

## 📌 Problem Statement

The objective of this project is to identify demographic, educational, and employment-related characteristics associated with individuals earning **more or less than $50,000 per year**, using anonymized U.S. Census data.

This work was completed as part of a **Data Scientist Technical Assessment**, with a focus on:

* Sound data science methodology
* Interpretability and communication
* Production-ready, reproducible code

---

## 📊 Dataset Overview

The dataset originates from the U.S. Census Bureau and consists of approximately **300,000 individuals**, split into predefined training and testing files.

Key characteristics:

* **Training instances:** ~199,523
* **Testing instances:** ~99,762
* **Target imbalance:**

  * ≤ $50K → ~93.8%
  * > $50K → ~6.2%
* **Feature types:**

  * Continuous: 7
  * Categorical: 33

Metadata provided by the Census Bureau was explicitly used to guide preprocessing decisions.

---

## ⚠️ Key Challenges

1. **Severe class imbalance**, making accuracy a misleading metric
2. **High-cardinality categorical features**, leading to dimensionality expansion
3. **Multicollinearity**, introduced by overlapping demographic concepts
4. **Customer-facing requirement**, requiring interpretability and clarity

---

## 🔍 Exploratory Data Analysis (EDA)

Key findings from EDA:

* Income is strongly associated with age, weeks worked, education level, and occupation group
* Several demographic variables encode overlapping information (e.g., migration and residence history)
* A naive majority-class model achieves **93.8% accuracy**, setting a critical baseline

EDA outputs are documented with visualizations and summary tables in the notebooks.

---

## 🧹 Data Preparation & Feature Engineering

The following steps were applied consistently to **both training and test datasets**:

* Explicit handling of “Not in universe” categories
* Logical grouping of categorical levels based on Census metadata
* One-Hot Encoding with reference-level dropping to avoid dummy variable traps
* Numeric feature scaling for linear models
* Feature diagnostics using:

  * **Correlation analysis (>|0.95|)**
  * **Variance Inflation Factor (VIF)**

Redundant variables were removed only after baseline modeling to avoid premature information loss.

---

## 🤖 Modeling Approach

Two complementary models were developed:

### 1️⃣ Logistic Regression (Baseline & Interpretable Model)

* Class imbalance handled via `class_weight='balanced'`
* Used to:

  * Establish baseline performance
  * Interpret feature influence
  * Diagnose multicollinearity impact

### 2️⃣ Random Forest (Non-linear Benchmark)

* Captures interaction effects
* Used for performance comparison, not interpretability replacement

---

## 📈 Model Evaluation

Given the imbalanced target, evaluation focused on:

* **Recall (high-income class)**
* **F1-score**
* **ROC-AUC**

### Logistic Regression (Validation Set)

* **ROC-AUC:** ~0.94
* **Recall (>50K):** ~0.89
* Accuracy intentionally sacrificed to improve minority-class detection

This represents a substantial improvement over the majority-class baseline.

---

## 🧠 Key Insights

* Employment intensity, education level, and occupation category are the strongest predictors of higher income
* Several demographic variables exhibit semantic multicollinearity
* Logistic regression provided strong discrimination while remaining interpretable
* Random Forest marginally improved recall but reduced transparency

---

## 🚧 Limitations & Future Work

* Hyperparameter tuning and threshold optimization were limited by scope
* Advanced imbalance techniques (e.g., SMOTE) could further improve precision
* Feature importance stability could be explored across bootstrap samples

---

## 📁 Repository Structure

```
├── notebooks/
│   ├── 01_data_understanding.ipynb
│   ├── 02_eda.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_modeling.ipynb
├── slides/
│   └── census_income_presentation.pdf
├── README.md
```

---

## ✅ Final Notes

The goal of this assessment was not model perfection, but rather to:

* Demonstrate a structured data science workflow
* Communicate findings effectively
* Make transparent, defensible modeling decisions

This repository is fully reproducible and designed for collaborative review.
