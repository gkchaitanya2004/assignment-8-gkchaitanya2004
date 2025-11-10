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
- After splitting into train and test, we trained 2 models (**Linear Regression** and **Decision Tree Regerssor**) on the training data and evaluated their performance on the test data set
- Here are their **RMSE**
| Model                        | RMSE   |
|------------------------------|--------|
| Decision Tree Regressor      | 118.46 |
| Linear Regressor| 100.45 |


### 4 Ensemble Techniques For Bias and Variance Reduction
- I used **Bagging** and **Boosting** to respective check how reduction in **variance and bias** and here are the results :
| Model                        | RMSE   |
|------------------------------|--------|
| Decision Tree Regressor      | 118.46 |
| Gradient Boosting Regressor  | 78.97  |
| Bagging Regressor| 112.27 |


### 5 Comparison of Bagging Vs Single Decision Tree vs Boosting
- - We can see that the **Bagging Regressor** has significantly low RMSE when compared to **Decision Tree Regressor**

- This is because the single decision tree is known for its **high variance** even a small change in data the tree will change its structure drastically

- Bagging reduces this by **averaging predictions** from many trees trained on slightly different random samples.

- The averaging process effectively reduces the variance leading to a more robust model that generalizes better, which results in a **low RMSE**

- This Single Decision Tree suffered from high variance, which Bagging helped reduce by averaging. However the drop was not too significant. This suggests the base model also suffered from high **bias**.

- Boosting effectively reduced bias by sequentially training multiple weak learners, where each tree focused on correcting the errors made by the previous ones.

- As a result, the bias of the model was reduced, leading to a more robust model that generalises better, which results in a **low RMSE**.

### 6 Stacking for Optimal Performance
- - **Stacking** is an **ensemble** learning technique where **multiple diverse models** are trained on the same dataset and then a **meta learner** is trained to combine their predictions in an optimal way

**How Stacking Works ??**

- First we will train several models independently on the training data.

- Each model or **base learner** predicts outputs. These predictions are then used as features to train another model (**meta-learner**).

- Its jobs is to learn the **best possible** way to combine the predictions from the base-learners.

**How the Meta-Learner Combines Predictions ??**

- The meta-learner takes the predictions from all base models as inputs and learns weights for each.

- For example in above models bosting performed better so it will assign a **higher weight** to the Boosting model's predictions.

- Essentially it is learning an **optimal way** to combine all precidiction using those weights it learn so that it minimizes the **final prediction error**.

## Final Analysis

### Comparative Table
| Model                        | RMSE   |
|------------------------------|--------|
| Stacking Regressor | 67.05
| Gradient Boosting Regressor  | 78.97  |
| Linear Regressor      | 100.45 |
| Bagging Regressor| 112.27 |


### Conclusion

- The best performing model is **Stacking Regressor** it achieved a RMSE of **67.05**.

**The Bias Variance TradeOff**
- The Baseline Linear Regression model has **high bias** and **low variance**. It It captures only linear relationships which limits its ability to identify **non-linear patterns** in the data.

- The **Bagging Regressor** helped in reducing variance by averaging predictions from multiple Decision Trees.However since all base learners were similar (Decision Trees with depth 6)it did not significantly reduce bias which is why the improvement was modest.

- The **Gradient Boosting Regressor**  effectively reduced bias by sequentially training multiple weak learners, where each tree focused on correcting the errors made by the previous ones. This approach significantly improved accuracy compared to both the single and bagged models as it gradually minimized the systematic errors. But it can be prone to **overfitting** because continues to learn and correct even very small residual errors including the **noise** in the training data.

- In contrast **Stacking Regressor** combines multiple models(base learners) and combining their results in an **optimal way** using meta learners

- By this approach we ensuring model diversity and leverages strengths of base learners while minimizing their errors.

- This helps to model to capture both linear and non-linear relationship resulting in a more generalized model and also its helps in finding the best overall **bias-variance trade-off**.

- As a result Stacking Regressor achieved the lowest RMSE 



