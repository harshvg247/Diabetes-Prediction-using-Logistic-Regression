# Diabetes Prediction using Logistic Regression with Statistical Inference

## Overview

This project builds a **logistic regression model** to predict diabetes using the Pima Indians Diabetes Dataset. It integrates:

* **Predictive modeling (scikit-learn)**
* **Statistical inference (statsmodels)**
* **Threshold optimization (ROC-based)**
* **Feature selection via hypothesis testing**

The goal is not only accurate prediction but also **interpretability and statistical validity**.

---

## Dataset

* Source: Pima Indians Diabetes Dataset
* Observations: ~768 patients
* Target variable:

  * `Outcome` (0 = Non-diabetic, 1 = Diabetic)

### Features used

* Pregnancies
* Glucose
* BloodPressure
* BMI
* DiabetesPedigreeFunction
* Age

### Dropped Features

* `Insulin`, `SkinThickness`

  * High missing values
  * Introduced noise

---

## Data Preprocessing

### 1. Handling Invalid Values

* Zero values in:

  * Glucose, BloodPressure, BMI
* Treated as missing and imputed using **median**

### 2. Feature Scaling

* StandardScaler applied before logistic regression

### 3. Train-Test Split

* Stratified split (85% train, 15% test)

---

## Statistical Inference (Logit Model)

Logistic regression was fitted using **Maximum Likelihood Estimation (MLE)** via `statsmodels`.

### Hypothesis Tested

[
H_0: \beta_i = 0
]

### Significant Features (p < 0.05)

* Glucose (highly significant)
* BMI (highly significant)
* Pregnancies (significant)
* DiabetesPedigreeFunction (significant)

### Insignificant Features

* BloodPressure (p ≈ 0.42)
* Age (p ≈ 0.29)

### Conclusion

* BloodPressure and Age were **statistically insignificant**
* Removed to form a **reduced model**

---

## Predictive Modeling

### Model Used

* Logistic Regression (scikit-learn)

---

## Threshold Optimization

Instead of default threshold (0.5), optimal threshold was computed using:

[
\text{Youden Index} = TPR - FPR
]

### Optimal Thresholds

* Full model: ~0.286
* Reduced model: ~0.268

---

## Model Performance

| Metric    | Full Model (0.5) | Full Model (Optimal) | Reduced Model (Optimal) |
| --------- | ---------------- | -------------------- | ----------------------- |
| Accuracy  | 0.724            | 0.767                | 0.767                   |
| Precision | 0.611            | 0.610                | 0.607                   |
| Recall    | 0.550            | 0.900                | **0.925**               |
| F1 Score  | 0.579            | 0.727                | **0.733**               |
| AUC-ROC   | 0.837            | 0.837                | 0.833                   |

---

## Key Insights

* **Glucose is the strongest predictor**
* Threshold tuning significantly improves **recall**
* Reduced model performs **as well or better** than full model
* Removing insignificant variables improves interpretability without hurting performance

---

## Medical Interpretation

* High recall (~92%) ensures most diabetic patients are detected
* Slight drop in precision is acceptable in diagnostic settings
* Model is suitable for **screening purposes**

---

## Project Structure

```
├── data/
│   └── diabetes.csv
├── main.ipynb
├── requirements.txt
└── README.md
```

---

## Installation

```bash
pip install -r requirements.txt
```

---

## How to Run

1. Open `main.ipynb`
2. Run all cells sequentially
3. Outputs include:

   * Statistical summary (p-values)
   * ROC curve
   * Confusion matrices
   * Model comparison

---

## Conclusion

This project demonstrates a complete pipeline combining:

* Statistical inference
* Machine learning
* Decision threshold optimization

The final model is both **interpretable and clinically meaningful**.

---

## Future Work

* Regularization (L1/L2)
* Cross-validation tuning
* Alternative models (Random Forest, XGBoost)
* Cost-sensitive learning
