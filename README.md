# Telco-Customer-Churn-Prediction
This project focuses on predicting customer churn using the **Telco Customer Churn** dataset. It involves comprehensive exploratory data analysis (EDA), feature engineering, model training, and performance evaluation.

---

## Dataset Used

**Telco Customer Churn Dataset**  
- Source: Kaggle  
- Records: 7,043 customers  
- Features: Demographics, account information, services subscribed, and churn status  
- Target: `Churn` (1 = customer left, 0 = customer stayed)

---

## Project Workflow

1. **Data Cleaning**  
   - Handled missing values  
   - Converted data types (e.g., `TotalCharges`)  
   - Encoded categorical variables  

2. **Exploratory Data Analysis (EDA)**  
   - Univariate, bivariate & multivariate analysis  
   - Correlation heatmaps  
   - Derived insights like average tenure, revenue distribution

3. **Feature Engineering**  
   - Created new features to improve model understanding  
   - Normalized and encoded additional patterns  

4. **Model Training**  
   - Logistic Regression classifier  
   - Evaluated using accuracy, confusion matrix, and classification report

---

## Results (Logistic Regression)

| Metric            | Value |
|-------------------|-------|
| Accuracy Score    | 81.76% (initial) / 80.69% (with feature engineering) |
| Precision (Churn) | ~0.68 |
| Recall (Churn)    | ~0.59 |
| F1-Score (Churn)  | ~0.63 |


## Insights

- **Model Training Without Feature Engineering:**
  - High precision for class 0: Model is confident when predicting no churn.
  - Lower recall for class 1: It's missing a lot of churners — that’s where the improvement lies.
  - We’re catching most of the non-churners, but a decent number of churners are slipping through.
  - The model correctly predicted customer churn or non-churn 82 out of every 100 times (81.76 % accuracy).
- **Dataset Information:**
  - 7043 customers (rows) and 31 features (columns)
  - Target variable is 'Churn' (0 or 1)
  - Numerical features are 'tenure', 'MonthlyCharges', and 'TotalCharges'
  - No null values are to be found
  - Categorical features encoded as booleans found - 'Contract_One year', 'gender_Male', 'StreamingTV_Yes', etc.
- **Insights - Tenure:**
  - Average tenure is 32.37 months, meaning roughly 3 years
  - The std (standard deviation) is 24.56, which is quite large. This means there is a lot of variability in how long customers have been with the company.
  - The minimum tenure is 0 months, which means some customers just joined or perhaps canceled immediately.
  - The maximum tenure is 72 months, meaning the longest a customer has been with the company is 6 years.
  - 25% of the customers have been with the company for 9 months or less, the median tenure is 29 months, and 75% of the customers have been with the company for less than 55 months.
  - Customers with shorter tenures are at a higher risk of churn.
- **Insights - MonthlyCharges**
  - The average MonthlyCharge is 64.76
  - The standard deviation is 30.09, indicating a good range of values
  - The minimum monthly charge is 18.25, which likely corresponds to the basic plan or possibly a free trial
  - The maximum monthly charge is 118.75, which is likely a premium plan
  - 25% of customers pay 35.50 or less per month, the median monthly charge is 70.35, and 75% of the customers pay less than 89.85 monthly
  - High Monthly Charges might be correlated with higher churn, depending on whether customers feel they are getting value for money.
- **Insights - TotalCharges**
  - The average TotalCharges is 2281.92
  - A standard deviation of 2265.27 means there's a lot of variation in the total money customers have paid.
  - The minimum value is 18.80, suggesting that some customers are very new
  - The maximum value is 8684.80, which is likely someone who has been with the company for a long time and possibly on a premium or high-value plan.
  - 25% of the customers have paid 402.23 or less, the median total charge is 1397.48, and 75% of customers have paid less than 3786.60 in total.
  - A low total charge could correlate with newer customers or customers on cheaper plans, while higher total charges could suggest longer-term customers.
- **Insights - Contract_One year**
  - The most frequent value is False, meaning most customers don’t have a one-year contract.
  - Most customers seem to be on month-to-month contracts, which suggests they may have more flexibility and may be more likely to churn.
- **Insights - gender_Male**
  - The most frequent value is True, meaning there are more male customers than female customers.
  - There’s a slight male dominance in the dataset, but the gender distribution is quite balanced.
- **Bivariate Analysis:**
  - The central tendency (median) of no churn is higher compared to the other.
  - Long whiskers of churn as yes indicate a wide spread of values and possible outliers, while the short whiskers of no churn suggest that the values are more concentrated around the median.
  - Genders are well-balanced.
  - Customers without any contract type are more numerous. But in both types, the ones with no churn are more.
  - tenure vs totalCharges shows a strong positive correlation (loyal customers tend to contribute more revenue over time)
  - monthlycharges vs totalcharges shows a moderate positive correlation (customer might pay a high monthly charge but still be new)
  - tenure vs monthlycharges shows a weak positive correlation (even long-tenure customers might have low monthly plans, or vice versa)
- **Feature Engineering:**
  - AvgChargesPerMonth: We'll calculate this only where tenure > 0 to avoid division by zero.
  - SeniorAlone: This will be 1 if the person is a senior citizen and has neither a partner nor dependents.
  - Churned users have lower average tenure, which means they tend to leave early, suggesting the first few months are crucial.
  - Loyal customers have higher revenue, which confirms that retaining customers boosts revenue.
  - High churn in specific services (like fiber optic or month-to-month contracts) can guide retention strategies — maybe those plans need better onboarding or customer support.
- **After Feature Engineering:**
  - You added derived or one-hot encoded features (more columns), maybe introduced multicollinearity or sparse info.
  - Accuracy: 80.69%
  - Recall for churn class (1): 0.56 (slightly down)
  - Here, although feature engineering gave more data to work with, not all added features may have been useful or necessary for Logistic Regression. 
  - Introduced correlation (like multiple "No internet service" features).
  - Added sparsity due to binary one-hot encoded columns.
  - Possibly caused overfitting or underfitting if not scaled well.
