# Predicting NYC Property Sale Prices Using Boosting

**Minor Project 5**

**Author:** Mayank L Surana

**Project Type:** Supervised Machine Learning | Regression

**Dataset:** NYC Housing Dataset

---

## 1. Project Overview

Property prices in New York City vary significantly depending on location, building size, property type, and other structural characteristics.

The objective of this project is to develop a machine learning model that predicts property sale prices using available geographical and building-related information.

The project compares three boosting algorithms against a Linear Regression baseline to identify the model that provides the best predictive performance.

The project also investigates the factors influencing property prices through exploratory data analysis and feature importance analysis.

### Objectives

- Understand and examine the NYC housing dataset.
- Identify and handle missing values, duplicate records, and inconsistent data.
- Perform exploratory data analysis to understand property price patterns.
- Prepare numerical and categorical features for machine learning.
- Apply appropriate transformations to the target variable.
- Train and compare four regression models.
- Evaluate model performance using standard regression metrics.
- Visualize actual and predicted property prices.
- Analyze prediction errors and identify influential features.

---

## 2. Dataset Description

The project uses the `nyc_housing_base.csv` dataset, which contains property sale records from New York City.

Each row represents a property sale, with information about its sale price, geographical location, and building characteristics.

The dataset initially contains **34,439 records and 19 columns**.

### Important Dataset Features

| Feature | Description |
|---|---|
| Sale Price | The recorded selling price of the property. |
| Borough | The New York City borough associated with the property. |
| Latitude | The geographical latitude of the property. |
| Longitude | The geographical longitude of the property. |
| Building Age | The age of the building in years. |
| Lot Area | The total area of the property lot. |
| Building Area | The total building area in square feet. |
| Residential Area | The area allocated to residential use. |
| Commercial Area | The area allocated to commercial use. |
| Residential Units | The number of residential units in the building. |
| Total Units | The total number of units in the building. |
| Number of Floors | The number of floors in the building. |
| Land Use | The classification describing the property's land use. |
| Building Class | The classification identifying the building type. |

The target variable is `sale_price`. The remaining useful features are used as inputs for predicting the target.

### Dataset Characteristics

The dataset contains numerical and categorical variables. It also contains missing values, duplicate records, inconsistent borough information, and observations that require validation before model training.

These issues are examined and addressed during preprocessing.

---

## 3. Technologies and Libraries Used

The project is implemented in Python using Google Colab and Jupyter Notebook.

The following libraries are used:

| Library | Purpose |
|---|---|
| Pandas | Loading, cleaning, manipulating, and analyzing tabular data. |
| NumPy | Numerical calculations and mathematical transformations. |
| Matplotlib | Creating charts and visualizations. |
| Seaborn | Statistical visualization and exploratory data analysis. |
| Scikit-learn | Data splitting, regression models, and model evaluation. |
| XGBoost | Implementing the XGBoost regression algorithm. |

---

## 4. Data Exploration and Quality Assessment

The dataset is initially examined to understand its structure and identify potential data quality issues.

The following operations are performed:

- Displaying the first five records.
- Checking the dataset dimensions.
- Examining column names and data types.
- Generating descriptive statistics.
- Counting missing values in each column.
- Identifying duplicate records.
- Comparing the two borough columns to identify inconsistencies.
- Checking records containing zero building area or zero total units.

This assessment helps identify unreliable observations and determine the appropriate cleaning strategy.

### Important Observation

A substantial proportion of records contain disagreements between the two borough columns. Such inconsistencies may indicate unreliable property information, so these records are removed before training.

---

## 5. Data Cleaning and Preprocessing

Data preprocessing prepares the dataset for reliable analysis and machine learning.

The following steps are implemented in the notebook.

### 5.1 Removing Duplicate Records

Duplicate rows are identified and removed to prevent repeated observations from unnecessarily influencing the analysis.

### 5.2 Removing Inconsistent Borough Records

The numeric borough codes are mapped to their corresponding borough abbreviations and compared with the second borough column.

Records where the two borough representations disagree are removed.

### 5.3 Removing Invalid Observations

Records are removed when they contain:

- Zero or negative building area.
- Zero or negative total units.
- Sale prices below $10,000.
- Missing latitude or longitude values.

These conditions help eliminate observations that are unsuitable for the intended analysis.

### 5.4 Handling Missing Values

Missing numerical values in residential area, commercial area, and number of floors are replaced with their respective median values.

Missing land use values are replaced with the most frequently occurring category, known as the mode.

### 5.5 Grouping Building Classes

Building class values are grouped according to their first character.

This reduces the number of distinct categories and simplifies the representation of building types.

### 5.6 Removing Redundant Features

Columns containing redundant information, identification numbers, or information already represented by other features are removed.

This includes the duplicate borough representation, block and lot identifiers, ZIP code, year built, and the original building class column.

The grouped building class and building age are retained for modeling.

### 5.7 Encoding Categorical Variables

Categorical variables are converted into numerical representations using one-hot encoding.

One-hot encoding creates separate binary indicator columns for categories, allowing machine learning algorithms to process categorical information.

The `drop_first` option is used to omit one category from each encoded categorical feature.

### 5.8 Log Transformation of Sale Price

The original sale price distribution is strongly right-skewed because a relatively small number of expensive properties have very high prices.

The target variable is transformed using:

`log1p(sale_price)`

The transformation is mathematically defined as:

\[
y' = \ln(1+y)
\]

where \(y\) represents the original sale price.

This transformation reduces the influence of extreme values on the target distribution and makes the distribution more balanced.

The model predictions are subsequently converted back to dollar values using the inverse transformation.

### Final Dataset

After the cleaning operations, the dataset contains approximately **24,591 records**.

The prepared data is then used for exploratory analysis and model development.

---

## 6. Exploratory Data Analysis

Exploratory Data Analysis, or EDA, is performed to understand the distribution of the target variable and the relationships between different features.

### 6.1 Sale Price Distribution

Histograms are created to compare the original sale price distribution with the log-transformed distribution.

**Observation:** The original distribution is strongly right-skewed. The log transformation produces a more balanced distribution.

### 6.2 Median Sale Price by Borough

A bar chart is generated to compare median property sale prices across the five New York City boroughs.

**Observation:** Brooklyn has the highest median sale price in the notebook's analysis, while the Bronx has the lowest.

This indicates that geographical location is an important consideration when estimating property prices.

### 6.3 Building Area Versus Sale Price

A scatter plot is created to examine the relationship between building area and sale price.

The visualization uses logarithmic scales to make differences across property sizes and prices easier to examine.

**Observation:** Property prices vary substantially even among properties with comparable building areas, indicating that building size alone cannot explain sale prices.

### 6.4 Sale Price by Building Age

Buildings are grouped into different age ranges, and their median sale prices are compared.

**Observation:** The relationship between building age and sale price is not strictly linear. This supports investigating models capable of capturing nonlinear patterns.

### 6.5 Correlation Heatmap

A correlation heatmap is generated for selected numerical features, including sale price, lot area, building area, residential area, commercial area, unit counts, number of floors, and building age.

**Observation:** Several area and unit-related variables are correlated with one another. The numerical relationships with sale price are not sufficiently strong to explain property prices independently.

These findings motivate the use of multiple features and nonlinear regression models.

---

## 7. Feature Preparation and Data Splitting

The dataset is divided into input features and the target variable.

The target is the logarithmically transformed sale price. The remaining selected features are used to predict this value.

After categorical encoding, the dataset is split into training and testing subsets.

| Subset | Number of Records | Proportion |
|---|---:|---:|
| Training Set | 19,672 | 80% |
| Testing Set | 4,919 | 20% |
| Total | 24,591 | 100% |

The split uses `random_state=42` to make the results reproducible.

### Definitions

**Training Set:** The portion of the dataset used to teach the model patterns and relationships.

**Testing Set:** The separate portion used to evaluate how well the trained model predicts previously unseen observations.

**Feature:** An input variable used by the model to make predictions.

**Target Variable:** The value the model is designed to predict. In this project, it is the transformed property sale price.

---

## 8. Machine Learning Models

Four regression models are trained and evaluated.

### 8.1 Linear Regression

Linear Regression is a supervised learning algorithm that models the relationship between input variables and a continuous target using a linear equation.

It serves as the baseline model against which the boosting algorithms are compared.

### 8.2 AdaBoost Regressor

AdaBoost, short for Adaptive Boosting, is an ensemble learning algorithm that combines multiple weak learners into a stronger predictive model.

It increases the emphasis on observations that previous learners predict poorly, helping subsequent learners focus on difficult cases.

### 8.3 Gradient Boosting Regressor

Gradient Boosting builds decision trees sequentially. Each successive tree attempts to correct the remaining prediction errors by optimizing a loss function.

Combining these trees can capture complex relationships between input features and property prices.

### 8.4 XGBoost Regressor

XGBoost, or Extreme Gradient Boosting, is an optimized implementation of gradient boosting.

It incorporates regularization and computational improvements to support efficient model training and predictive performance.

### Model Training Configuration

The notebook uses the following configurations:

| Model | Main Configuration |
|---|---|
| Linear Regression | Default configuration |
| AdaBoost | 100 estimators |
| Gradient Boosting | 300 estimators, learning rate 0.1, maximum depth 4 |
| XGBoost | 600 estimators, learning rate 0.05, maximum depth 6, row and column subsampling of 0.8 |

All four models are trained using the same training dataset.

Their predictions are evaluated using the same testing dataset.

---

## 9. Model Evaluation Metrics

Three evaluation metrics are used to compare the predictive performance of the trained models.

### 9.1 R-Squared Score

R-squared, represented by \(R^2\), measures how much of the variation in the target variable is explained by a model.

A higher score generally indicates better predictive performance.

An \(R^2\) value of 0.61 indicates that the model explains approximately 61% of the variation in the log-transformed target, according to the evaluation used in this project.

### 9.2 Root Mean Squared Error

Root Mean Squared Error, or RMSE, measures the square root of the average squared prediction errors.

\[
RMSE = \sqrt{\frac{1}{n}\sum_{i=1}^{n}(y_i-\hat{y}_i)^2}
\]

Here, \(y_i\) represents an actual value, \(\hat{y}_i\) represents a predicted value, and \(n\) is the number of observations.

RMSE penalizes larger errors more heavily than smaller errors.

In this project, RMSE is calculated on the log-transformed price scale. Therefore, it should not be interpreted directly as an error measured in dollars.

### 9.3 Mean Absolute Error

Mean Absolute Error, or MAE, measures the average absolute difference between actual and predicted values.

\[
MAE = \frac{1}{n}\sum_{i=1}^{n}|y_i-\hat{y}_i|
\]

A lower MAE indicates that predictions are closer to the actual values on average.

The notebook converts predictions and actual target values back to dollars before calculating MAE.

---

## 10. Model Performance Comparison

The following results are obtained in the project notebook.

| Model | R-Squared Score | RMSE on Log Price | MAE |
|---|---:|---:|---:|
| XGBoost | 0.6101 | 0.4917 | $345,026 |
| Gradient Boosting | 0.5857 | 0.5068 | $358,460 |
| Linear Regression | 0.3598 | 0.6300 | $499,941 |
| AdaBoost | 0.1562 | 0.7233 | $587,908 |

### Interpretation

XGBoost achieves the highest R-squared score and the lowest RMSE and MAE among the four tested models.

Gradient Boosting is the second-best model.

Both boosting models outperform the Linear Regression baseline in this experiment, suggesting that nonlinear relationships are important when predicting NYC property sale prices.

AdaBoost achieves the lowest R-squared score and the highest prediction errors among the tested models.

**Best Performing Model: XGBoost Regressor**

The reported MAE of approximately $345,026 indicates that prediction errors remain substantial in dollar terms.

---

## 11. Actual Versus Predicted Prices

A scatter plot compares the actual sale prices with the prices predicted by the best-performing model.

The chart uses logarithmic axes to accommodate the wide range of property prices.

A reference line represents perfect predictions, where predicted prices equal actual prices.

Points closer to this line indicate more accurate predictions.

This visualization helps identify how closely the model's predictions correspond to observed sale prices.

---

## 12. Residual Analysis

Residuals represent the differences between actual and predicted target values.

In this project, residuals are calculated on the log-transformed price scale.

\[
Residual = Actual\ Log\ Price - Predicted\ Log\ Price
\]

A histogram is generated to examine their distribution.

Residual analysis helps identify systematic prediction errors and understand whether the model consistently overpredicts or underpredicts certain observations.

Residuals close to zero indicate predictions that are close to actual values on the log scale.

---

## 13. Feature Importance Analysis

Feature importance analysis is performed to identify which input variables contribute most to the predictions made by the selected tree-based model.

The notebook calculates feature importance scores and visualizes the ten most important features.

The analysis identifies the Manhattan borough indicator as the leading feature, followed by residential unit count and land-use indicators.

### Definition

**Feature Importance:** A measure provided by a trained model that estimates the relative contribution of individual input features to its predictions.

Feature importance helps explain which variables the model relies on most heavily.

However, high feature importance does not establish causation. It does not prove that changing a particular feature will directly cause a corresponding change in property price.

---

## 14. Key Findings

The project produces the following findings:

1. Data cleaning is important because the original dataset contains duplicate records, missing values, and inconsistent borough information.

2. The sale price distribution is strongly right-skewed, making a logarithmic transformation useful for preparing the target variable.

3. Property prices vary across boroughs, demonstrating the importance of geographical information.

4. Building area, building age, and unit-related characteristics provide useful information, but no single numerical variable fully explains sale prices.

5. XGBoost achieves the best predictive performance among the four evaluated models.

6. Gradient Boosting performs better than Linear Regression and AdaBoost in the reported evaluation.

7. The feature importance analysis highlights geographical and building-related information as influential predictors.

8. Despite its better performance, the selected model still produces substantial errors when predicting property prices in dollars.

---

## 15. Limitations

The project has several limitations.

- The dataset does not provide detailed individual-unit characteristics such as bedrooms and property condition.
- Sale dates are unavailable for representing changes in market conditions over time.
- Some building-level characteristics may not accurately describe individual apartment sales.
- The model's average absolute prediction error remains substantial.
- The reported results depend on the available dataset, preprocessing decisions, selected features, and model configurations.
- The models have not been exhaustively optimized through systematic hyperparameter tuning.

These limitations should be considered when interpreting the predictions.

---

## 16. Future Improvements

The following improvements could be explored in future work:

- Apply Grid Search or Randomized Search for hyperparameter optimization.
- Add neighborhood-level property statistics and geographical indicators.
- Incorporate sale dates and additional market information when available.
- Investigate more detailed building classifications and property characteristics.
- Compare XGBoost with other advanced algorithms, including LightGBM and CatBoost.
- Examine model performance across different boroughs and price ranges.
- Investigate alternative feature engineering strategies and methods for reducing prediction errors.

---

## 17. Conclusion

This project demonstrates an end-to-end machine learning workflow for predicting New York City property sale prices.

The workflow includes data loading, data quality assessment, preprocessing, exploratory data analysis, feature engineering, model training, model evaluation, prediction visualization, residual analysis, and feature importance analysis.

Four regression models are compared using a consistent training and testing procedure.

Among the evaluated models, XGBoost achieves the strongest results, with an R-squared score of 0.6101, an RMSE of 0.4917 on the log-transformed target, and an MAE of approximately $345,026.

The results suggest that boosting algorithms can capture useful nonlinear patterns in property data and outperform the linear baseline in this experiment.

However, the remaining prediction error and the limitations of the available dataset indicate that further feature development, model tuning, and validation are needed before using the model for practical property valuation.

Overall, the project provides practical experience in data preprocessing, exploratory analysis, ensemble learning, regression evaluation, and interpreting machine learning results.

---
