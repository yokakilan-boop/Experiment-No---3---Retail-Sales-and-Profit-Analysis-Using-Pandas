# DSWP-Experiment-3-Retail-Sales-and-Profit-Analysis-Using-Pandas

## Aim
To create a sample retail dataset, identify and handle missing values (`NaN`/`None`) and duplicate records, and compute summary statistics using Pandas in Python.

## Algorithm

1. **Start** the program.
2. **Import Library**: Import the `pandas` library as `pd` for tabular data cleaning and analysis.
3. **Initialize Raw Retail Dataset**: Create a Python dictionary `data` containing retail records (`Order_ID`, `Product`, `Region`, `Sales`, `Discount`, `Profit`) with deliberate missing (`None`) entries and duplicate rows.
4. **Construct DataFrame & Inspect**:
   * Convert `data` into a Pandas DataFrame `df` using `pd.DataFrame(data)`.
   * Print the original dataset and its initial dimensions (`df.shape`).
5. **Detect Missing Values**:
   * Count missing entries per column using `df.isnull().sum()`.
6. **Impute Missing Values**:
   * Replace missing numerical values in `Sales`, `Discount`, and `Profit` with their respective column means using `.fillna(df[col].mean())`.
   * Replace missing categorical values in `Region` with the column mode (most frequent category) using `.fillna(df["Region"].mode()[0])`.
7. **Remove Duplicate Records**:
   * Drop exact duplicate rows from `df` using `df.drop_duplicates()`.
8. **Display Cleaned Dataset & Summary Statistics**:
   * Print the cleaned DataFrame, updated dimensions (`df.shape`), and descriptive statistical metrics (`df.describe()`).
9. **Stop** the program.

## Functions and Methods Used

| Category | Function / Method | Purpose / Description |
| :--- | :--- | :--- |
| **Data Creation & Inspection** | `pd.DataFrame()` | Converts a Python dictionary into a labeled 2D tabular DataFrame |
| | `df.shape` | Returns the `(rows, columns)` dimensions before and after cleaning |
| | `df.isnull().sum()` | Counts the number of missing (`NaN`/`None`) values in each column |
| **Missing Value Imputation** | `df[col].fillna()` | Replaces missing values with a specified replacement value |
| | `df[col].mean()` | Calculates the arithmetic mean for numerical column imputation |
| | `df[col].mode()[0]` | Retrieves the most frequent category for categorical column imputation |
| **Deduplication & Summary** | `df.drop_duplicates()` | Identifies and removes duplicate rows from the DataFrame |
| | `df.describe()` | Generates count, mean, standard deviation, min, quartiles, and max for numerical features |

## Program
## Input 1
```
# Cleaning and Preparing Retail Data using Pandas
import pandas as pd

# Step 1: Create a sample retail dataset
data = {
    "Order_ID": [101, 102, 103, 104, 105, 105, 106, 107],
    "Product": ["Laptop", "Tablet", "Phone", "Printer", "Monitor", "Monitor", "Tablet", "Laptop"],
    "Region": ["East", "West", "North", "South", "East", "East", "West", None],
    "Sales": [55000, 32000, None, 18000, 24000, 24000, 32000, 55000],
    "Discount": [5, None, 10, 8, 5, 5, None, 8],
    "Profit": [8000, 5000, 4000, None, 3000, 3000, 5000, 8000]
}

df = pd.DataFrame(data)
print("---- Original Retail Dataset ----")
print(df)
print("\nDataset Shape:", df.shape)
```
## Output 1
```
---- Original Retail Dataset ----
   Order_ID  Product Region    Sales  Discount  Profit
0       101   Laptop   East  55000.0       5.0  8000.0
1       102   Tablet   West  32000.0       NaN  5000.0
2       103    Phone  North      NaN      10.0  4000.0
3       104  Printer  South  18000.0       8.0     NaN
4       105  Monitor   East  24000.0       5.0  3000.0
5       105  Monitor   East  24000.0       5.0  3000.0
6       106   Tablet   West  32000.0       NaN  5000.0
7       107   Laptop   None  55000.0       8.0  8000.0

Dataset Shape: (8, 6)
```
## Input 2
```
# Step 2: Check for missing values
print("\nMissing Values per Column:\n", df.isnull().sum())
```
## Output 2
```
Missing Values per Column:
 Order_ID    0
Product     0
Region      1
Sales       1
Discount    2
Profit      1
dtype: int64
```
## Input 3
```
# Step 3: Fill missing numeric values with column mean
df["Sales"] = df["Sales"].fillna(df["Sales"].mean())
df["Discount"] = df["Discount"].fillna(df["Discount"].mean())
df["Profit"] = df["Profit"].fillna(df["Profit"].mean())

# Step 4: Fill missing Region with mode (most frequent value)
df["Region"] = df["Region"].fillna(df["Region"].mode()[0])

# Step 5: Remove duplicate records
df = df.drop_duplicates()

print("\n---- Cleaned Retail Dataset ----")
print(df)
print("\nDataset Shape after Cleaning:", df.shape)
```
## Output 3
```
---- Cleaned Retail Dataset ----
   Order_ID  Product Region         Sales   Discount       Profit
0       101   Laptop   East  55000.000000   5.000000  8000.000000
1       102   Tablet   West  32000.000000   6.833333  5000.000000
2       103    Phone  North  34285.714286  10.000000  4000.000000
3       104  Printer  South  18000.000000   8.000000  5142.857143
4       105  Monitor   East  24000.000000   5.000000  3000.000000
6       106   Tablet   West  32000.000000   6.833333  5000.000000
7       107   Laptop   East  55000.000000   8.000000  8000.000000

Dataset Shape after Cleaning: (7, 6)
```
## Input 4
```
# Step 6: Display summary statistics
print("\nSummary Statistics:\n", df.describe())
```
## Output 4
```
Summary Statistics:
          Order_ID         Sales   Discount       Profit
count    7.000000      7.000000   7.000000     7.000000
mean   104.000000  35755.102041   7.095238  5448.979592
std      2.160247  14285.884353   1.779141  1897.776306
min    101.000000  18000.000000   5.000000  3000.000000
25%    102.500000  28000.000000   5.916667  4500.000000
50%    104.000000  32000.000000   6.833333  5000.000000
75%    105.500000  44642.857143   8.000000  6571.428571
max    107.000000  55000.000000  10.000000  8000.000000
```


## Result
The program successfully creates a retail dataset, identifies missing entries and duplicate rows, imputes missing values using mean and mode strategies, removes duplicates, and outputs a clean dataset ready for downstream analysis.
