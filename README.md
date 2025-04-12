### NAME: SURYA P <br>
### REG NO: 212224230280

# DS-Workshop-Data-Cleaning-and-Data-Analysis

## AIM :

1. Perform Data cleaning process wherever necessary

2. Implement Boxplot method to detect outliers

3. Implement IQR method to Remove Outliers 

4. Implement Count plot method for univariate analysis
5. Implement DistPlot method for multivariate analysis

# EXPLANATION : 

Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information. The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.


# ALGORITHM : 

STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers


STEP 7: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 8: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 9: Use boxplot method to analyze the outliers of the given dataset.

STEP 10: Remove the outliers using Inter Quantile Range method.

STEP 11: Use Countplot method to analyze in a graphical method for categorical data.

STEP 12: Use displot method to represent the univariate distribution of data.

STEP 13: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 14: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

# CODING :

```
Developed by: Surya P
RegisterNumber:  212224230280

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# 1. Data Cleaning
df = pd.read_csv("supermarket.csv")
df['Date'] = pd.to_datetime(df['Date'])
df['Time'] = pd.to_datetime(df['Time'], format='%H:%M').dt.time
df_cleaned = df.drop(columns=['Invoice ID'])
df_cleaned = df_cleaned.drop_duplicates()

# 2. Boxplot Method to Detect Outliers
sns.set(style="whitegrid")
numerical_cols = ['Unit price', 'Quantity', 'Tax 5%', 'Total', 'cogs', 'gross income', 'Rating']

plt.figure(figsize=(16, 12))
for i, col in enumerate(numerical_cols, 1):
    plt.subplot(3, 3, i)
    sns.boxplot(data=df_cleaned, y=col)
    plt.title(f'Boxplot of {col}')
plt.tight_layout()
plt.show()

# 3. IQR Method to Remove Outliers
def remove_outliers_iqr(data, columns):
    for col in columns:
        Q1 = data[col].quantile(0.25)
        Q3 = data[col].quantile(0.75)
        IQR = Q3 - Q1
        lower = Q1 - 1.5 * IQR
        upper = Q3 + 1.5 * IQR
        data = data[(data[col] >= lower) & (data[col] <= upper)]
    return data

df_no_outliers = remove_outliers_iqr(df_cleaned.copy(), numerical_cols)
print("Original rows:", df_cleaned.shape[0])
print("After removing outliers:", df_no_outliers.shape[0])

# 4. Count Plot for Univariate Analysis (Categorical Variables)
categorical_cols = ['Branch', 'City', 'Customer type', 'Gender', 'Product line', 'Payment']

plt.figure(figsize=(18, 15))
for i, col in enumerate(categorical_cols, 1):
    plt.subplot(3, 2, i)
    sns.countplot(data=df_no_outliers, x=col)
    plt.title(f'Count Plot of {col}')
    plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# 5. DistPlot / PairPlot for Multivariate Analysis
sns.pairplot(df_no_outliers[numerical_cols])
plt.suptitle("Multivariate Analysis - Pairplot", y=1.02)
plt.show()

```

# OUTPUT : 

![image](https://github.com/user-attachments/assets/cc6da384-476d-43a9-a10c-5f654c915dc3)

![image](https://github.com/user-attachments/assets/70ef2ae1-9918-49ab-be0e-24005a4aaf15)

![image](https://github.com/user-attachments/assets/c0f3d010-e3ca-41f4-bab3-58ca63752461)

![image](https://github.com/user-attachments/assets/2e136c5e-7859-4810-a321-5f546eecf1dc)

![image](https://github.com/user-attachments/assets/c08b86fe-7f41-4fa0-9381-68c794a39147)

![image](https://github.com/user-attachments/assets/1e594886-ee3c-4c37-a8c3-529a2e71edf2)

# RESULT :

Thus, The given data is read and data cleaning process , outlier deduction and removal is performed successfully
