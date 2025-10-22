# Lab 5: Data Visualization Techniques

## Objectives

- Create effective data visualizations using Matplotlib and Seaborn
- Master line charts, bar graphs, histograms, and scatter plots
- Develop skills in visualization customization and styling
- Learn best practices for communicating insights through visual data
- Build foundation for advanced dashboards and interactive visualizations
- Create compelling charts that drive business insights

## Tools and Resources

- **Tools**
  - [Python](https://www.python.org/)
  - [Jupyter Notebook](https://jupyter.org/) or [Visual Studio Code](https://code.visualstudio.com/)
  - [Pandas](https://pandas.pydata.org/)
  - [Matplotlib](https://matplotlib.org/)
  - [Seaborn](https://seaborn.pydata.org/)

- **Resources**
  - [Matplotlib Official Documentation](https://matplotlib.org/stable/index.html)
  - [Seaborn Tutorial: Plotting with Categorical Data](https://seaborn.pydata.org/tutorial/categorical.html)
  - [Top Data Visualization Best Practices](https://moldstud.com/articles/p-top-data-visualization-best-practices-tips-for-matplotlib-and-seaborn)
  - [Matplotlib Color Maps Reference](https://matplotlib.org/stable/tutorials/colors/colormaps.html)
  - [Data Storytelling Guide](https://www.interaction-design.org/literature/topics/data-storytelling)
  - [Kaggle Datasets for Practice](https://www.kaggle.com/datasets)

## Content

### 1. Introduction to Data Visualization Principles

Effective data visualization transforms complex data into accessible insights. A well-designed chart tells a story, guides viewers' attention, and enables informed decision-making. Key principles include clarity, accuracy, and accessibility.

#### 1.1 Code Example

```python
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd

# Set up visualization style
sns.set_style("whitegrid")
sns.set_palette("husl")

# Sample dataset: Monthly sales by product
data = {
    "Month": ["Jan", "Feb", "Mar", "Apr", "May", "Jun"],
    "Product_A": [15000, 18000, 22000, 25000, 28000, 31000],
    "Product_B": [12000, 14000, 16000, 18000, 20000, 22000],
    "Product_C": [10000, 12000, 14000, 13000, 15000, 18000],
}
df = pd.DataFrame(data)

print("Sales Dataset:")
print(df)
print("----------------------------")

# Basic line plot
plt.figure(figsize=(12, 6))
for col in ["Product_A", "Product_B", "Product_C"]:
    plt.plot(df["Month"], df[col], marker="o", linewidth=2,
             label=col, markersize=8)

plt.title("Monthly Sales Trends by Product", fontsize=14,
          fontweight="bold")
plt.xlabel("Month", fontsize=12)
plt.ylabel("Sales ($)", fontsize=12)
plt.legend(loc="best")
plt.grid(True, alpha=0.3)
plt.tight_layout()
plt.show()

print("Line plot created successfully")
```

**Explanation:**

- `sns.set_style()`: Applies consistent Seaborn styling
- `sns.set_palette()`: Uses a cohesive color palette
- `figsize`: Controls plot dimensions
- `linewidth`, `marker`, `markersize`: Customize line appearance
- `tight_layout()`: Adjusts spacing automatically
- `grid()`: Adds reference lines for readability

#### 1.2 Exercise

1. Load a dataset with at least 2–3 numeric columns
2. Create a simple line plot showing trends over time
3. Add proper titles, labels, and legends
4. Customize colors and line styles
5. Save the figure as a PNG file with 300 DPI

---

### 2. Line Charts and Trend Analysis

Line charts are ideal for displaying data trends over time or continuous ranges. They help viewers identify patterns, peaks, and anomalies.

#### 2.1 Code Example

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

# Sample dataset: Website traffic over 30 days
days = pd.date_range("2025-01-01", periods=30, freq="D")
traffic_data = {
    "Date": days,
    "Desktop": 5000 + np.random.randint(-500, 500, 30)
                + np.arange(30) * 50,
    "Mobile": 3000 + np.random.randint(-300, 300, 30)
              + np.arange(30) * 40,
    "Tablet": 1500 + np.random.randint(-200, 200, 30)
              + np.arange(30) * 20,
}
df = pd.DataFrame(traffic_data)

print("Website Traffic Data (First 5 rows):")
print(df.head())
print("----------------------------")

# Create multiple subplots for different perspectives
fig, axes = plt.subplots(2, 1, figsize=(14, 10))

# Subplot 1: All devices in one plot
axes[0].plot(df["Date"], df["Desktop"], label="Desktop",
             marker="o", linewidth=2, alpha=0.8)
axes[0].plot(df["Date"], df["Mobile"], label="Mobile",
             marker="s", linewidth=2, alpha=0.8)
axes[0].plot(df["Date"], df["Tablet"], label="Tablet",
             marker="^", linewidth=2, alpha=0.8)
axes[0].set_title("Website Traffic: All Devices", fontsize=12,
                  fontweight="bold")
axes[0].set_xlabel("Date")
axes[0].set_ylabel("Traffic (visitors)")
axes[0].legend(loc="best")
axes[0].grid(True, alpha=0.3)

# Subplot 2: Stacked area chart
axes[1].stackplot(df["Date"], df["Desktop"], df["Mobile"],
                  df["Tablet"], labels=["Desktop", "Mobile",
                  "Tablet"], alpha=0.8)
axes[1].set_title("Website Traffic: Stacked View", fontsize=12,
                  fontweight="bold")
axes[1].set_xlabel("Date")
axes[1].set_ylabel("Traffic (visitors)")
axes[1].legend(loc="best")
axes[1].grid(True, alpha=0.3)

plt.tight_layout()
plt.show()

print("Multi-subplot visualization created")
print("----------------------------")

# Calculate and display statistics
print("Traffic Statistics:")
print(f"Desktop Average: {df['Desktop'].mean():.0f}")
print(f"Mobile Average: {df['Mobile'].mean():.0f}")
print(f"Tablet Average: {df['Tablet'].mean():.0f}")
```

**Explanation:**

- `plt.subplots()`: Creates multiple plots in a grid
- `stackplot()`: Shows composition with stacked areas
- `alpha`: Controls transparency for visibility
- Different markers: Distinguish between multiple lines
- `marker` options: `"o"` (circle), `"s"` (square), `"^"` (triangle)

#### 2.2 Exercise

1. Create a dataset with time-series data (e.g., daily temperatures)
2. Generate line charts for multiple categories
3. Add trend annotations (e.g., "Peak: 5/15")
4. Compare stacked vs. overlaid line charts
5. Identify and highlight anomalies

---

### 3. Bar Charts and Categorical Comparisons

Bar charts effectively compare values across categories. They're ideal for showing rankings, differences, and distributions.

#### 3.1 Code Example

```python
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
import pandas as pd

# Sample dataset: Product sales by region
sales_data = {
    "Region": ["North", "South", "East", "West"],
    "Q1": [50000, 45000, 55000, 48000],
    "Q2": [55000, 50000, 60000, 52000],
    "Q3": [60000, 52000, 65000, 55000],
    "Q4": [70000, 58000, 75000, 62000],
}
df = pd.DataFrame(sales_data)

print("Sales by Region and Quarter:")
print(df)
print("----------------------------")

# Create figure with multiple bar chart styles
fig, axes = plt.subplots(2, 2, figsize=(14, 10))
fig.suptitle("Sales Analysis by Region", fontsize=16,
             fontweight="bold")

# 1. Grouped bar chart
x = np.arange(len(df["Region"]))
width = 0.2
quarters = ["Q1", "Q2", "Q3", "Q4"]

for i, quarter in enumerate(quarters):
    axes[0, 0].bar(x + i * width, df[quarter], width,
                   label=quarter)

axes[0, 0].set_xlabel("Region")
axes[0, 0].set_ylabel("Sales ($)")
axes[0, 0].set_title("Grouped Bar Chart")
axes[0, 0].set_xticks(x + width * 1.5)
axes[0, 0].set_xticklabels(df["Region"])
axes[0, 0].legend()
axes[0, 0].grid(axis="y", alpha=0.3)

# 2. Stacked bar chart
df.set_index("Region")[quarters].plot(kind="bar", stacked=True,
                                       ax=axes[0, 1], width=0.7)
axes[0, 1].set_title("Stacked Bar Chart")
axes[0, 1].set_xlabel("Region")
axes[0, 1].set_ylabel("Sales ($)")
axes[0, 1].legend(title="Quarter")
axes[0, 1].grid(axis="y", alpha=0.3)

# 3. Horizontal bar chart (ranking)
total_sales = df[quarters].sum(axis=1)
sorted_sales = total_sales.sort_values()

axes[1, 0].barh(sorted_sales.index, sorted_sales.values,
                color="steelblue")
axes[1, 0].set_title("Total Sales by Region (Ranking)")
axes[1, 0].set_xlabel("Total Sales ($)")
axes[1, 0].grid(axis="x", alpha=0.3)

# Add value labels on bars
for i, v in enumerate(sorted_sales.values):
    axes[1, 0].text(v + 1000, i, f"${v:,.0f}",
                    va="center", fontweight="bold")

# 4. Comparison bar chart (Seaborn)
sales_melted = df.melt(id_vars=["Region"], var_name="Quarter",
                        value_name="Sales")
sns.barplot(data=sales_melted, x="Region", y="Sales",
            hue="Quarter", ax=axes[1, 1])
axes[1, 1].set_title("Sales by Region and Quarter (Seaborn)")
axes[1, 1].grid(axis="y", alpha=0.3)

plt.tight_layout()
plt.show()

print("Bar chart visualizations created")
```

**Explanation:**

- **Grouped bars**: Compare multiple categories side by side
- **Stacked bars**: Show composition of totals
- **Horizontal bars**: Better for long category names
- `melt()`: Transforms data for categorical plotting
- Value labels: Add precision to visual interpretation

#### 3.2 Exercise

1. Create dataset with categorical data (e.g., product categories, departments)
2. Generate grouped and stacked bar charts
3. Create horizontal bar chart with rankings
4. Add value labels directly on bars
5. Compare Matplotlib vs. Seaborn bar charts

---

### 4. Histograms and Distributions

Histograms display frequency distributions of continuous data, revealing patterns in data spread and central tendency.

#### 4.1 Code Example

```python
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
import numpy as np

# Generate sample dataset: Student test scores by subject
np.random.seed(42)
data = {
    "Math": np.random.normal(75, 12, 200),
    "English": np.random.normal(72, 15, 200),
    "Science": np.random.normal(78, 10, 200),
}
df = pd.DataFrame(data)

print("Test Scores Summary:")
print(df.describe())
print("----------------------------")

# Create figure with histogram variations
fig, axes = plt.subplots(2, 2, figsize=(14, 10))
fig.suptitle("Distribution Analysis: Test Scores",
             fontsize=16, fontweight="bold")

# 1. Basic histogram
axes[0, 0].hist(df["Math"], bins=20, color="skyblue",
                edgecolor="black", alpha=0.7)
axes[0, 0].set_title("Histogram: Math Scores")
axes[0, 0].set_xlabel("Score")
axes[0, 0].set_ylabel("Frequency")
axes[0, 0].axvline(df["Math"].mean(), color="red", linestyle="--",
                   linewidth=2, label=f"Mean: {df['Math'].mean():.1f}")
axes[0, 0].axvline(df["Math"].median(), color="green",
                   linestyle="--", linewidth=2,
                   label=f"Median: {df['Math'].median():.1f}")
axes[0, 0].legend()
axes[0, 0].grid(axis="y", alpha=0.3)

# 2. Histogram with KDE (Kernel Density Estimate)
axes[0, 1].hist(df["English"], bins=20, color="lightcoral",
                edgecolor="black", alpha=0.7, density=True)
axes[0, 1].set_title("Histogram with KDE: English Scores")
axes[0, 1].set_xlabel("Score")
axes[0, 1].set_ylabel("Density")

# Add KDE curve
from scipy import stats
x = np.linspace(df["English"].min(), df["English"].max(), 100)
kde = stats.gaussian_kde(df["English"])
axes[0, 1].plot(x, kde(x), "k-", linewidth=2, label="KDE")
axes[0, 1].legend()
axes[0, 1].grid(axis="y", alpha=0.3)

# 3. Multiple distributions overlay
axes[1, 0].hist(df["Math"], bins=15, alpha=0.5, label="Math",
                color="blue")
axes[1, 0].hist(df["English"], bins=15, alpha=0.5, label="English",
                color="orange")
axes[1, 0].hist(df["Science"], bins=15, alpha=0.5, label="Science",
                color="green")
axes[1, 0].set_title("Overlaid Distributions")
axes[1, 0].set_xlabel("Score")
axes[1, 0].set_ylabel("Frequency")
axes[1, 0].legend()
axes[1, 0].grid(axis="y", alpha=0.3)

# 4. Seaborn distplot (multiple features)
sns.histplot(data=df, kde=True, stat="density", bins=20,
             ax=axes[1, 1])
axes[1, 1].set_title("Seaborn Distribution Plot")
axes[1, 1].set_xlabel("Score")
axes[1, 1].set_ylabel("Density")
axes[1, 1].grid(axis="y", alpha=0.3)

plt.tight_layout()
plt.show()

print("Distribution visualizations created")
```

**Explanation:**

- **Bins**: Number of intervals for histogram
- **KDE**: Smooth curve representing data distribution
- **Alpha**: Transparency for overlaid histograms
- **Density**: Normalize histogram to probability density
- `axvline()`: Add reference lines (mean, median)

#### 4.2 Exercise

1. Generate 3 datasets with different distributions
2. Create histograms with varying bin sizes
3. Overlay KDE curves on histograms
4. Compare multiple distributions side by side
5. Identify distribution shape (normal, skewed, bimodal)

---

### 5. Scatter Plots and Correlations

Scatter plots reveal relationships between two continuous variables, helping identify correlations and patterns.

#### 5.1 Code Example

```python
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
import numpy as np

# Sample dataset: House prices vs. various features
np.random.seed(42)
n_samples = 200
data = {
    "Square_Feet": np.random.normal(2000, 500, n_samples),
    "Bedrooms": np.random.randint(1, 6, n_samples),
    "Age": np.random.randint(1, 100, n_samples),
}

# Create price with relationships to features
data["Price"] = (100 * data["Square_Feet"] + 50000 *
                 data["Bedrooms"] - 1000 * data["Age"] +
                 np.random.normal(0, 100000, n_samples))

df = pd.DataFrame(data)

print("House Data Summary:")
print(df.head(10))
print(df.corr())
print("----------------------------")

# Create scatter plot variations
fig, axes = plt.subplots(2, 2, figsize=(14, 10))
fig.suptitle("House Features vs. Price Analysis", fontsize=16,
             fontweight="bold")

# 1. Basic scatter plot with regression line
axes[0, 0].scatter(df["Square_Feet"], df["Price"], alpha=0.6,
                   s=50, color="steelblue")
z = np.polyfit(df["Square_Feet"], df["Price"], 1)
p = np.poly1d(z)
axes[0, 0].plot(df["Square_Feet"].sort_values(),
                p(df["Square_Feet"].sort_values()), "r--",
                linewidth=2, label="Trend line")
axes[0, 0].set_title("Price vs. Square Footage")
axes[0, 0].set_xlabel("Square Feet")
axes[0, 0].set_ylabel("Price ($)")
axes[0, 0].legend()
axes[0, 0].grid(True, alpha=0.3)

# 2. Scatter plot with color gradient
scatter = axes[0, 1].scatter(df["Square_Feet"], df["Price"],
                             c=df["Age"], cmap="viridis",
                             s=100, alpha=0.6)
axes[0, 1].set_title("Price vs. Square Footage (colored by Age)")
axes[0, 1].set_xlabel("Square Feet")
axes[0, 1].set_ylabel("Price ($)")
cbar = plt.colorbar(scatter, ax=axes[0, 1])
cbar.set_label("Age (years)")
axes[0, 1].grid(True, alpha=0.3)

# 3. Seaborn regplot (regression plot)
sns.regplot(data=df, x="Bedrooms", y="Price", ax=axes[1, 0],
            scatter_kws={"s": 50, "alpha": 0.6},
            line_kws={"color": "red", "linewidth": 2})
axes[1, 0].set_title("Price vs. Number of Bedrooms")
axes[1, 0].grid(True, alpha=0.3)

# 4. Seaborn hexbin plot (for dense data)
axes[1, 1].hexbin(df["Square_Feet"], df["Price"], gridsize=15,
                  cmap="YlOrRd", mincnt=1)
axes[1, 1].set_title("Price vs. Square Footage (Hexbin)")
axes[1, 1].set_xlabel("Square Feet")
axes[1, 1].set_ylabel("Price ($)")
axes[1, 1].grid(True, alpha=0.3)

plt.tight_layout()
plt.show()

print("Scatter plot visualizations created")

# Calculate correlation
print("\nCorrelation Analysis:")
print(df.corr()["Price"].sort_values(ascending=False))
```

**Explanation:**

- **Scatter plot**: Display individual data points
- **Regression line**: Show linear relationship trend
- **Color mapping**: Represent third variable using color
- **Hexbin**: Aggregate overlapping points for clarity
- **s parameter**: Control point size
- `cmap`: Color map for continuous variables

#### 5.2 Exercise

1. Load dataset with 2+ numeric columns (e.g., Iris dataset)
2. Create scatter plots for different variable pairs
3. Add regression lines and trend analysis
4. Use color gradients to represent third dimension
5. Calculate and display correlation coefficients

---

### 6. Advanced Customization and Best Practices

Professional visualizations require careful attention to aesthetics, clarity, and accessibility.

#### 6.1 Code Example

```python
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd
import numpy as np

# Sample dataset
data = {
    "Month": ["Jan", "Feb", "Mar", "Apr", "May", "Jun"],
    "Revenue": [45000, 52000, 48000, 61000, 55000, 70000],
    "Expenses": [30000, 32000, 31000, 35000, 33000, 38000],
}
df = pd.DataFrame(data)

print("Financial Data:")
print(df)
print("----------------------------")

# Create professional-looking figure
fig, ax = plt.subplots(figsize=(12, 7))

# Plot data
x = np.arange(len(df))
width = 0.35

bars1 = ax.bar(x - width/2, df["Revenue"], width, label="Revenue",
               color="#2E86AB", alpha=0.9, edgecolor="black",
               linewidth=1.5)
bars2 = ax.bar(x + width/2, df["Expenses"], width,
               label="Expenses", color="#A23B72", alpha=0.9,
               edgecolor="black", linewidth=1.5)

# Customize axes and labels
ax.set_xlabel("Month", fontsize=12, fontweight="bold")
ax.set_ylabel("Amount ($)", fontsize=12, fontweight="bold")
ax.set_title("Revenue vs. Expenses Analysis", fontsize=14,
             fontweight="bold", pad=20)
ax.set_xticks(x)
ax.set_xticklabels(df["Month"])
ax.legend(fontsize=11, loc="upper left", framealpha=0.95)

# Format y-axis with thousands separator
ax.yaxis.set_major_formatter(plt.FuncFormatter(
    lambda x, p: f"${x/1000:.0f}K"))

# Add gridlines
ax.grid(axis="y", alpha=0.3, linestyle="--", linewidth=0.7)
ax.set_axisbelow(True)

# Add value labels on bars
for bar in bars1:
    height = bar.get_height()
    ax.text(bar.get_x() + bar.get_width()/2., height,
            f"${height/1000:.0f}K", ha="center", va="bottom",
            fontsize=10, fontweight="bold")

for bar in bars2:
    height = bar.get_height()
    ax.text(bar.get_x() + bar.get_width()/2., height,
            f"${height/1000:.0f}K", ha="center", va="bottom",
            fontsize=10, fontweight="bold")

# Add profit annotation
profit = df["Revenue"] - df["Expenses"]
for i, p in enumerate(profit):
    ax.text(i, max(df["Revenue"].iloc[i], df["Expenses"].iloc[i]) +
            5000, f"Profit: ${p/1000:.0f}K", ha="center",
            fontsize=9, style="italic", color="green",
            fontweight="bold")

# Customize spines (chart borders)
sns.despine(left=False, bottom=False, top=True, right=True)

plt.tight_layout()
plt.show()

print("Professional visualization created")
print("----------------------------")

# Save high-quality figure
plt.savefig("revenue_analysis.png", dpi=300, bbox_inches="tight",
            facecolor="white")
print("Figure saved as 'revenue_analysis.png'")
```

**Explanation:**

- **Color palette**: Use professional, colorblind-friendly colors
- **Edgecolor**: Add borders to bars for definition
- **Annotations**: Add value labels directly on visualizations
- **FuncFormatter**: Custom axis formatting
- **despine()**: Remove unnecessary chart borders
- **High DPI**: 300 DPI for publication-quality output
- **bbox_inches**: Include all elements when saving

#### 6.2 Best Practices Summary

**Design Principles:**

- Use consistent colors and fonts across figures
- Limit to 5 or fewer colors per chart
- Ensure high contrast for readability
- Label all axes with units

**Clarity Guidelines:**

- Write descriptive titles and subtitles
- Remove unnecessary gridlines and decorations
- Use direct labeling instead of legends when possible
- Ensure text is legible at all sizes

**Accessibility:**

- Use colorblind-friendly palettes (viridis, cividis)
- Never rely on color alone to convey information
- Include alt-text for web-based visualizations
- Test figures in grayscale

#### 6.3 Exercise

1. Recreate a basic chart (bar or line)
2. Apply professional styling (colors, fonts, labels)
3. Add value annotations and reference lines
4. Customize axis formatting and gridlines
5. Save at high resolution (300 DPI)
6. Test with colorblind simulator

---

## Summary

You now understand:

- Creating line charts for trend analysis
- Designing bar charts for categorical comparisons
- Building histograms to visualize distributions
- Constructing scatter plots to show relationships
- Customizing plots with professional styling
- Following best practices for clarity and accessibility
- Saving high-quality visualizations
- Communicating insights effectively through visuals

These visualization skills are essential for exploratory data analysis, business reporting, and data storytelling. Mastering these techniques enables you to transform raw data into compelling narratives that drive understanding and decision-making.

## Up Next

In Lab 6, you'll explore advanced data representation techniques including heatmaps, correlation matrices, interactive visualizations, and comprehensive dashboards to communicate complex insights effectively.
