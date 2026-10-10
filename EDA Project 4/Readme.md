# Titanic Survival Prediction using Random Forest

A machine learning project that predicts whether a passenger survived the RMS Titanic disaster using a **Random Forest Classifier**. The notebook covers the full workflow: data exploration, preprocessing, model training, evaluation, and feature importance analysis.

## Project Overview

- **Problem type:** Binary classification (Survived = 1, Not Survived = 0)
- **Algorithm:** Random Forest Classifier (`scikit-learn`)
- **Environment:** Google Colab / Jupyter Notebook
- **Notebook:** `Mayank_L_Surana_Random_Forest_Project_4.ipynb`
- **Dataset:** `Titanic-Dataset.csv`

## Dataset Description

The dataset contains passenger records from the RMS Titanic, including demographic details, ticket information, and survival status.

- **Rows:** 891 passengers
- **Columns:** 12
- **Target variable:** `Survived`
- **Class distribution:** 549 did not survive (61.6%) and 342 survived (38.4%)

| Column | Description |
|---|---|
| `PassengerId` | Unique ID for each passenger |
| `Survived` | Survival status (0 = No, 1 = Yes) — **target** |
| `Pclass` | Ticket class (1 = First, 2 = Second, 3 = Third) |
| `Name` | Passenger name |
| `Sex` | Gender of the passenger |
| `Age` | Age in years |
| `SibSp` | Number of siblings / spouses aboard |
| `Parch` | Number of parents / children aboard |
| `Ticket` | Ticket number |
| `Fare` | Ticket fare paid |
| `Cabin` | Cabin number |
| `Embarked` | Port of embarkation (C = Cherbourg, Q = Queenstown, S = Southampton) |

**Missing values:** `Age` (177), `Cabin` (687), `Embarked` (2).

## Workflow

1. **Import libraries and load the dataset** (pandas, matplotlib, seaborn)
2. **Explore the data** — shape, data types, summary statistics, missing values
3. **Handle missing values**
   - `Age` → filled with the median
   - `Embarked` → filled with the mode
4. **Exploratory Data Analysis**
   - Survival distribution
   - Correlation heatmap
   - Survival by gender
   - Survival by passenger class
   - Age distribution
5. **Prepare features** — separate `X` and `y`, one-hot encode categorical columns (`drop_first=True`)
6. **Train / test split** — 80% / 20% with `stratify=y` and `random_state=42`
7. **Train the model** — `RandomForestClassifier(n_estimators=100, max_depth=10, random_state=42)`
8. **Evaluate** — confusion matrix, precision, recall, F1-score, ROC-AUC
9. **Feature importance** — top 10 most influential features

## Results

| Metric | Score |
|---|---|
| Accuracy | ~0.68 |
| Precision (Survived) | 0.875 |
| Recall (Survived) | 0.203 |
| F1-Score (Survived) | 0.329 |
| ROC-AUC | 0.818 |

**Key insights**
- **Gender** and **passenger class** are among the strongest predictors of survival, followed by **fare** and **age**.
- Female passengers had a much higher survival rate than male passengers.
- First-class passengers survived more often than third-class passengers.

## Possible Improvements

- Drop high-cardinality text columns (`Name`, `Ticket`, `Cabin`) or engineer features from them (e.g., title extraction, `FamilySize`, cabin deck) instead of one-hot encoding them directly, which creates a very large number of sparse columns.
- Tune hyperparameters with `GridSearchCV` / `RandomizedSearchCV`.
- Try class weighting or threshold tuning to improve recall on the "Survived" class.
- Compare against other models (Logistic Regression, Gradient Boosting, XGBoost).

## Tech Stack

- Python 3
- pandas
- matplotlib
- seaborn
- scikit-learn

## How to Run

1. Clone this repository:
   ```bash
   git clone <your-repo-url>
   cd <your-repo-folder>
   ```
2. Install the dependencies:
   ```bash
   pip install pandas matplotlib seaborn scikit-learn jupyter
   ```
3. Open the notebook:
   ```bash
   jupyter notebook Mayank_L_Surana_Random_Forest_Project_4.ipynb
   ```
4. Make sure `Titanic-Dataset.csv` is in the same folder as the notebook.

> **Note:** In Google Colab the notebook uses `files.upload()` to load the CSV. When running locally, remove the `from google.colab import files` and `files.upload()` lines.

## Author

**Mayank L Surana**
