# Cars Dataset - Exploratory Data Analysis

Exploratory Data Analysis on an automobile dataset to understand pricing patterns, clean data
quality issues, and surface relationships between a car's specifications and its price,
through descriptive statistics and visualizations. No machine learning model is built; the
focus is purely on inspection, cleaning, and visual and statistical exploration.

---

## Repository Contents

| File | Description |
|---|---|
| Cars EDA Project notebook (.ipynb) | Jupyter/Colab notebook containing the full EDA workflow: loading, cleaning, statistics, and visualizations. |
| Cars Dataset (.csv) | The raw automobile dataset used for analysis (208 rows, 26 columns). |
| README.md | This file. |

---

## Objective

- Inspect the structure and quality of the dataset (shape, types, missing values, duplicates).
- Clean the data and document every cleaning decision.
- Compute descriptive statistics for numerical and categorical features.
- Explore relationships through univariate, bivariate, and multivariate analysis.
- Identify outliers and correlations, especially around car price.

---

## Dataset Overview

- Rows (raw): 208
- Columns: 26
- Rows after removing duplicates: 205
- Target/focus variable: price

### Data Dictionary

| Column | Type | Definition |
|---|---|---|
| car ID | Integer | Unique identifier for each listing or row. |
| symboling | Integer | Insurance risk rating, from -3 (safe) to +3 (risky), assigned based on how risky the car is to insure relative to its price. |
| CarName | Text | Manufacturer and model name, for example "toyota corolla". |
| fueltype | Category | Type of fuel the car uses: gas or diesel. |
| aspiration | Category | Engine aspiration type: standard (naturally aspirated) or turbo (turbocharged). |
| doornumber | Category | Number of doors: two or four. |
| carbody | Category | Body style, for example sedan, hatchback, wagon, hardtop, or convertible. |
| drivewheel | Category | Drive configuration: front wheel drive, rear wheel drive, or four wheel drive. |
| enginelocation | Category | Position of the engine: front or rear. |
| wheelbase | Float | Distance between the front and rear axles, in inches. |
| carlength | Float | Overall length of the car, in inches. |
| carwidth | Float | Overall width of the car, in inches. |
| carheight | Float | Overall height of the car, in inches. |
| curbweight | Integer | Weight of the car without occupants or cargo, in pounds. |
| enginetype | Category | Engine design, for example dohc, ohc, ohcv, or rotor. |
| cylindernumber | Category | Number of cylinders, written as a word, for example four, six, or eight. |
| enginesize | Float | Engine displacement in cubic inches; larger generally means more power. |
| fuelsystem | Category | Fuel delivery system, for example mpfi (multi point fuel injection) or 2bbl (two barrel carburetor). |
| boreratio | Float | Bore diameter of the engine cylinder, in inches. |
| stroke | Float | Piston stroke length, in inches. |
| compressionratio | Float | Ratio of cylinder volume at the bottom versus top of the piston stroke; higher generally means more efficient combustion. |
| horsepower | Float | Engine power output, in horsepower. |
| peakrpm | Integer | Engine speed, in RPM, at which peak horsepower is produced. |
| citympg | Integer | Fuel efficiency in city driving, in miles per gallon. |
| highwaympg | Integer | Fuel efficiency in highway driving, in miles per gallon. |
| price | Float | Selling price of the car, in USD. The main variable of interest for this analysis. |

Note: symboling, boreratio, stroke, and compressionratio are technical engineering fields.
Keep these in mind if a chart or statistic involving them looks unintuitive, since they are
less commonly discussed than horsepower, price, or fuel economy.

---

## Data Cleaning Summary

| Step | Before | After | Notes |
|---|---|---|---|
| Duplicate rows | 208 rows | 205 rows | Three fully duplicated rows were dropped. |
| Missing values | Four cells missing across fueltype, enginesize, horsepower, and price | Zero missing | See handling below. |

Missing value handling:

- Numerical columns (horsepower, price, enginesize) were filled with the median of each
  column, to avoid distortion from outliers or skew.
- The categorical column (fueltype) was filled with the mode, the most frequent value.

---

## EDA Workflow

The notebook follows this structure, in order:

1. Setup: import libraries (pandas, numpy, matplotlib, seaborn).
2. Load and inspect: shape, column list, info summary, describe summary.
3. Data quality check: missing values (count and percentage), duplicate rows, and
   categorical consistency (value counts per column).
4. Cleaning: drop duplicates, impute missing values (median or mode), and record
   before and after row counts.
5. Descriptive statistics: summary statistics for numerical and categorical columns,
   plus price specific statistics (mean, median, minimum, maximum, standard deviation).
6. Univariate analysis:
   - Histogram of price distribution
   - Count plot of cars by fuel type
   - Histogram of horsepower distribution
7. Bivariate analysis:
   - Scatter plot of horsepower versus price
   - Scatter plot of engine size versus price
   - Box plot of price distribution by fuel type
8. Multivariate analysis:
   - Correlation heatmap across all numerical columns
9. Outlier analysis:
   - Box plot of price outliers

---

## Chart Types Used

Histogram, count plot, scatter plot, box plot, and correlation heatmap. Five distinct chart
types across eight charts in total.

---

## How to Run

1. Clone this repository.

   ```
   git clone <your-repo-url>
   cd <your-repo-folder>
   ```

2. Install dependencies.

   ```
   pip install pandas numpy matplotlib seaborn
   ```

3. Open the notebook in Jupyter or Google Colab.

   ```
   jupyter notebook "Cars EDA Project.ipynb"
   ```

4. If running in Google Colab, the second cell uses a file upload prompt to load the CSV
   file manually. To run locally instead, replace that step with a direct file read of the
   CSV using pandas.

---

## Suggested Next Steps

The following are not yet included in the notebook and are worth adding:

- A written key findings section summarizing what each chart shows, for example how
  strongly horsepower and engine size correlate with price.
- A note on the limitations of the dataset, such as its small sample size, absence of a
  listing date, or coverage limited to specific market specifications.
- A brief comment on whether the duplicate rows and the missing values meaningfully affect
  results, given the dataset contains only 205 to 208 rows in total.

---

## Author

Mayank L. Surana

## License

Add a license of your choice, such as MIT, if this repository is public.
