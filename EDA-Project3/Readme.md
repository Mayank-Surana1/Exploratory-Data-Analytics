# Diabetes Prediction using Logistic Regression

A machine learning project that predicts whether a patient has diabetes from diagnostic measurements, using the **Pima Indians Diabetes Database** (Kaggle) and a **Logistic Regression** model built with scikit-learn.

> **Disclaimer:** This project is for learning classification concepts. It is **not** a medical diagnostic tool.

---

## Table of Contents
- [Objective](#objective)
- [Dataset](#dataset)
- [Workflow](#workflow)
- [Project Structure](#project-structure)
- [How to Run](#how-to-run)
- [Step-by-Step Explanation](#step-by-step-explanation)
- [Results](#results)
- [Key Findings](#key-findings)
- [Limitations](#limitations)
- [Tech Stack](#tech-stack)
- [Author](#author)

---

## Objective

Predict the `Outcome` column:

| Value | Meaning |
|-------|---------|
| `0` | No diabetes |
| `1` | Diabetes |

## Dataset

- **Source:** [Pima Indians Diabetes Database, Kaggle](https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database)
- **File:** `diabetes.csv`
- **Size:** 768 rows, 9 columns
- **Class balance:** 500 non-diabetic (about 65%), 268 diabetic (about 35%)

| Feature | Description |
|---------|-------------|
| `Pregnancies` | Number of pregnancies |
| `Glucose` | Plasma glucose concentration |
| `BloodPressure` | Diastolic blood pressure (mm Hg) |
| `SkinThickness` | Triceps skinfold thickness (mm) |
| `Insulin` | 2-hour serum insulin (mu U/ml) |
| `BMI` | Body mass index |
| `DiabetesPedigreeFunction` | Diabetes family-history score |
| `Age` | Age in years |
| `Outcome` | Target: 0 or 1 |

## Workflow

```
Load CSV → Inspect data → Replace invalid zeros → Train-test split
→ Median imputation → Scaling → Train Logistic Regression
→ Evaluate → Interpret coefficients
```

## Project Structure

```
├── diabetes_logistic_regression.ipynb   # Executed notebook (all outputs and graphs visible)
├── diabetes.csv                         # Dataset
├── Logistic_Regression_Report.pdf       # One-page project report
└── README.md
```

## How to Run

### Google Colab (recommended)
1. Open `diabetes_logistic_regression.ipynb` in [Google Colab](https://colab.research.google.com/).
2. Run **Runtime → Restart and run all**.
3. When prompted in the data-loading cell, upload `diabetes.csv`.

### Locally
```bash
git clone <your-repo-url>
cd <your-repo-folder>
pip install numpy pandas matplotlib seaborn scikit-learn jupyter
jupyter notebook diabetes_logistic_regression.ipynb
```
When running locally, replace the Colab `files.upload()` line with `df = pd.read_csv("diabetes.csv")`.

---

## Step-by-Step Explanation

### 1. Import libraries
| Library | Purpose |
|---------|---------|
| `numpy` | Numerical operations, `np.nan`, `np.exp` |
| `pandas` | DataFrame handling |
| `matplotlib`, `seaborn` | Visualisation |
| `train_test_split` | Separate training and test data |
| `Pipeline` | Chain preprocessing and model into one object |
| `SimpleImputer` | Fill missing values |
| `StandardScaler` | Standardise features |
| `LogisticRegression` | The classifier |
| `sklearn.metrics` | Accuracy, precision, recall, F1, ROC-AUC, confusion matrix, ROC curve |

### 2. Load the data
`pd.read_csv` loads `diabetes.csv` into a DataFrame, and `df.head()` confirms it loaded correctly.

### 3. Inspect the data
`df.shape`, `df.info()`, `df.describe()` and `value_counts()` reveal data types, ranges and missing values. They also show the **class imbalance**, which motivates the use of `class_weight="balanced"` and recall/F1 alongside accuracy.

### 4. Replace invalid zeros
A value of `0` is physically impossible for `Glucose`, `BloodPressure`, `SkinThickness`, `Insulin` and `BMI`; in the original data it means "not recorded". These are converted to `NaN` so they cannot distort means, scaling or the model. `Pregnancies` is excluded because 0 is a valid value.

> The version of the CSV used here is already cleaned, so this step finds 0 zeros. It is kept as part of the standard workflow.

### 5. Exploratory visuals
A class-distribution bar chart, feature histograms and a correlation heatmap show the data's shape, skew and relationships.

### 6. Train-test split
```python
train_test_split(X, y, test_size=0.2, random_state=42, stratify=y)
```
- 80% train and 20% test (154 test rows)
- `random_state=42` makes results reproducible
- `stratify=y` keeps the class ratio equal in both sets
- The split happens **before** imputing and scaling to avoid data leakage

### 7. Model pipeline
| Step | What it does | Why |
|------|--------------|-----|
| `SimpleImputer(strategy="median")` | Fills missing values with the column median | Robust to outliers and skewed features |
| `StandardScaler()` | Rescales each feature to mean 0, std 1 | Features have very different scales; makes coefficients comparable |
| `LogisticRegression(class_weight="balanced", max_iter=1000)` | Learns weights and outputs a probability via the sigmoid function | `balanced` penalises mistakes on the rarer diabetic class more, which raises recall |

All statistics (medians, means, standard deviations) are learned from training data only and then applied to the test data automatically.

### 8. Evaluation
| Metric | Formula / idea | Meaning |
|--------|----------------|---------|
| Accuracy | (TP+TN) / all | Overall correct predictions |
| Precision | TP / (TP+FP) | Reliability of positive predictions |
| Recall | TP / (TP+FN) | Share of actual diabetics detected |
| F1-score | Harmonic mean of precision and recall | Balance of the two |
| ROC-AUC | Area under the ROC curve | Class-separation ability across all thresholds |

### 9. Confusion matrix and ROC curve
The confusion matrix shows the type of errors: **FN** (missed diabetics) is the costly one in screening, while **FP** is a false alarm. The ROC curve shows performance across every probability threshold, with a dashed diagonal marking random guessing.

### 10. Coefficient interpretation
Because features are standardised, coefficients are directly comparable. `np.exp(coefficient)` converts each into an **odds ratio**: for example, 2.47 means one standard deviation increase in that feature multiplies the odds of diabetes by about 2.5, with other features held fixed. These show association, not causation.

---

## Results

Test set: 154 samples (`test_size=0.2`, `random_state=42`, stratified).

| Metric | Result |
|--------|--------|
| Accuracy | 0.747 |
| Precision | 0.609 |
| Recall | 0.778 |
| F1-score | 0.683 |
| ROC-AUC | 0.827 |

**Confusion matrix**

|            | Predicted 0 | Predicted 1 |
|------------|-------------|-------------|
| **Actual 0** | TN = 73 | FP = 27 |
| **Actual 1** | FN = 12 | TP = 42 |

**Standardised coefficients**

| Feature | Coefficient | Odds Ratio |
|---------|-------------|------------|
| Glucose | 0.904 | 2.47 |
| Insulin | 0.849 | 2.34 |
| BMI | 0.474 | 1.61 |
| Pregnancies | 0.319 | 1.38 |
| SkinThickness | 0.278 | 1.32 |
| DiabetesPedigreeFunction | 0.228 | 1.26 |
| Age | 0.164 | 1.18 |
| BloodPressure | 0.024 | 1.02 |

---

## Key Findings

- The model reaches a ROC-AUC of about **0.83** and detects about **78%** of diabetic cases in the test set.
- **Glucose**, **Insulin** and **BMI** have the strongest positive coefficients.
- Recall is especially important in a screening-style task, because false negatives are missed cases.
- Balanced class weights trade some precision (more false alarms) for higher recall.

## Limitations

- Small, historical dataset representing a specific population.
- Results depend on the particular train-test split.
- The model is suitable for learning classification concepts, **not** for medical diagnosis.

## Tech Stack

Python · NumPy · pandas · Matplotlib · Seaborn · scikit-learn · Google Colab

## Author

**Name:** _your name_
**Date:** _date_
