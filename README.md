# Analysis-DataSet
Automated Data Acquisition and Initial Analysis of the Titanic Dataset in Google Colab

Automated Data Acquisition, Cleaning, and Initial Analysis of the Titanic Dataset in Google Colab
Objective: To demonstrate the process of automating data download from Kaggle, cleaning the dataset, and performing initial analysis using Google Colab.

Steps and Description
Step 1: Install Kaggle API
The first step involves installing the Kaggle API, which is essential for downloading datasets directly from Kaggle to your Google Colab environment.

python
Copy code
!pip install kaggle
Step 2: Upload Kaggle API Credentials
To authenticate and use the Kaggle API, you need to upload your kaggle.json file, which contains your API credentials. This file should be manually uploaded to your Colab environment.

python
Copy code
import os
os.makedirs('/root/.kaggle', exist_ok=True)
!mv kaggle.json /root/.kaggle/
!chmod 600 /root/.kaggle/kaggle.json
Step 3: Download the Titanic Dataset
Using the Kaggle API, you can download the Titanic dataset. The dataset file is then unzipped for use.

python
Copy code
# Download the Titanic dataset
!kaggle competitions download -c titanic -f train.csv

# Unzip the downloaded file
!unzip train.csv.zip
Step 4: Load and Clean the Dataset
Load the dataset into a pandas DataFrame and perform essential data cleaning steps, including handling missing values, encoding categorical data, and dropping unnecessary columns.

Load the Dataset:

python
Copy code
import pandas as pd

# Load the dataset
df = pd.read_csv('train.csv')
print("Initial DataFrame:")
print(df.head())
Handle Missing Values:

python
Copy code
# Check for missing values
print("\nMissing values before cleaning:")
print(df.isnull().sum())

# Fill missing values for 'Age' with the median
df['Age'].fillna(df['Age'].median(), inplace=True)

# Fill missing values for 'Embarked' with the mode
df['Embarked'].fillna(df['Embarked'].mode()[0], inplace=True)

# Drop the 'Cabin' column due to a high number of missing values
df.drop(columns=['Cabin'], inplace=True)
Handle Categorical Data:

python
Copy code
# Convert 'Sex' to numerical values
df['Sex'] = df['Sex'].map({'male': 0, 'female': 1})

# Convert 'Embarked' to numerical values
df['Embarked'] = df['Embarked'].map({'S': 0, 'C': 1, 'Q': 2})
Drop Unnecessary Columns:

python
Copy code
# Drop columns that are not useful for prediction
df.drop(columns=['Name', 'Ticket', 'PassengerId'], inplace=True)

print("\nCleaned DataFrame:")
print(df.head())

print("\nMissing values after cleaning:")
print(df.isnull().sum())
Step 5: Initial Analysis
Conduct initial analysis to understand the dataset better. This includes generating summary statistics and visualizing data distributions and relationships.

Summary Statistics:

python
Copy code
print("\nSummary Statistics:")
print(df.describe())
Visualizations:

Distribution of Age:

python
Copy code
import matplotlib.pyplot as plt
import seaborn as sns

# Distribution of Age
plt.figure(figsize=(10, 6))
sns.histplot(df['Age'], bins=30, kde=True)
plt.title('Age Distribution')
plt.xlabel('Age')
plt.ylabel('Frequency')
plt.show()
Survival Rate by Sex:

python
Copy code
# Survival rate by sex
plt.figure(figsize=(10, 6))
sns.barplot(x='Sex', y='Survived', data=df)
plt.title('Survival Rate by Sex')
plt.xlabel('Sex')
plt.ylabel('Survival Rate')
plt.show()
Survival Rate by Embarked:

python
Copy code
# Survival rate by Embarked
plt.figure(figsize=(10, 6))
sns.barplot(x='Embarked', y='Survived', data=df)
plt.title('Survival Rate by Embarked')
plt.xlabel('Embarked')
plt.ylabel('Survival Rate')
plt.show()
Summary
This tutorial demonstrates the full process of automating data acquisition from Kaggle, cleaning the dataset, and performing initial data analysis in Google Colab. It emphasizes the importance of clean data for accurate analysis and prepares the data for further exploration and modeling.
