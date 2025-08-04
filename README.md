# cleaned-customer-personality-analysis-dataset
 A comprehensive data cleaning on a marketing campaign dataset is performed using python . It handles missing values, standardizes categorical fields, creates new features, and exports a clean CSV file for further analysis.
This project cleans and preprocesses a marketing campaign dataset for analysis .
gitclone 
## Features

- Handles missing values
- Standardizes categorical columns
- Converts dates and adds customer tenure
- Removes outliers and constant columns
- Adds new features like age, children, and total spending

## Files

- 'marketing_campaign.csv' : Original dataset ( from Kaggle )
- 'clean_script.py': Python script for cleaning
- 'marketing_campaign1.csv' : Output of cleaned data
- updated README.md # Project documentation (this file)

## Contributions
Contributions are welcome! Feel free to open issues or submit pull requests to enhance or expand the project.

The python code for following is :
import pandas as pd 
df = pd.read_csv("/content/marketing_campaign.csv" , sep='\t')
print(df.head()) 
print(df.isna().sum())
df['Income'] = df['Income'].replace(['n/a', 'none', 'na'], pd.NA)
print(df.dropna())
df.drop(columns=["Z_CostContact", "Z_Revenue"], inplace=True)
df.drop_duplicates()
df['Education'] = (df['Education'].str.replace(r'\s+', ' ', regex=True).str.strip().str.replace(r'[^\w\s]', '', regex=True))
df['Marital_Status'] = (df['Marital_Status'].str.replace(r'\s+', ' ', regex=True).str.strip().str.replace(r'[^\w\s]', '', regex=True))
df.sort_values(by='ID' , ascending =True , inplace = True)
print(df)
pd.to_datetime(df['Dt_Customer'], format='%d-%m-%Y')
df['Children'] = df['Kidhome'] + df['Teenhome']
expenses = ['MntWines', 'MntFruits', 'MntMeatProducts', 'MntFishProducts', 'MntSweetProducts', 'MntGoldProds']
df['TotalExpenses'] = df[expenses].sum(axis=1)
print("Number of complains = ",df['Complain'].sum())
print("Number of responses = ",df['Response'].sum())
df.to_csv("marketing_campaign1.csv", index=False)
