# EXNO2DS
# AIM:
      To perform Exploratory Data Analysis on the given data set.
      
# EXPLANATION:
  The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.
  
# ALGORITHM:
STEP 1: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 2: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 3: Use boxplot method to analyze the outliers of the given dataset.

STEP 4: Remove the outliers using Inter Quantile Range method.

STEP 5: Use Countplot method to analyze in a graphical method for categorical data.

STEP 6: Use displot method to represent the univariate distribution of data.

STEP 7: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 8: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

## CODING AND OUTPUT
    import pandas as pd 
    import numpy as np 
    import seaborn as sns 
    import matplotlib.pyplot as plt 

    data = pd.read_csv("titanic_dataset.csv") 
    df=pd.DataFrame(data)
    df
<img width="1370" height="479" alt="{7FF72FEF-4EB5-4FCF-A830-85E9B57F8FEE}" src="https://github.com/user-attachments/assets/238b5700-1c42-402b-a7c7-ad402f6feb67" />

    sns.heatmap(df.isnull())
<img width="904" height="638" alt="{ACC567C0-7FDE-47FA-B6C6-4CB3F88B3C09}" src="https://github.com/user-attachments/assets/21bf8b17-54c8-47b6-b880-16efea6f9b95" />

    df.isnull().sum()
<img width="385" height="283" alt="{1FDAD843-B06C-49C3-97AB-57589DB57B72}" src="https://github.com/user-attachments/assets/41425114-e7ad-4956-a709-7a84e52e212f" />

# Use mean for numeric and mode for categorical values 
    for column in df.columns: 
        if df[column].dtype == 'object': 
            df[column] = df[column].fillna(df[column].mode()[0])  # Fill with mode 
        else: 
           df[column] = df[column].fillna(df[column].mean())  # Fill with mean 
 
    print(" Missing values handled.") 
    df
<img width="1359" height="566" alt="{31623345-16D3-4114-86B8-7975514775E5}" src="https://github.com/user-attachments/assets/0ae373cf-36b7-4651-800c-585b37f670a8" />

    sns.boxplot(x=df['Age'])
    plt.title("Boxplot - Salary")
    plt.xlabel("Salary")
    plt.show()
<img width="1117" height="558" alt="{303F1FC0-9FB8-4809-9AF0-54F3CD6CEF63}" src="https://github.com/user-attachments/assets/f5b000a2-baee-441f-9eda-94eca86dc2e8" />

    def remove_outliers_iqr(df, column): 
        Q1 = df[column].quantile(0.25) 
        Q3 = df[column].quantile(0.75) 
        IQR = Q3 - Q1 
        lower = Q1 - 1.5 * IQR 
        upper = Q3 + 1.5 * IQR 
        return df[(df[column] >= lower) & (df[column] <= upper)] 
 # Apply IQR method on 'Age' 
    data = remove_outliers_iqr(df, 'Age') 
    print("Outliers removed using IQR method.")

    sns.countplot(x='Embarked', data=df) 
    plt.title("Countplot - Embarked Distribution") 
    plt.show()
<img width="940" height="577" alt="{98D8BA13-3105-49F9-A3D6-A644A9A109B5}" src="https://github.com/user-attachments/assets/e66ef870-198a-41fc-acb7-27772748503f" />

    sns.displot(data['Age'], kde=True)
    plt.title("Displot - Age Distribution")
    plt.xlabel("Age") 
    plt.ylabel("Frequency") 
    plt.show() 
<img width="994" height="642" alt="{A9EA7F40-51C6-4D4A-95C7-C784B8F19691}" src="https://github.com/user-attachments/assets/78e4ec0c-788b-4ef3-bb6d-8545f1eefbac" />

    crosstab_result = pd.crosstab(df['Pclass'], df['Sex']) 
    print("\nCross Tabulation Result:") 
    print(crosstab_result) 
<img width="346" height="159" alt="image" src="https://github.com/user-attachments/assets/01fc5dfa-346b-46e9-affd-c999236eac82" />

    correlation_matrix = data.corr() 
    sns.heatmap(correlation_matrix, annot=True ) 
    plt.title("Correlation Heatmap") 
    plt.show()
<img width="1001" height="621" alt="{09B12762-67CA-40BD-AA61-00DB63D22371}" src="https://github.com/user-attachments/assets/b3f9ade2-0d1c-4365-a63c-ec40422028ae" />

# RESULT
        Thus the program to implement the exploratory data analysis has been succesfully completed
