# Lab 3: Data Summaries & Descriptive Statistics

## Objectives

- Calculate and interpret fundamental statistical measures
- Understand measures of central tendency and spread
- Compute percentiles, ranges, and quartiles
- Apply descriptive statistics to real datasets
- Build foundation for advanced statistical analysis

## Tools and Resources

- **Tools**
  - [Python](https://www.python.org/)
  - [Jupyter Notebook](https://jupyter.org/) or [Visual Studio Code](https://code.visualstudio.com/)
  - [Pandas](https://pandas.pydata.org/)

- **Resources**
  - [Pandas: How to calculate summary statistics](https://pandas.pydata.org/docs/getting_started/intro_tutorials/06_calculate_statistics.html) - Official Pandas tutorial with real-world examples
  - [GeeksforGeeks: Descriptive Statistics in Pandas](https://www.geeksforgeeks.org/python/how-to-get-the-descriptive-statistics-for-pandas-dataframe/) - Practical examples with detailed explanations
  - [NumPy Statistical Functions](https://www.tutorialspoint.com/numpy/numpy_statistical_functions.htm) - Comprehensive coverage of statistical calculations
  - [Towards Data Science: Hidden Gems in NumPy](https://towardsdatascience.com/hidden-gems-in-numpy-7-functions-every-data-scientist-should-know/) - Advanced statistical functions guide

## Content

### 1. Introduction to Descriptive Statistics

Descriptive statistics summarize and describe data characteristics. They help identify patterns, trends, and anomalies in datasets.

#### 1.1 Code Example

```python
import pandas as pd

# Sample dataset
data = {
    "StudentID": [101, 102, 103, 104, 105, 106, 107, 108],
    "Name": ["Ahmed", "Fatima", "Ali", "Layla", "Hassan", "Noor",
             "Mariam", "Omar"],
    "Math": [85, 90, 78, 92, 88, 76, 91, 84],
    "Science": [88, 87, 92, 85, 90, 80, 89, 86],
    "English": [80, 95, 85, 90, 82, 79, 93, 88],
}
df = pd.DataFrame(data)
print("Student Dataset:")
print(df)
print("----------------------------")

# Quick overview using describe()
print("Descriptive Statistics Summary:")
print(df[["Math", "Science", "English"]].describe())
print("----------------------------")

# Statistical methods
print("Mean (Average):")
print(df[["Math", "Science", "English"]].mean())
print("----------------------------")

print("Median (Middle Value):")
print(df[["Math", "Science", "English"]].median())
print("----------------------------")

print("Mode (Most Frequent):")
print(df[["Math", "Science", "English"]].mode())
print("----------------------------")

print("Standard Deviation:")
print(df[["Math", "Science", "English"]].std())
print("----------------------------")

print("Variance:")
print(df[["Math", "Science", "English"]].var())
```

**Explanation:**

- `describe()`: Provides count, mean, std, min, 25%, 50%, 75%, max
- `mean()`: Average value (sum ÷ count)
- `median()`: Middle value when sorted
- `mode()`: Most frequently occurring value
- `std()`: Standard deviation (spread from mean)
- `var()`: Variance (squared standard deviation)

---

### 2. Measures of Central Tendency

Central tendency describes the center point of a dataset using mean, median, and mode.

#### 2.1 Code Example

```python
import pandas as pd

# Sample salary data
salaries = {
    "Department": ["IT", "IT", "IT", "IT", "IT", "HR", "HR", "HR",
                   "Finance", "Finance"],
    "Salary": [3000, 3200, 3500, 3800, 50000, 2800, 2900, 3000,
               4000, 4500],
}
df = pd.DataFrame(salaries)

print("Salary Data:")
print(df)
print("----------------------------")

# Calculate central tendency for overall salaries
print("Overall Salary Statistics:")
print(f"Mean: ${df['Salary'].mean():.2f}")
print(f"Median: ${df['Salary'].median():.2f}")
print(f"Mode: ${df['Salary'].mode().values[0]:.2f}")
print("----------------------------")

# Central tendency by department
print("Mean Salary by Department:")
print(df.groupby("Department")["Salary"].mean())
print("----------------------------")

print("Median Salary by Department:")
print(df.groupby("Department")["Salary"].median())
print("----------------------------")

# Understanding impact of outliers
print("Impact of Outlier (50000):")
print(f"Mean with outlier: ${df['Salary'].mean():.2f}")
salaries_no_outlier = df[df["Salary"] < 10000]["Salary"]
print(f"Mean without outlier: ${salaries_no_outlier.mean():.2f}")
print(f"Median is stable: ${df['Salary'].median():.2f}")
print("(Median is robust to outliers)")
```

**Explanation:**

- **Mean**: Sum of all values ÷ count (affected by outliers)
- **Median**: Middle value when sorted (robust to outliers)
- **Mode**: Most frequently occurring value (useful for categorical data)
- Median is preferred when outliers exist

---

### 3. Measures of Spread (Dispersion)

Spread describes how data is distributed around the center using range, variance, and standard deviation.

#### 3.1 Code Example

```python
import pandas as pd

# Sample test scores from two classes
data = {
    "ClassA": [75, 76, 77, 78, 79, 80, 81, 82, 83, 84],
    "ClassB": [45, 55, 60, 75, 80, 85, 90, 95, 98, 100],
}
df = pd.DataFrame(data)

print("Test Scores Comparison:")
print(df)
print("----------------------------")

# Range (Max - Min)
print("Range (Max - Min):")
print(f"ClassA Range: {df['ClassA'].max() - df['ClassA'].min()}")
print(f"ClassB Range: {df['ClassB'].max() - df['ClassB'].min()}")
print("----------------------------")

# Min and Max
print("Min and Max Values:")
print(f"ClassA: Min={df['ClassA'].min()}, Max={df['ClassA'].max()}")
print(f"ClassB: Min={df['ClassB'].min()}, Max={df['ClassB'].max()}")
print("----------------------------")

# Variance (average squared deviation from mean)
print("Variance:")
print(f"ClassA Variance: {df['ClassA'].var():.2f}")
print(f"ClassB Variance: {df['ClassB'].var():.2f}")
print("----------------------------")

# Standard Deviation (square root of variance)
print("Standard Deviation:")
print(f"ClassA Std Dev: {df['ClassA'].std():.2f}")
print(f"ClassB Std Dev: {df['ClassB'].std():.2f}")
print("----------------------------")

# Mean and relationship to std dev
print("Mean and Std Dev:")
print(f"ClassA Mean: {df['ClassA'].mean():.2f}, "
      f"Std Dev: {df['ClassA'].std():.2f}")
print(f"ClassB Mean: {df['ClassB'].mean():.2f}, "
      f"Std Dev: {df['ClassB'].std():.2f}")
print("(Both have similar means but different spreads)")
print("----------------------------")

# Interquartile Range (Q3 - Q1)
print("Interquartile Range (IQR):")
q1_a = df['ClassA'].quantile(0.25)
q3_a = df['ClassA'].quantile(0.75)
print(f"ClassA IQR: {q3_a - q1_a:.2f}")

q1_b = df['ClassB'].quantile(0.25)
q3_b = df['ClassB'].quantile(0.75)
print(f"ClassB IQR: {q3_b - q1_b:.2f}")
```

**Explanation:**

- **Range**: Max - Min (simple measure, affected by outliers)
- **Variance**: Average squared deviation from mean
- **Standard Deviation**: Square root of variance (same units as data)
- **IQR**: Q3 - Q1 (middle 50% of data, robust to outliers)

---

### 4. Percentiles and Quartiles

Percentiles divide data into 100 parts; quartiles divide into 4 parts.

#### 4.1 Code Example

```python
import pandas as pd

# Sample exam scores
scores = {
    "StudentID": range(1, 21),
    "Score": [45, 52, 58, 61, 65, 68, 72, 75, 78, 80,
              82, 84, 85, 87, 89, 90, 91, 93, 95, 98],
}
df = pd.DataFrame(scores)

print("Exam Scores:")
print(df)
print("----------------------------")

# Common percentiles
print("Percentiles:")
print(f"25th Percentile (Q1): {df['Score'].quantile(0.25)}")
print(f"50th Percentile (Q2/Median): {df['Score'].quantile(0.50)}")
print(f"75th Percentile (Q3): {df['Score'].quantile(0.75)}")
print(f"90th Percentile: {df['Score'].quantile(0.90)}")
print(f"95th Percentile: {df['Score'].quantile(0.95)}")
print("----------------------------")

# Quartiles breakdown
q1 = df['Score'].quantile(0.25)
q2 = df['Score'].quantile(0.50)
q3 = df['Score'].quantile(0.75)

print("Quartile Breakdown:")
print(f"Bottom 25% (below Q1={q1:.1f}):")
print(df[df['Score'] < q1]['Score'].values)
print(f"\nMiddle 25-50% (Q1={q1:.1f} to Q2={q2:.1f}):")
print(df[(df['Score'] >= q1) & (df['Score'] < q2)]['Score'].values)
print(f"\nMiddle 50-75% (Q2={q2:.1f} to Q3={q3:.1f}):")
print(df[(df['Score'] >= q2) & (df['Score'] < q3)]['Score'].values)
print(f"\nTop 25% (above Q3={q3:.1f}):")
print(df[df['Score'] >= q3]['Score'].values)
print("----------------------------")

# Multiple percentiles at once
percentiles = [10, 25, 50, 75, 90]
print("Multiple Percentiles:")
for p in percentiles:
    value = df['Score'].quantile(p / 100)
    print(f"{p}th Percentile: {value:.1f}")
print("----------------------------")

# Finding students above a percentile threshold
threshold_90 = df['Score'].quantile(0.90)
print(f"Students scoring above 90th percentile ({threshold_90:.1f}):")
print(df[df['Score'] > threshold_90])
```

**Explanation:**

- **Percentile**: Value below which a percentage of data falls
- **Quartile**: Special percentiles (25%, 50%, 75%)
- Q1 (25th): 25% of data below this value
- Q2 (50th): Median—50% of data below this value
- Q3 (75th): 75% of data below this value
- **IQR** = Q3 - Q1 (middle 50% of data)

---

### 5. Summary Statistics and Data Profiles

Generate comprehensive statistical summaries for datasets.

#### 5.1 Code Example

```python
import pandas as pd

# Sample e-commerce data
data = {
    "OrderID": range(1001, 1011),
    "ProductCategory": ["Electronics", "Clothing", "Electronics",
                        "Books", "Clothing", "Electronics", "Books",
                        "Clothing", "Electronics", "Books"],
    "OrderAmount": [250, 45, 320, 25, 60, 180, 35, 55, 290, 40],
    "CustomerAge": [28, 35, 42, 55, 31, 26, 48, 37, 33, 52],
}
df = pd.DataFrame(data)

print("E-Commerce Dataset:")
print(df)
print("----------------------------")

# Overall summary statistics
print("Overall Statistics:")
print(df.describe())
print("----------------------------")

# Statistics by category
print("Order Amount Statistics by Category:")
print(df.groupby("ProductCategory")["OrderAmount"].describe())
print("----------------------------")

# Custom statistics function
def summary_stats(series):
    return pd.Series({
        'Count': series.count(),
        'Mean': series.mean(),
        'Median': series.median(),
        'Std Dev': series.std(),
        'Min': series.min(),
        'Max': series.max(),
        'Q1': series.quantile(0.25),
        'Q3': series.quantile(0.75),
        'IQR': series.quantile(0.75) - series.quantile(0.25),
    })

print("Custom Summary Statistics:")
print(summary_stats(df["OrderAmount"]))
print("----------------------------")

# Statistics by multiple groupings
print("Order Amount by Category and Age Group:")
df["AgeGroup"] = pd.cut(df["CustomerAge"],
                        bins=[0, 35, 50, 100],
                        labels=["Young", "Middle", "Senior"])
print(df.groupby(["ProductCategory", "AgeGroup"])
  ["OrderAmount"].agg(['count', 'mean', 'std']))
print("----------------------------")

# Correlation between numeric columns
print("Correlation Analysis:")
print(df[["OrderAmount", "CustomerAge"]].corr())
```

**Explanation:**

- `describe()`: Automatic summary statistics
- `agg()`: Apply multiple aggregation functions
- Custom functions for domain-specific summaries
- `groupby()`: Statistics for subsets
- `corr()`: Relationship between variables

---

### 6. Identifying Outliers and Anomalies

Detect unusual values that may indicate errors or special cases.

#### 6.1 Code Example

```python
import pandas as pd

# Sample data with outliers
data = {
    "Day": range(1, 16),
    "DailySales": [100, 105, 103, 102, 104, 103, 102, 500, 101,
                   104, 102, 103, 105, 104, 103],
}
df = pd.DataFrame(data)

print("Daily Sales Data:")
print(df)
print("----------------------------")

# Method 1: IQR method
q1 = df['DailySales'].quantile(0.25)
q3 = df['DailySales'].quantile(0.75)
iqr = q3 - q1

lower_bound = q1 - 1.5 * iqr
upper_bound = q3 + 1.5 * iqr

print("IQR Method:")
print(f"Q1: {q1}, Q3: {q3}, IQR: {iqr}")
print(f"Lower Bound: {lower_bound}, Upper Bound: {upper_bound}")
print("----------------------------")

outliers_iqr = df[(df['DailySales'] < lower_bound) |
                  (df['DailySales'] > upper_bound)]
print("Outliers (IQR Method):")
print(outliers_iqr)
print("----------------------------")

# Method 2: Z-score method
mean = df['DailySales'].mean()
std = df['DailySales'].std()

df['ZScore'] = (df['DailySales'] - mean) / std

print("Z-Score Method:")
print(f"Mean: {mean:.2f}, Std Dev: {std:.2f}")
print(df[['Day', 'DailySales', 'ZScore']])
print("----------------------------")

outliers_zscore = df[df['ZScore'].abs() > 3]
print("Outliers (Z-Score > 3):")
print(outliers_zscore)
print("----------------------------")

# Statistics with and without outliers
print("Impact of Outlier:")
print(f"Mean with outlier: {df['DailySales'].mean():.2f}")
print(f"Mean without outlier: "
      f"{df[df['DailySales'] < 200]['DailySales'].mean():.2f}")
print(f"Median (stable): {df['DailySales'].median():.2f}")
```

**Explanation:**

- **IQR Method**: Outliers beyond Q1 - 1.5×IQR or Q3 + 1.5×IQR
- **Z-Score Method**: Outliers with |z| > 3 (3 standard deviations)
- **Impact**: Outliers distort mean but not median
- **Action**: Investigate, clean, or handle appropriately

---

## Summary

You now understand:

- Calculating mean, median, and mode for central tendency
- Using variance and standard deviation to measure spread
- Computing percentiles and quartiles for data distribution
- Generating comprehensive statistical summaries
- Detecting outliers using IQR and Z-score methods
- Applying statistics to real datasets with grouping and aggregation

These skills enable you to extract meaningful insights from data and prepare datasets for machine learning!

## Up Next

In Lab 4, you'll explore distribution analysis and visualize how data is spread across ranges using advanced statistical techniques.
