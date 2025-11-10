# 📘 Assignment – Ensemble Learning for Complex Regression Modeling on Bike Share Data

## Name: Krishna Chaitanya
## Roll No: DA25M011

## 📂 Submission Contents
submission.ipynb → The single notebook that contains all code, visualisations, and explanations for this assignment.

## 📌 Overview

The main goal of this assignment is to forecast **hourly bike rental counts** using the [UCI Bike Sharing Dataset](https://archive.ics.uci.edu/ml/datasets/bike+sharing+dataset), which consists of over **17,000 hourly records** influenced by factors such as **weather**, **season**, **temperature**, and **time of day**.

The objective is to **accurately predict the total number of rentals (`cnt`)** by applying and comparing multiple **ensemble regression techniques** to minimize **Root Mean Squared Error (RMSE)**.

We explored and compared the following five models:

1. **Linear Regression**
2. **Decision Tree Regerssor**
3. **Bagging Regressor** 
4. **Gradient Boosting Regressor** 
5. **Stacking Regressor**

## Methodology
### 1. Data Loading and Feature Engineering

- After loading the dataset using **pandas** library first step is to **drop** the irrelevant columns (`instant, dteday, casual, and registered.`)
-  Didnt check for null values as mentioned in data description there are no missing valaues
- And there are categorical variables in the dataset (`eason', 'yr', 'mnth', 'hr', 'holiday', 'weekday', 'workingday', 'weathersit`) These are converted into **numerical** features using **OneHot Encoding**

### 2 Train Test Split
- After obtaining the clean and processed data from `step-1` splitted the preprocessed data into training and testing sets using `train_test_split` library from sklearn

### 3 Baseline Model
- After splitting into train and test we evaluated 2 models 
