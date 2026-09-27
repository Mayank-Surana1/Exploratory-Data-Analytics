# 🚗 Cars Dataset — Exploratory Data Analysis (EDA)

Exploratory Data Analysis on an automobile dataset to understand pricing patterns, clean data
quality issues, and surface relationships between a car's specifications and its price —
through descriptive statistics and visualizations. No machine-learning model is built; the
focus is purely on inspection, cleaning, and visual/statistical exploration.

---

## 📁 Repository Contents

| File | Description |
|---|---|
| `Mayank_L_Surana_Cars_EDA_Project2.ipynb` | Jupyter/Colab notebook containing the full EDA workflow — loading, cleaning, statistics, and visualizations. |
| `Cars_Dataset.csv` | The raw automobile dataset used for analysis (208 rows × 26 columns). |
| `README.md` | This file. |

---

## 🎯 Objective

- Inspect the structure and quality of the dataset (shape, types, missing values, duplicates).
- Clean the data and document every cleaning decision.
- Compute descriptive statistics for numerical and categorical features.
- Explore relationships through univariate, bivariate, and multivariate analysis.
- Identify outliers and correlations, especially around car **price**.

---

## 📊 Dataset Overview

- **Rows (raw):** 208
- **Columns:** 26
- **Rows after removing duplicates:** 205
- **Target/focus variable:** `price`

### Data Dictionary

| Column | Type | Definition |
|---|---|---|
| `car_ID` | int | Unique identifier for each listing/row. |
| `symboling` | int | Insurance risk rating, from -3 (safe) to +3 (risky); assigned based on how risky the car is to insure relative to its price. |
| `CarName` | text | Manufacturer and model name (e.g. "toyota corolla"). |
| `fueltype` | category | Type of fuel the car uses — `gas` or `diesel`. |
| `aspiration` | category | Engine aspiration type — `std` (naturally aspirated) or `turbo` (turbocharged). |
| `doornumber` | category | Number of doors — `two` or `four`. |
| `carbody` | category | Body style — e.g. `sedan`, `hatchback`, `wagon`, `hardtop`, `convertible`. |
| `drivewheel` | category | Drive configuration — `fwd` (front-wheel), `rwd` (rear-wheel), `4wd` (four-wheel). |
| `enginelocation` | category | Position of the engine — `front` or `rear`. |
| `wheelbase` | float | Distance between the front and rear axles (inches). |
| `carlength` | float | Overall length of the car (inches). |
| `carwidth` | float | Overall width of the car (inches). |
| `carheight` | float | Overall height of the car (inches). |
| `curbweight` | int | Weight of the car without occupants or cargo (pounds). |
| `enginetype` | category | Engine design — e.g. `dohc`, `ohc`, `ohcv`, `rotor`. |
| `cylindernumber` | category | Number of cylinders, written as a word (e.g. `four`, `six`, `eight`). |
| `enginesize` | float | Engine displacement (cubic inches) — larger generally means more power. |
| `fuelsystem` | category | Fuel delivery system — e.g. `mpfi` (multi-point fuel injection), `2bbl` (2-barrel carburetor). |
| `boreratio` | float | Bore diameter of the engine cylinder (inches). |
| `stroke` | float | Piston stroke length (inches). |
| `compressionratio` | float | Ratio of cylinder volume at the bottom vs. top of the piston stroke — higher generally means more efficient combustion. |
| `horsepower` | float | Engine power output (horsepower). |
| `peakrpm` | int | Engine speed (RPM) at which peak horsepower is produced. |
| `citympg` | int | Fuel efficiency in city driving (miles per gallon). |
| `highwaympg` | int | Fuel efficiency in highway driving (miles per gallon). |
| `price` | float | Selling price of the car (USD) — the main variable of interest for this analysis. |

> **Note:** `symboling`, `boreratio`, `stroke`, and `compressionratio` are technical
> engineering fields — keep an eye on these if a chart or stat involving them looks
> unintuitive, since they're less commonly discussed than horsepower/price/mpg.

---

## 🧹 Data Cleaning Summary

| Step | Before | After | Notes |
|---|---|---|---|
| Duplicate rows | 208 rows | 205 rows | 3 fully duplicated rows were dropped. |
| Missing values | 4 cells missing across `fueltype`, `enginesize`, `horsepower`, `price` | 0 missing | See handling below. |

**Missing value handling:**
- **Numerical columns** (`horsepower`, `price`, `enginesize`) → filled with the **median** of
  each column, to avoid distortion from outliers/skew.
- **Categorical column** (`fueltype`) → filled with the **mode** (most frequent value).

---

## 🔍 EDA Workflow

The notebook follows this structure, in order:

1. **Setup** — import libraries (`pandas`, `numpy`, `matplotlib`, `seaborn`).
2. **Load & Inspect** — shape, column list, `.info()`, `.describe()`.
3. **Data Quality Check** — missing values (count + %), duplicate rows, categorical
   consistency (`value_counts()` per column).
4. **Cleaning** — drop duplicates, impute missing values (median/mode), record
   before/after row counts.
5. **Descriptive Statistics** — summary stats for numerical and categorical columns;
   price-specific stats (mean, median, min, max, std).
6. **Univariate Analysis**
   - Histogram — distribution of `price`
   - Count plot — cars by `fueltype`
   - Histogram — distribution of `horsepower`
7. **Bivariate Analysis**
   - Scatter plot — `horsepower` vs. `price`
   - Scatter plot — `enginesize` vs. `price`
   - Box plot — `price` distribution by `fueltype`
8. **Multivariate Analysis**
   - Correlation heatmap across all numerical columns
9. **Outlier Analysis**
   - Box plot — `price` outliers

---

## 📈 Chart Types Used

Histogram · Count Plot · Scatter Plot · Box Plot · Correlation Heatmap
*(5 distinct chart types, 8 charts total)*

---

## 🛠️ How to Run

1. Clone this repository:
   ```bash
   git clone <your-repo-url>
   cd <your-repo-folder>
   ```
2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn
   ```
3. Open the notebook in Jupyter or Google Colab:
   ```bash
   jupyter notebook Mayank_L_Surana_Cars_EDA_Project2.ipynb
   ```
4. If running in **Google Colab**, the second cell uses `files.upload()` to upload
   `Cars_Dataset.csv` manually. To run locally instead, replace that upload step with:
   ```python
   df = pd.read_csv("Cars_Dataset.csv")
   ```

---

## ✅ Suggested Next Steps *(not yet in the notebook — worth adding)*

- [ ] Add a written **"Key Findings"** section summarizing what each chart shows (e.g. how
  strongly `horsepower` and `enginesize` correlate with `price`).
- [ ] Note any **limitations** of the dataset (small sample size, no listing date, U.S.-market
  specs only, etc.).
- [ ] Consider whether the 3 duplicate rows and 1 row of missing data meaningfully change
  results, given the dataset is only 205–208 rows.

---

## 👤 Author

**Mayank L. Surana**

## 📄 License

Add a license of your choice (e.g. MIT) if this repository is public.
