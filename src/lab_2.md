# Lab 2: Dataset Manipulation with Python

## Objectives

- Learn to load and explore datasets using Pandas
- Understand DataFrame structure and operations
- Clean and manipulate data for AI applications
- Process real-world datasets effectively
- Build skills for data preprocessing in machine learning

## Tools and Resources

- **Tools**
  - [Python](https://www.python.org/)
  - [Jupyter Notebook](https://jupyter.org/) or [Visual Studio Code](https://code.visualstudio.com/)
  - [Pandas](https://pandas.pydata.org/)
  - [NumPy](https://numpy.org/)

- **Resources**
  - [Pandas Official Documentation](https://pandas.pydata.org/docs/)
  - [Real Python - Pandas Tutorial](https://realpython.com/learning-paths/pandas-data-science/)
  - [Kaggle Datasets](https://www.kaggle.com/datasets)
  - [Data Manipulation Cheatsheet](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)

## Content

### 1. Introduction to Pandas and DataFrames

Pandas is a powerful library for data manipulation and analysis. DataFrames are the core data structure, similar to Excel spreadsheets or SQL tables.

#### 1.1 Code Example

```python
import pandas as pd

# Creating a DataFrame from a dictionary
data = {
    "Name": ["Ahmed", "Fatima", "Ali", "Layla"],
    "Age": [25, 28, 22, 30],
    "Salary": [3000, 3500, 2800, 4000],
    "Department": ["IT", "HR", "IT", "Finance"],
}
df = pd.DataFrame(data)
print("DataFrame from a dictionary:")
print(df)
print("----------------------------")

# Creating a DataFrame from lists
employees = [
    ["Hassan", 26, 3200, "IT"],
    ["Noor", 24, 2900, "HR"],
    ["Mariam", 29, 3800, "Finance"],
]
df2 = pd.DataFrame(employees, columns=["Name", "Age", "Salary", "Department"])
print("DataFrame from lists:")
print(df2)
print("----------------------------")

# Viewing basic information
print("Basic information:")
print(df.head())  # First 5 rows
print("----------------------------")
print(df.tail(2))  # Last 2 rows
print("----------------------------")
print(df.shape)  # (rows, columns)
print("----------------------------")
print(df.info())  # Data types and info
print("----------------------------")
print(df.describe())  # Statistical summary
```

**Explanation:**

- DataFrames have rows and columns like spreadsheets
- `head()`: Shows first n rows (default 5)
- `tail()`: Shows last n rows
- `shape`: Returns tuple of (num_rows, num_columns)
- `info()`: Displays data types and missing values
- `describe()`: Provides statistical summary

#### 1.2 Exercise

Create a DataFrame with the following data:

| Product | Price | Quantity | Category    |
| ------- | ----- | -------- | ----------- |
| Laptop  | 800   | 5        | Electronics |
| Desk    | 150   | 12       | Furniture   |
| Chair   | 75    | 25       | Furniture   |
| Mouse   | 25    | 40       | Electronics |
| Monitor | 300   | 8        | Electronics |

1. Create the DataFrame from a dictionary
2. Display the first 3 rows
3. Show the shape and data types
4. Print statistical summary

---

### 2. Loading Data from Files

Real-world data often comes from CSV, Excel, or other file formats.

#### 2.1 Code Example

```python
import pandas as pd

# Loading CSV file
df_csv = pd.read_csv('students.csv')
print(df_csv.head())

# Loading Excel file
df_excel = pd.read_excel('data.xlsx', sheet_name='Sheet1')
print(df_excel)

# Specifying additional parameters
df = pd.read_csv('data.csv',
                  sep=',',           # Delimiter
                  encoding='utf-8',  # File encoding
                  skiprows=1,        # Skip first row
                  nrows=100)         # Read only 100 rows

# Saving DataFrame to file
df.to_csv('output.csv', index=False)
df.to_excel('output.xlsx', index=False)
df.to_json('output.json')

# Loading from URL
url = 'https://raw.githubusercontent.com/example/data.csv'
df_url = pd.read_csv(url)
print(df_url.head())
```

**Explanation:**

- `read_csv()`: Load data from CSV files
- `read_excel()`: Load data from Excel files
- Parameters customize how data is imported
- `to_csv()`, `to_excel()`: Save DataFrame to various formats
- `index=False`: Don't save row indices

#### 2.2 Exercise

1. Load the `students.csv` file into a DataFrame using Pandas
2. Display the first and last 3 rows
3. Save the DataFrame to an Excel file
4. Load the Excel file back and verify the data matches

---

### 3. Accessing and Selecting Data

Efficiently extracting specific data from DataFrames is crucial for analysis.

#### 3.1 Code Example

```python
import pandas as pd

# Sample DataFrame
data = {
    "StudentID": [101, 102, 103, 104, 105],
    "Name": ["Ahmed", "Fatima", "Ali", "Layla", "Hassan"],
    "Math": [85, 90, 78, 92, 88],
    "Science": [88, 87, 92, 85, 90],
    "English": [80, 95, 85, 90, 82],
}
df = pd.DataFrame(data)

# Accessing columns
print(df["Name"])  # Single column (Series)
print(df[["Name", "Math"]])  # Multiple columns (DataFrame)
print("----------------------------")

# Accessing rows
print(df.loc[0])  # By label/index
print(df.iloc[0])  # By position
print(df.loc[0:2])  # Multiple rows by label
print(df.iloc[0:3])  # Multiple rows by position
print("----------------------------")

# Conditional selection
print(df[df["Math"] > 85])  # Rows where Math > 85
print(df[(df["Math"] > 80) & (df["Science"] > 85)])
print("----------------------------")

# Accessing specific cells
print(df.loc[0, "Name"])  # By label
print(df.iloc[0, 1])  # By position
print("----------------------------")

# Using .at and .iat for single values
print(df.at[0, "Math"])  # Fast access by label
print(df.iat[0, 2])  # Fast access by position
```

**Explanation:**

- `df['column']`: Access single column
- `df[['col1', 'col2']]`: Access multiple columns
- `loc[]`: Label-based indexing
- `iloc[]`: Position-based indexing
- Boolean indexing for conditional selection

#### 3.2 Exercise

Using the student DataFrame from Exercise 2:

1. Extract and print only the student names
2. Display rows where GPA is greater than 3.0
3. Show all columns except the ID
4. Find students in a specific major using conditional selection
5. Get the value at row 2, column 'GPA' using both `loc[]` and `iloc[]`

---

### 4. Data Cleaning and Handling Missing Values

Real datasets often have missing or incorrect values that must be handled.

#### 4.1 Code Example

```python
import numpy as np
import pandas as pd

# Creating DataFrame with missing values
data = {
    "ID": [1, 2, 3, 4, 5],
    "Name": ["Ahmed", "Fatima", None, "Layla", "Hassan"],
    "Age": [25, np.nan, 30, 28, 35],
    "Salary": [3000, 3500, 2800, np.nan, 4500],
}
df = pd.DataFrame(data)
print("Original DataFrame:")
print(df)
print("----------------------------")

# Checking for missing values
print(df.isnull())  # True for missing values
print(df.isnull().sum())  # Count missing per column
print(df.dropna())  # Remove rows with any missing value
print("----------------------------")

# Dropping specific columns with missing values
print(df.dropna(subset=["Age"]))
print("----------------------------")

# Filling missing values
df_filled = df.fillna(0)  # Fill with 0
print(df_filled)
print("----------------------------")

# Fill with column mean/average
df["Age"] = df["Age"].fillna(df["Age"].mean())
print(df)
print("----------------------------")

# Forward fill and backward fill
df["Salary"] = df["Salary"].ffill()
print(df)
print("----------------------------")

# Removing duplicates
data2 = {"Name": ["Ahmed", "Fatima", "Ahmed", "Ali"], "Age": [25, 28, 25, 22]}
df2 = pd.DataFrame(data2)
print("\nDataFrame with duplicates:")
print(df2)
print("\nAfter removing duplicates:")
print(df2.drop_duplicates())
print("----------------------------")

# Removing specific duplicate columns
print(df2.drop_duplicates(subset=["Name"]))
```

**Explanation:**

- `isnull()`: Identifies missing values
- `dropna()`: Removes rows/columns with missing values
- `fillna()`: Replaces missing values
- `drop_duplicates()`: Removes duplicate rows
- `mean()`, `median()`: Statistics for filling values

#### 4.2 Exercise

1. Create a DataFrame with intentional missing values and duplicates
2. Display summary of missing values
3. Remove rows with missing critical data
4. Fill missing values in numeric columns with the column mean
5. Remove duplicate rows
6. Verify the cleaned data

---

### 5. Data Transformation and Manipulation

Transform data into useful formats for analysis.

#### 5.1 Code Example

```python
import pandas as pd

# Sample DataFrame
data = {
    "ID": [1, 2, 3, 4],
    "FirstName": ["ahmed", "FATIMA", "ali", "LAYLA"],
    "LastName": ["Hassan", "ali", "Mahmoud", "Ibrahim"],
    "Salary": [3000, 3500, 2800, 4000],
    "Department": ["IT", "IT", "HR", "Finance"],
}
df = pd.DataFrame(data)

# String operations
df["FirstName"] = df["FirstName"].str.capitalize()
df["FullName"] = df["FirstName"] + " " + df["LastName"]
print(df[["FirstName", "LastName", "FullName"]])
print("----------------------------")

# Numeric operations
df["SalaryIncrease"] = df["Salary"] * 1.10  # 10% increase
df["TaxAmount"] = df["Salary"] * 0.15
print(df[["Salary", "SalaryIncrease", "TaxAmount"]])
print("----------------------------")

# Creating new columns based on conditions
df["SalaryLevel"] = df["Salary"].apply(
    lambda x: "Low" if x < 3000 else "Medium" if x < 3500 else "High"
)
print(df[["Salary", "SalaryLevel"]])
print("----------------------------")

# Renaming columns
df_renamed = df.rename(
    columns={"ID": "EmployeeID", "FirstName": "First Name", "Salary": "Monthly Salary"}
)
print(df_renamed.columns)
print("----------------------------")

# Sorting data
print("Sorted by Salary (ascending):")
print(df.sort_values("Salary"))

print("Sorted by Department then Salary (descending):")
print(df.sort_values(["Department", "Salary"], ascending=[True, False]))
print("----------------------------")

# Filtering and selecting
print("IT Department employees:")
print(df[df["Department"] == "IT"])
print("----------------------------")

# Grouping data
print("Average salary by department:")
print(df.groupby("Department")["Salary"].mean())
```

**Explanation:**

- String methods: `str.capitalize()`, `str.upper()`, `str.lower()`
- `apply()`: Apply functions to columns
- Lambda functions: Anonymous functions for quick operations
- `sort_values()`: Sort by one or multiple columns
- `groupby()`: Group data for aggregation

#### 5.2 Exercise

1. Load the `employees.csv` file into a DataFrame using Pandas
2. Create a "FullName" column combining first and last names
3. Calculate bonus (15% of salary) and net salary (salary - tax)
4. Categorize employees as "Junior", "Senior", or "Manager" based on salary

---

### 6. Advanced Data Manipulation

Combine and reshape data for complex analysis.

#### 6.1 Code Example

```python
import pandas as pd

# Sample DataFrames
employees = {
    'EmployeeID': [1, 2, 3, 4],
    'Name': ['Ahmed', 'Fatima', 'Ali', 'Layla'],
    'DepartmentID': [1, 1, 2, 2]
}

departments = {
    'DepartmentID': [1, 2],
    'Department': ['IT', 'HR'],
    'Budget': [50000, 30000]
}

df_emp = pd.DataFrame(employees)
df_dept = pd.DataFrame(departments)

# Merging DataFrames
merged = pd.merge(df_emp, df_dept, on='DepartmentID')
print("Merged DataFrame:")
print(merged)

# Different join types
left_join = pd.merge(df_emp, df_dept,
                     on='DepartmentID', how='left')
print("\nLeft Join:")
print(left_join)

# Concatenating DataFrames
df1 = pd.DataFrame({
    'Name': ['Ahmed', 'Fatima'],
    'Score': [85, 90]
})
df2 = pd.DataFrame({
    'Name': ['Ali', 'Layla'],
    'Score': [78, 92]
})
concatenated = pd.concat([df1, df2], ignore_index=True)
print("\nConcatenated:")
print(concatenated)

# Melting (unpivot) - converting wide to long format
data = {
    'Student': ['Ahmed', 'Fatima', 'Ali'],
    'Math': [85, 90, 78],
    'Science': [88, 87, 92],
    'English': [80, 95, 85]
}
df_wide = pd.DataFrame(data)
df_long = pd.melt(df_wide, id_vars=['Student'],
                   var_name='Subject', value_name='Score')
print("\nMelted DataFrame:")
print(df_long)

# Pivot - converting long to wide format
df_pivot = df_long.pivot(index='Student',
                         columns='Subject',
                         values='Score')
print("\nPivot Table:")
print(df_pivot)

# Creating pivot tables with aggregation
sales = {
    'Month': ['Jan', 'Jan', 'Feb', 'Feb', 'Jan', 'Feb'],
    'Product': ['A', 'B', 'A', 'B', 'A', 'B'],
    'Sales': [100, 150, 120, 180, 90, 200]
}
df_sales = pd.DataFrame(sales)
pivot_sales = pd.pivot_table(df_sales,
                              values='Sales',
                              index='Month',
                              columns='Product',
                              aggfunc='sum')
print("\nPivot Table with Aggregation:")
print(pivot_sales)
```

**Explanation:**

- `merge()`: Combine DataFrames based on common columns
- `concat()`: Stack DataFrames vertically or horizontally
- `melt()`: Transform from wide to long format
- `pivot()`: Transform from long to wide format
- `pivot_table()`: Create pivot tables with aggregation

---

## Summary

You now understand:

- Creating and loading DataFrames
- Accessing and selecting specific data
- Identifying and handling missing values
- Data transformation and cleaning
- Advanced manipulation with merging and pivoting

These skills are essential for preprocessing datasets in machine learning projects!

## Up Next

In Lab 3, you'll learn data summarization and statistical analysis using Python to extract meaningful insights from datasets.
