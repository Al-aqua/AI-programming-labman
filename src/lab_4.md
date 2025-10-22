# Lab 4: Central Tendency & Distribution Analysis

## Objectives

- Analyze data distribution characteristics and variation
- Calculate and interpret standard deviation and variance
- Compute percentiles, z-scores, and other distribution metrics
- Understand skewness and kurtosis for data shape analysis
- Visualize distributions using histograms, box plots, and density plots
- Prepare data for machine learning through normalization and scaling
- Build foundation for advanced statistical analysis

## Tools and Resources

- **Tools**
  - [Python](https://www.python.org/)
  - [Jupyter Notebook](https://jupyter.org/) or [Visual Studio Code](https://code.visualstudio.com/)
  - [Pandas](https://pandas.pydata.org/)
  - [Matplotlib](https://matplotlib.org/)
  - [Seaborn](https://seaborn.pydata.org/)
  - [SciPy](https://scipy.org/)
  - [Scikit-learn](https://scikit-learn.org/)

- **Resources**
  - [Seaborn Distribution Plots](https://seaborn.pydata.org/tutorial/distributions.html)
  - [Understanding Skewness and Kurtosis in Statistics](https://www.tutorialspoint.com/seaborn/seaborn_kernel_density_estimates.htm)
  - [Z-Score Normalization Tutorial](https://spotintelligence.com/2025/02/14/z-score-normalization/)
  - [Data Normalization with Scikit-Learn](https://scikit-learn.org/stable/modules/preprocessing.html)
  - [Matplotlib Distribution Visualization](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.hist.html)

## Content

### 1. Understanding Data Distribution

Data distribution describes how values are spread across a dataset. Understanding the shape, center, and spread of distributions is fundamental for effective data analysis and modeling.

#### 1.1 Code Example

```python
import pandas as pd
import numpy as np

# Sample datasets with different distributions
data = {
    "StudentID": range(1, 101),
    "MathScore": np.random.normal(75, 12, 100),
    "EnglishScore": np.random.normal(72, 15, 100),
    "Science": np.random.exponential(2) * 25 + 50,  # Right-skewed
}
df = pd.DataFrame(data)

print("Dataset Overview:")
print(df.head(10))
print("----------------------------")

# Basic distribution statistics
print("Math Score Statistics:")
print(f"Mean: {df['MathScore'].mean():.2f}")
print(f"Median: {df['MathScore'].median():.2f}")
print(f"Std Dev: {df['MathScore'].std():.2f}")
print(f"Min: {df['MathScore'].min():.2f}")
print(f"Max: {df['MathScore'].max():.2f}")
print("----------------------------")

# Compare distributions
print("Distribution Comparison:")
print(df[["MathScore", "EnglishScore", "Science"]].describe())
```

**Explanation:**

- Distribution analysis involves examining how data points are spread across a range
- `describe()` provides a quick overview of central tendency and spread
- Different subjects may have different distribution patterns
- Understanding these patterns helps identify data characteristics

#### 1.2 Exercise

1. Load a dataset with at least 3 numeric columns
2. Calculate mean, median, standard deviation for each column
3. Compare the distributions using `describe()`
4. Identify which subject has the most consistent scores (lowest std dev)

---

### 2. Variance and Standard Deviation

Variance measures the average squared deviation from the mean, while standard deviation is its square root. These metrics quantify data spread.

#### 2.1 Code Example

```python
import pandas as pd

# Sample data: Test scores from three classes
data = {
    "Class_A": [78, 82, 85, 88, 90, 78, 80, 86, 84, 82],
    "Class_B": [60, 95, 75, 88, 70, 85, 65, 92, 78, 82],
    "Class_C": [80, 81, 82, 83, 84, 79, 80, 81, 82, 83],
}
df = pd.DataFrame(data)

print("Test Scores by Class:")
print(df)
print("----------------------------")

# Calculate variance and standard deviation
print("Variance Analysis:")
print(f"Class A Variance: {df['Class_A'].var():.2f}")
print(f"Class B Variance: {df['Class_B'].var():.2f}")
print(f"Class C Variance: {df['Class_C'].var():.2f}")
print("----------------------------")

print("Standard Deviation Analysis:")
print(f"Class A Std Dev: {df['Class_A'].std():.2f}")
print(f"Class B Std Dev: {df['Class_B'].std():.2f}")
print(f"Class C Std Dev: {df['Class_C'].std():.2f}")
print("----------------------------")

# Mean comparison
print("Mean Scores:")
print(f"Class A Mean: {df['Class_A'].mean():.2f}")
print(f"Class B Mean: {df['Class_B'].mean():.2f}")
print(f"Class C Mean: {df['Class_C'].mean():.2f}")
print("----------------------------")

# Coefficient of Variation (Std Dev / Mean)
print("Coefficient of Variation (Relative Spread):")
cv_a = df['Class_A'].std() / df['Class_A'].mean()
cv_b = df['Class_B'].std() / df['Class_B'].mean()
cv_c = df['Class_C'].std() / df['Class_C'].mean()
print(f"Class A CV: {cv_a:.3f}")
print(f"Class B CV: {cv_b:.3f}")
print(f"Class C CV: {cv_c:.3f}")
```

**Explanation:**

- **Variance**: Average squared distance from mean (units are squared)
- **Standard Deviation**: Square root of variance (same units as data)
- **Coefficient of Variation**: Relative measure, useful for comparing variability across different scales
- Higher std dev indicates more spread in data

#### 2.2 Exercise

1. Create three datasets with the same mean but different standard deviations
2. Calculate variance and standard deviation for each
3. Compare coefficient of variation across datasets
4. Visualize the differences using histograms

---

### 3. Z-Scores and Data Normalization

Z-scores standardize data by transforming it to have a mean of 0 and standard deviation of 1, enabling fair comparison across different scales.

#### 3.1 Code Example

```python
import pandas as pd
from sklearn.preprocessing import StandardScaler

# Data with different scales: salary (thousands), age (years)
data = {
    "Salary": [45, 52, 48, 65, 72, 55, 68, 70, 58, 75],
    "Age": [28, 35, 30, 45, 40, 32, 50, 48, 38, 55],
    "Experience": [2, 8, 5, 15, 18, 7, 20, 16, 10, 22],
}
df = pd.DataFrame(data)

print("Original Data:")
print(df)
print("----------------------------")

# Manual Z-score calculation
print("Manual Z-Score Calculation:")
salary_mean = df['Salary'].mean()
salary_std = df['Salary'].std()

df['Salary_ZScore'] = (df['Salary'] - salary_mean) / salary_std
print("Salary Z-Scores:")
print(df[["Salary", "Salary_ZScore"]])
print("----------------------------")

# Using Scikit-learn StandardScaler
print("Using StandardScaler:")
scaler = StandardScaler()
df_scaled = pd.DataFrame(
    scaler.fit_transform(df[["Salary", "Age", "Experience"]]),
    columns=["Salary_Scaled", "Age_Scaled", "Experience_Scaled"]
)
print(df_scaled)
print("----------------------------")

# Verify scaling properties
print("Verification (should be ~0 and ~1):")
print(f"Mean of Salary_Scaled: {df_scaled['Salary_Scaled'].mean():.6f}")
print(f"Std of Salary_Scaled: {df_scaled['Salary_Scaled'].std():.6f}")
print("----------------------------")

# Identifying outliers using Z-scores
print("Outlier Detection (|Z-Score| > 3):")
outliers = df[abs(df['Salary_ZScore']) > 3]
print(outliers if not outliers.empty else "No outliers detected")
```

**Explanation:**

- **Z-Score Formula**: \( z = \frac{x - \mu}{\sigma} \)
- Z-score of 0 means at the mean; ±1 means 1 standard deviation away
- Enables comparison of variables on different scales
- Outliers typically have |z-score| > 3
- StandardScaler from Scikit-learn simplifies the process

#### 3.2 Exercise

1. Load employee data with salary, years of experience, and age
2. Calculate Z-scores for each numeric column
3. Identify employees with Z-scores beyond ±2
4. Verify that scaled data has mean ≈ 0 and std ≈ 1

---

### 4. Skewness and Kurtosis

Skewness measures asymmetry in distribution; kurtosis measures the tailedness and peakedness compared to a normal distribution.

#### 4.1 Code Example

```python
import pandas as pd
import numpy as np
from scipy.stats import skew, kurtosis

# Create datasets with different distribution shapes
np.random.seed(42)
data = {
    "Symmetric": np.random.normal(100, 15, 1000),
    "Right_Skewed": np.random.exponential(2) * 30 + 50,
    "Left_Skewed": 150 - np.random.exponential(2) * 30,
}
df = pd.DataFrame(data)

print("Distribution Shapes:")
print("----------------------------")

# Calculate skewness for each distribution
print("Skewness Analysis:")
for col in df.columns:
    skewness_val = skew(df[col])
    print(f"{col} Skewness: {skewness_val:.3f}")
    if skewness_val < -0.5:
        shape = "Left-skewed"
    elif skewness_val > 0.5:
        shape = "Right-skewed"
    else:
        shape = "Approximately symmetric"
    print(f"  → {shape}")
print("----------------------------")

# Calculate kurtosis for each distribution
print("Kurtosis Analysis:")
for col in df.columns:
    kurt_val = kurtosis(df[col])
    print(f"{col} Kurtosis: {kurt_val:.3f}")
    if kurt_val > 0.5:
        tail = "Heavy tails (Leptokurtic)"
    elif kurt_val < -0.5:
        tail = "Light tails (Platykurtic)"
    else:
        tail = "Normal-like tails (Mesokurtic)"
    print(f"  → {tail}")
print("----------------------------")

# Summary statistics with skewness and kurtosis
print("Complete Distribution Summary:")
summary = df.describe().T
summary['Skewness'] = df.skew()
summary['Kurtosis'] = df.kurtosis()
print(summary)
```

**Explanation:**

- **Skewness**:
  - Positive: Right tail is longer (right-skewed)
  - Negative: Left tail is longer (left-skewed)
  - Near 0: Symmetric distribution
- **Kurtosis**:
  - Positive: Heavy tails, more outliers (leptokurtic)
  - Negative: Light tails, fewer outliers (platykurtic)
  - Near 0: Similar to normal distribution (mesokurtic)
- Important for assessing normality assumptions in statistical tests

#### 4.2 Exercise

1. Generate three datasets: one normal, one right-skewed, one left-skewed
2. Calculate skewness and kurtosis for each
3. Interpret the results
4. Visualize all three distributions

---

### 5. Distribution Visualization

Visual representation of distributions helps identify patterns, outliers, and normality.

#### 5.1 Code Example

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Load or create sample data
np.random.seed(42)
data = {
    "Age": np.random.normal(35, 10, 500),
    "Salary": np.concatenate([
        np.random.normal(50000, 10000, 300),
        np.random.normal(80000, 20000, 200)
    ]),
    "Hours_Worked": np.random.exponential(5) * 8,
}
df = pd.DataFrame(data)

# Set Seaborn style
sns.set_style("whitegrid")

# 1. Histogram with KDE (Kernel Density Estimate)
fig, axes = plt.subplots(1, 3, figsize=(15, 5))

for idx, col in enumerate(["Age", "Salary", "Hours_Worked"]):
    sns.histplot(data=df, x=col, kde=True, bins=30, ax=axes[idx],
                 color="skyblue", edgecolor="black")
    axes[idx].set_title(f"Distribution of {col}", fontsize=12,
                        fontweight="bold")
    axes[idx].set_ylabel("Frequency")

plt.tight_layout()
plt.show()
print("Histograms with KDE curves created")
print("----------------------------")

# 2. Box Plots for outlier detection
fig, axes = plt.subplots(1, 3, figsize=(15, 5))

for idx, col in enumerate(["Age", "Salary", "Hours_Worked"]):
    sns.boxplot(data=df, y=col, ax=axes[idx], color="lightgreen")
    axes[idx].set_title(f"Box Plot: {col}", fontsize=12,
                        fontweight="bold")

plt.tight_layout()
plt.show()
print("Box plots created")
print("----------------------------")

# 3. Q-Q Plot for normality assessment
from scipy import stats

fig, axes = plt.subplots(1, 3, figsize=(15, 5))

for idx, col in enumerate(["Age", "Salary", "Hours_Worked"]):
    stats.probplot(df[col], dist="norm", plot=axes[idx])
    axes[idx].set_title(f"Q-Q Plot: {col}", fontsize=12,
                        fontweight="bold")
    axes[idx].grid(True, alpha=0.3)

plt.tight_layout()
plt.show()
print("Q-Q plots created")
```

**Explanation:**

- **Histogram + KDE**: Shows frequency distribution with smooth density curve
- **Box Plot**: Displays quartiles, median, and outliers
  - Box: Q1 to Q3 (middle 50%)
  - Line in box: Median (Q2)
  - Whiskers: Extend to 1.5×IQR
  - Dots: Outliers beyond whiskers
- **Q-Q Plot**: Compares data distribution to normal distribution
  - Points close to diagonal line indicate normality
  - Deviations suggest non-normal distribution

#### 5.2 Exercise

1. Load the `students.csv` file
2. Create histograms with KDE for 3+ numeric columns
3. Generate box plots to identify outliers
4. Create Q-Q plots to assess normality
5. Interpret findings for each variable

---

### 6. Comparing Distributions

Comparing multiple distributions helps identify differences in central tendency, spread, and shape.

#### 6.1 Code Example

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Data: Test scores by subject and gender
np.random.seed(42)
data = {
    "Subject": ["Math"]*100 + ["Science"]*100 + ["English"]*100,
    "Score": np.concatenate([
        np.random.normal(75, 12, 100),
        np.random.normal(78, 10, 100),
        np.random.normal(72, 15, 100)
    ]),
    "Gender": ["Male", "Female"] * 150,
}
df = pd.DataFrame(data)

print("Data Overview:")
print(df.groupby("Subject")["Score"].describe())
print("----------------------------")

# Violin plot: Shows full distribution shape
plt.figure(figsize=(12, 5))
sns.violinplot(data=df, x="Subject", y="Score", hue="Gender",
               split=False, palette="Set2")
plt.title("Score Distribution by Subject and Gender", fontsize=14,
          fontweight="bold")
plt.ylabel("Score")
plt.show()
print("Violin plot created")
print("----------------------------")

# Strip plot overlay
plt.figure(figsize=(12, 5))
sns.violinplot(data=df, x="Subject", y="Score", hue="Gender",
               palette="Set2")
sns.stripplot(data=df, x="Subject", y="Score", hue="Gender",
              color="black", alpha=0.3, size=4)
plt.title("Distribution with Individual Points", fontsize=14,
          fontweight="bold")
plt.ylabel("Score")
plt.show()
print("Violin plot with overlay created")
print("----------------------------")

# Statistical comparison
print("Statistical Comparison:")
for subject in ["Math", "Science", "English"]:
    subject_data = df[df["Subject"] == subject]["Score"]
    print(f"\n{subject}:")
    print(f"  Mean: {subject_data.mean():.2f}")
    print(f"  Median: {subject_data.median():.2f}")
    print(f"  Std Dev: {subject_data.std():.2f}")
    print(f"  Q1: {subject_data.quantile(0.25):.2f}")
    print(f"  Q3: {subject_data.quantile(0.75):.2f}")
```

**Explanation:**

- **Violin Plot**: Combines distribution shape with statistical summary
- Shows density across full range of values
- Useful for comparing multiple groups
- Can separate by categories using `hue` parameter
- Strip plot overlay shows individual data points

#### 6.2 Exercise

1. Load employee data with salary by department
2. Create violin plots comparing salary distributions
3. Generate box plots with individual points
4. Calculate statistics for each department
5. Identify departments with highest variability

---

## Summary

You now understand:

- How to analyze data distribution characteristics
- Calculating and interpreting variance and standard deviation
- Computing z-scores for data standardization
- Measuring skewness and kurtosis for distribution shape
- Creating and interpreting distribution visualizations
- Comparing multiple distributions for insights
- Preparing data for machine learning through normalization
- Identifying outliers and assessing normality

These skills enable you to characterize data distributions, identify patterns and anomalies, and prepare data for advanced statistical analysis and machine learning!

## Up Next

In Lab 5, you'll master advanced data visualization techniques including heatmaps, correlation matrices, and interactive dashboards to communicate insights effectively.
