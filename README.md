# Exploratory Data Analysis

A practical, end-to-end guide to Exploratory Data Analysis, from raw data to meaningful insights.

EDA is the stage where you learn what your data is actually saying before building machine learning models. It helps you understand the dataset, uncover patterns, detect problems, test assumptions, and decide what should happen next.

## What This Guide Covers

| Stage | Purpose |
|---|---|
| Data Collection | Know where the data comes from and whether it can be trusted |
| Data Understanding | Learn the structure, meaning, types, and scope of the data |
| Data Cleaning | Fix duplicates, inconsistent values, invalid types, and data quality issues |
| Preprocessing | Convert raw fields into analysis-ready features |
| Univariate Analysis | Understand individual variables |
| Bivariate Analysis | Study relationships between two variables |
| Multivariate Analysis | Explore interactions across several variables |
| Missing Values | Understand why data is missing and choose an appropriate treatment |
| Outliers | Separate genuine extremes from errors |
| Feature Engineering | Create useful information from existing variables |
| Visualization | Turn patterns into clear visual evidence |
| Statistical Testing | Test whether observed patterns have statistical support |
| Correlation | Measure and interpret relationships between variables |
| Dimensionality | Control redundant or excessive features |
| Final Insights | Convert analysis into useful conclusions and next steps |

## 1. Start With the Question

Before writing code, define what you are trying to understand.

Ask:

- What problem are we investigating?
- What does each row represent?
- What does each column represent?
- Which variables matter to the problem?
- Is there a target variable?
- What decisions should this analysis support?

Good EDA is not about creating as many charts as possible. Every analysis should answer a question.

## 2. Data Collection

Understand the origin of the dataset before analyzing it.

Check:

- Data source: database, API, CSV, JSON, web scraping, sensors, or other systems
- Collection method and time period
- Sampling frequency and population represented
- Licensing, access permissions, and privacy requirements
- Whether the dataset can be reproduced or updated
- Whether the original raw data has been preserved

Keep the raw dataset unchanged so every transformation can be traced back to the source.

## 3. Data Understanding

Get a first look at the dataset.

Check:

- Number of rows and columns
- Column names
- Data types
- Numerical, categorical, ordinal, datetime, text, and boolean variables
- Unique values and category counts
- Minimum, maximum, mean, median, and percentiles
- Target variable and class balance when applicable
- Business or research meaning of each variable

Create a data dictionary containing:

| Column | Meaning | Type | Unit | Expected Range |
|---|---|---|---|---|
| Example | Description of the variable | Numeric | Unit | Valid range |

## 4. Data Quality and Cleaning

Before looking for patterns, make sure the data itself is reliable.

Look for:

- Duplicate records
- Missing values
- Incorrect data types
- Inconsistent category names
- Extra spaces and spelling differences
- Invalid dates
- Impossible values
- Encoding problems
- Broken or unexpected characters
- Referential integrity issues across related tables

Examples of domain validation:

- Age should not be negative
- Price should normally not be negative
- Dates should follow valid date formats
- Categories such as `Male`, `male`, and `M` may need standardization

Do not blindly delete suspicious values. First understand why they exist.

## 5. Data Preprocessing

Convert the cleaned data into a form suitable for analysis.

Common tasks:

- Convert strings to datetime
- Extract year, month, day, weekday, or seasonality
- Standardize measurement units
- Split composite fields into meaningful columns
- Encode categorical variables when required
- Scale numerical features when the analysis or model requires it
- Normalize text fields
- Prepare consistent formats across datasets

The goal is not to transform everything. Apply only the transformations that support the analytical objective.

## 6. Univariate Analysis

Study one variable at a time.

For numerical variables, examine:

- Mean
- Median
- Mode
- Standard deviation
- Variance
- Minimum and maximum
- Percentiles
- Skewness
- Kurtosis
- Distribution shape

Useful visualizations:

- Histogram
- Density plot
- Box plot

For categorical variables:

- Frequency counts
- Percentages
- Bar charts

Key questions:

- What is typical?
- How widely does the variable vary?
- Is it skewed?
- Are there unusual values?
- Are some categories much more common than others?

## 7. Bivariate Analysis

Study the relationship between two variables.

### Numerical vs Numerical

Use:

- Scatter plots
- Correlation coefficients
- Trend lines when appropriate

Example:

`Horsepower vs Price`

### Numerical vs Categorical

Use:

- Box plots
- Violin plots
- Grouped summaries
- Grouped bar charts where appropriate

### Categorical vs Categorical

Use:

- Cross-tabulation
- Stacked bar charts
- Proportion comparisons

The goal is to understand whether differences or relationships exist, not simply to produce a chart.

## 8. Multivariate Analysis

Real-world patterns often involve several variables at once.

Useful techniques:

- Pair plots
- Correlation heatmaps
- Grouped visualizations
- Faceted charts
- Interaction analysis
- Principal Component Analysis for high-dimensional data
- Clustering exploration when appropriate

Example question:

Does horsepower affect price differently depending on the car's engine size, brand, or fuel type?

## 9. Missing Value Analysis

Missing values are not automatically errors.

First determine:

1. How much data is missing?
2. Which columns are affected?
3. Is missingness concentrated in certain groups?
4. Why might the values be missing?
5. Could the missingness itself contain useful information?

Common strategies:

- Remove rows or columns when justified
- Mean or median imputation
- Mode imputation
- Forward or backward fill
- Model-based imputation

After imputation, compare the resulting distributions with the original data to check for unwanted distortion.

## 10. Outlier Detection

An outlier is an observation that is unusually far from the rest of the data.

Common methods:

- Interquartile Range rule
- Z-score
- Box plots
- Scatter plots
- Domain-specific thresholds

Always distinguish between:

**Data error**

A value caused by incorrect entry, measurement, or processing.

**Genuine extreme value**

A real observation that happens to be unusual.

Possible treatments:

- Keep
- Remove
- Cap
- Transform
- Investigate separately

Document the reason behind the decision.

## 11. Feature Engineering

Feature engineering converts existing information into variables that may be more useful for analysis or modeling.

Examples:

- Extract age from date of birth
- Extract month from a transaction date
- Calculate profit from revenue and cost
- Create price-per-unit
- Group continuous values into meaningful ranges
- Create interaction features
- Apply logarithmic or square-root transformations to highly skewed variables

A new feature should have a clear reason for existing. More columns do not automatically mean better data.

## 12. Data Visualization

Choose the visualization based on the question.

| Question | Useful Visualization |
|---|---|
| What does the distribution look like? | Histogram, density plot |
| Are there outliers? | Box plot |
| How do two numerical variables relate? | Scatter plot |
| How do categories compare? | Bar chart |
| How do groups differ in distribution? | Box plot, violin plot |
| How does something change over time? | Line chart |
| How are numerical variables related? | Correlation heatmap |
| How do multiple variables interact? | Pair plot, faceted chart |

Every chart should have:

- Clear title
- Meaningful axis labels
- Appropriate units
- Useful legend when required
- Consistent formatting

Avoid misleading scales and unnecessary decoration.

## 13. Statistical Testing

Use statistical tests when you need formal evidence for an observed pattern.

Common examples:

- t-test for comparing means between two groups
- ANOVA for comparing means across multiple groups
- Chi-square test for categorical independence
- Correlation significance testing

For each test, define:

- Null hypothesis
- Alternative hypothesis
- Significance level
- Test statistic
- p-value
- Confidence interval
- Effect size where appropriate

A statistically significant result does not automatically mean the effect is practically important.

## 14. Correlation and Relationships

Correlation helps quantify how variables move together.

Common measures:

- Pearson correlation for linear relationships
- Spearman correlation for monotonic relationships and ranked data
- Kendall correlation for ordinal or ranked relationships

Important:

**Correlation does not prove causation.**

Also check for:

- Multicollinearity
- Non-linear relationships
- Confounding variables
- Spurious relationships

Use domain knowledge alongside statistical measures.

## 15. Dimensionality Considerations

More features can create more complexity.

Review whether:

- Features are redundant
- Some variables contain little useful information
- The number of features is reasonable for the number of observations
- Highly correlated predictors can be reduced
- Dimensionality reduction would help visualization or modeling

Possible approaches:

- Feature selection
- Removing redundant variables
- Principal Component Analysis
- Domain-based feature reduction

Document why features were retained, removed, or transformed.

## 16. Tools and Technologies

### Python

Common libraries:

- Pandas for data manipulation
- NumPy for numerical operations
- Matplotlib for visualization
- Seaborn for statistical visualization
- Plotly for interactive charts
- SciPy for statistical analysis
- Scikit-learn for preprocessing and machine learning workflows

### Other Tools

- Jupyter Notebook or JupyterLab
- SQL for structured data extraction
- Git for version control
- Automated profiling tools such as Sweetviz and similar EDA reporting tools

## 17. A Practical EDA Workflow

A useful project flow is:

```text
Raw Data
   |
   v
Understand the Problem
   |
   v
Inspect the Dataset
   |
   v
Check Data Quality
   |
   v
Clean the Data
   |
   v
Preprocess
   |
   v
Univariate Analysis
   |
   v
Bivariate Analysis
   |
   v
Multivariate Analysis
   |
   v
Missing Values and Outliers
   |
   v
Feature Engineering
   |
   v
Visualization
   |
   v
Statistical Validation
   |
   v
Key Insights
   |
   v
Next Steps
