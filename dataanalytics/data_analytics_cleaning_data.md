# Data Cleaning

# Table of Contents

- [Data Cleaning](#data-cleaning)
  - [1. Handling NaN Values](#1-handling-nan-values)
    - [A. Identifying NaN Values](#a-identifying-nan-values)
    - [B. Removing NaN Values](#b-removing-nan-values)
    - [C. Filling NaN Values](#c-filling-nan-values)
    - [D. Interpolation](#d-interpolation)
  - [2. Removing Duplicates](#2-removing-duplicates)
  - [3. Handling Outliers](#3-handling-outliers)
    - [Identifying Outliers](#identifying-outliers)
    - [Removing Outliers](#removing-outliers)
    - [Capping Outliers](#capping-outliers)
  - [4. Data Type Conversion](#4-data-type-conversion)
  - [5. Standardizing and Normalizing Data](#5-standardizing-and-normalizing-data)
    - [Standardization (Z-score Normalization)](#standardization-z-score-normalization)
    - [Normalization (Min-Max Scaling)](#normalization-min-max-scaling)
  - [6. String Cleaning](#6-string-cleaning)
    - [Trimming Whitespaces](#trimming-whitespaces)
    - [Replacing Characters](#replacing-characters)
  - [7. Encoding Categorical Variables](#7-encoding-categorical-variables)
    - [One-Hot Encoding](#one-hot-encoding)
    - [Label Encoding](#label-encoding)
  - [8. Checking for Consistency](#8-checking-for-consistency)
  - [9. Validating Data](#9-validating-data)
  - [10. Documenting Cleaning Steps](#10-documenting-cleaning-steps)
- [Conclusion](#conclusion)


When preparing data for analysis or modeling, it’s essential to clean it thoroughly. Below are strategies to handle common data issues, including NaN values.

## 1. Handling NaN Values

### A. Identifying NaN Values
- **Using Pandas (Python)**
    ```python
    import pandas as pd

    df.isna()  # Returns a DataFrame of the same shape as df with True for NaN values
    df.isna().sum()  # Count of NaN values per column
    ```

### B. Removing NaN Values
- **Drop Rows with Any NaN Values**
    ```python
    df_cleaned = df.dropna()  # Drop rows with any NaN values
    ```

- **Drop Columns with Any NaN Values**
    ```python
    df_cleaned = df.dropna(axis=1)  # Drop columns with any NaN values
    ```

### C. Filling NaN Values
- **Fill with a Specific Value**
    ```python
    df_filled = df.fillna(value=0)  # Fill NaNs with 0
    ```

- **Forward Fill**
    ```python
    df_filled = df.fillna(method='ffill')  # Fill NaNs with the last valid observation
    ```

### D. Interpolation
- **Linear Interpolation**
    ```python
    df_interpolated = df.interpolate()  # Interpolate missing values linearly
    ```

## 2. Removing Duplicates
- **Identifying and Dropping Duplicates**
    ```python
    df.duplicated()  # Returns a boolean Series indicating duplicates
    df_cleaned = df.drop_duplicates()  # Drop duplicate rows
    ```

## 3. Handling Outliers
- **Identifying Outliers**
    ```python
    import seaborn as sns
    import matplotlib.pyplot as plt

    sns.boxplot(x=df['column'])  # Visualize outliers using a boxplot
    ```

- **Removing Outliers**
    ```python
    df_cleaned = df[(df['column'] < upper_limit) & (df['column'] > lower_limit)]  # Use logical conditions to filter
    ```

- **Capping Outliers**
    ```python
    df['column'] = np.where(df['column'] > upper_limit, upper_limit, df['column'])  # Cap values at upper limit
    ```

## 4. Data Type Conversion
- **Converting Data Types**
    ```python
    df['column'] = df['column'].astype('category')  # Convert to categorical type
    df['column'] = pd.to_numeric(df['column'], errors='coerce')  # Convert to numeric, coercing errors to NaN
    ```

## 5. Standardizing and Normalizing Data
- **Standardization (Z-score Normalization)**
    ```python
    from sklearn.preprocessing import StandardScaler

    scaler = StandardScaler()
    df[['column']] = scaler.fit_transform(df[['column']])  # Standardize the column
    ```

- **Normalization (Min-Max Scaling)**
    ```python
    from sklearn.preprocessing import MinMaxScaler

    scaler = MinMaxScaler()
    df[['column']] = scaler.fit_transform(df[['column']])  # Normalize the column
    ```

## 6. String Cleaning
- **Trimming Whitespaces**
    ```python
    df['column'] = df['column'].str.strip()  # Remove leading and trailing whitespaces
    ```

- **Replacing Characters**
    ```python
    df['column'] = df['column'].str.replace('old_value', 'new_value')  # Replace occurrences of old_value with new_value
    ```

## 7. Encoding Categorical Variables
- **One-Hot Encoding**
    ```python
    df_encoded = pd.get_dummies(df, columns=['categorical_column'], drop_first=True)  # One-hot encode a categorical column
    ```

- **Label Encoding**
    ```python
    from sklearn.preprocessing import LabelEncoder

    le = LabelEncoder()
    df['categorical_column'] = le.fit_transform(df['categorical_column'])  # Encode labels as integers
    ```

## 8. Checking for Consistency
- **Ensuring Consistent Data Formats**
    ```python
    df['date_column'] = pd.to_datetime(df['date_column'])  # Convert to datetime format
    ```

## 9. Validating Data
- **Custom Validation Functions**
    ```python
    def validate_data(row):
        # Custom validation logic here
        return True  # or False based on the validation

    df['is_valid'] = df.apply(validate_data, axis=1)  # Apply validation function across rows
    ```

## 10. Documenting Cleaning Steps
- **Maintaining a Data Cleaning Log**
    ```markdown
    ## Data Cleaning Log
    - [Date] - Removed NaN values from 'column_name'
    - [Date] - Dropped duplicates from the dataset
    - [Date] - Converted 'date_column' to datetime format
    ```

## Conclusion

Effective data cleaning is vital for producing reliable analysis and insights. Utilize these strategies to ensure your data is clean, consistent, and ready for analysis.
