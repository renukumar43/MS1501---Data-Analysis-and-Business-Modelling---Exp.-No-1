# Experiment No. 1: Data Cleaning and Preprocessing

## Aim

To perform data cleaning and preprocessing on a business dataset using Python libraries for better data quality and analysis readiness.

## Dataset

The dataset used for this experiment is `heartdisease.csv`. It contains
medical and demographic information related to heart disease patients.

The dataset is opened and analyzed using Jupyter Notebook to study its
data structure, identify data types, and perform basic statistical
analysis for data-cleaning and preprocessing purposes.

## Algorithm

1.  Import essential Python libraries.
2.  Load the dataset using Pandas.
3.  View the dataset structure, data types, and memory usage.
4.  Check for missing values and duplicates.
5.  Perform data summary statistics using `describe()`.
6.  View initial and final records using `head()` and `tail()`.
7.  Sort and group the data based on key attributes.
8.  Rename columns or modify data where necessary.
9.  Save the cleaned dataset for further analysis.

## Functions and Methods Used in the Experiment

### 1. Data Loading and Basic Exploration

  Function / Method      Description  
  ---------------------- ------------------------------------------------------\
  `pd.read_csv()`        Reads a CSV file into a Pandas DataFrame.\
  `df.info()`            Displays column names, data types, and memory usage.\
  `df.dtypes`            Returns the data types of all columns.\
  `df['column'].dtype`   Returns the data type of a specific column.\
  `df.describe()`        Provides summary statistics for numerical columns.\
  `df.head()`            Displays the first 5 rows of the DataFrame.\
  `df.tail()`            Displays the last 5 rows of the DataFrame.\

### 2. Sorting and Grouping

  Function / Method    Description  
  -------------------- ---------------------------------------------  
  `df.sort_values()`   Sorts the DataFrame by one or more columns.  
  `df.groupby()`       Groups data based on one or more columns.  
  `groupby.sum()`      Returns the sum for each group.  
  `groupby.mean()`     Returns the mean for each group.  
  `groupby.median()`   Returns the median for each group.  
  `groupby.max()`      Returns the maximum value in each group.  
  `groupby.min()`      Returns the minimum value in each group.  

### 3. Data Summary and Manipulation  

  Function / Method   Description  
  ------------------- ----------------------------------------------  
  `df.mean()`         Calculates the mean for all numeric columns.  
  `df.rename()`       Renames columns in the DataFrame.  

### 4. Optional Additions  

  Function / Method         Description  
  ------------------------- ----------------------------------------------  
  `df.isnull().sum()`       Checks for missing values in each column.  
  `df.duplicated().sum()`   Counts duplicate rows.  
  `df.dropna()`             Removes rows containing missing values.  
  `df.fillna()`             Fills missing values with a specified value.  
  `df.drop_duplicates()`    Removes duplicate rows.  
  `df.shape`                Returns the number of rows and columns.  
  `df.columns`              Lists column names in the DataFrame.  

## Program & Output
<< Enter your code and the corresponding screenshot of the output in this section>>

# 1. Import essential Python libraries
import pandas as pd  
import numpy as np  
from pathlib import Path  

# Display more columns in notebook output  
pd.set_option('display.max_columns', None)  
pd.set_option('display.width', 120)  

print("Libraries imported successfully.")  

# 2. Load the dataset
file_path = Path("heartdisease (1).csv")  

if not file_path.exists():  
    raise FileNotFoundError(  
        "heartdisease.csv was not found. Place the CSV file in the same folder "  
        "as this notebook, or update file_path with the correct location."  
    )

df = pd.read_csv(file_path)

print("Dataset loaded successfully.")  
print("Dataset shape (rows, columns):", df.shape)  
display(df.head())  

# 3. View dataset structure, data types, and memory usage
print("Dataset information:")  
df.info()  

print("\nData types of all columns:")  
display(df.dtypes)  

print("\nData type of each column:")  
for column in df.columns:  
    print(f"{column}: {df[column].dtype}")  

# 4. Check for missing values and duplicate records
print("Missing values in each column:")  
display(df.isnull().sum())  

print("Total missing values:", df.isnull().sum().sum())  
print("Number of duplicate rows:", df.duplicated().sum())  

# 5. Generate summary statistics
print("Descriptive statistics:")  
display(df.describe(include='all'))  

print("Mean of numeric columns:")  
display(df.mean(numeric_only=True))  

# 6. View the first and last five records
print("First five records:")  
display(df.head())  

print("Last five records:")  
display(df.tail())  

# 7. Sort the dataset
# Sort by the first numeric column, if one is available.
numeric_columns = df.select_dtypes(include=np.number).columns.tolist()  

if numeric_columns:
    sort_column = numeric_columns[0]  
    print(f"Dataset sorted by: {sort_column}")  
    display(df.sort_values(by=sort_column).head(10))  
else:
    print("No numeric columns are available for sorting.")  


# 8. Group the dataset
# Group by the first categorical column and calculate numeric summaries.
categorical_columns = df.select_dtypes(include=['object', 'category', 'bool']).columns.tolist()

if categorical_columns and numeric_columns:
    group_column = categorical_columns[0]  
    print(f"Grouped by: {group_column}")  

    grouped = df.groupby(group_column)[numeric_columns]  
    print("\nMean for each group:")  
    display(grouped.mean())  

    print("\nMedian for each group:")  
    display(grouped.median())  

    print("\nMinimum for each group:")  
    display(grouped.min())  

    print("\nMaximum for each group:")  
    display(grouped.max())  

    print("\nSum for each group:")  
    display(grouped.sum())  
elif numeric_columns:
    print("No categorical column found. Grouping is skipped.")  
else:
    print("No numeric columns found for group summary.")  

    
# 10. Handle missing values and remove duplicate records
# For numeric columns, fill missing values with the median.
# For non-numeric columns, fill missing values with the mode when available.
numeric_cols = df_clean.select_dtypes(include=np.number).columns  
categorical_cols = df_clean.select_dtypes(exclude=np.number).columns  

for column in numeric_cols:
    if df_clean[column].isnull().any():  
        df_clean[column] = df_clean[column].fillna(df_clean[column].median())  

for column in categorical_cols:  
    if df_clean[column].isnull().any():  
        mode_values = df_clean[column].mode(dropna=True)  
        if not mode_values.empty:  
            df_clean[column] = df_clean[column].fillna(mode_values.iloc[0])  

# Remove duplicate rows
df_clean = df_clean.drop_duplicates()  

print("Cleaning completed.")  
print("Shape before cleaning:", df.shape)  
print("Shape after cleaning:", df_clean.shape)  

print("\nMissing values after cleaning:")  
display(df_clean.isnull().sum())  

print("Duplicate rows after cleaning:", df_clean.duplicated().sum())  
    
# 11. Save the cleaned dataset
output_path = Path("heartdisease_cleaned.csv")  
df_clean.to_csv(output_path, index=False)  

print(f"Cleaned dataset saved successfully as: {output_path.resolve()}")  








## Result

<< Enter the program execution result>>
