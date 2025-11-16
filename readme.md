
## 1. Project Overview

This deliverable focuses on developing and evaluating regression models to predict **Billing Amount** using the cleaned healthcare dataset from Deliverable 1. The work includes:

- Feature engineering  
- Data preprocessing  
- Two regression models: Linear Regression and Ridge Regression  
- Model evaluation using R², MSE, RMSE, MAE  
- **5-fold cross-validation** on a 2,000-row sample  
- Diagnostic visualizations  
- Final performance summary and interpretation  

The goal is to demonstrate practical predictive modeling using supervised learning on real healthcare data.

---

## 2. Dataset Summary

The dataset contains over **10,000 simulated patient records** with attributes such as:

- Age, Gender, Blood Type  
- Medical Condition, Medication, Doctor  
- Hospital, Insurance Provider  
- Room Number  
- Date of Admission, Discharge Date  
- Billing Amount (target)

These variables capture both clinical and operational factors that influence healthcare costs, making the dataset suitable for regression modeling.

---

## 3. Feature Engineering

To enhance predictive power, the following features were engineered:

### Engineered Features
- **Length_of_Stay**: Difference between Discharge Date and Admission Date  
- **Admission Year**  
- **Admission Month**  
- **Top-K Category Reduction**: High-cardinality columns (Hospital, Doctor, Medication, etc.) reduced to top 10 values + “Other”

### Preprocessing Steps
- Median imputation for numeric values  
- Most frequent imputation for categorical values  
- Standardized numeric variables  
- One-hot encoding for categorical variables  
- Dropped raw date columns after extracting engineered features  

This approach produced a finalized dataset ready for modeling.

---

## 4. Models Developed

Two regression models were created:

### Linear Regression
- Serves as the baseline model  
- Highly interpretable  
- Very fast to train  

### Ridge Regression
- Regularized linear model  
- Handles high-dimensional encoded features better  
- Reduces coefficient magnitude to mitigate overfitting

**Note:** Lasso Regression was intentionally excluded due to severe computation time and repeated crashes during experimentation. Ridge Regression offered similar benefits with much faster performance.

---

## 5. Model Evaluation

Models were evaluated using the following metrics:

- **R² Score**  
- **Mean Squared Error (MSE)**  
- **Root Mean Squared Error (RMSE)**  
- **Mean Absolute Error (MAE)**  

A results table was used to compare model performance side-by-side.

### Diagnostic Visualizations
To assess fit quality, the following were plotted for the best model:

- Predicted vs Actual Billing Amount  
- Residuals vs Predicted  
- Residual distribution histogram  

These visualizations helped identify variance structure, outlier behavior, and potential heteroscedasticity.

---

## 6. Cross-Validation (5-Fold on 2,000-Row Sample)

Full dataset cross-validation was not computationally practical due to:

- Long run times  
- CPU overheating  
- Kernel restarts  

### Final Approach
A **2,000-row sample** was used for efficient cross-validation.

- **5-fold cross-validation** provided reliable generalization performance estimates  
- R² mean and standard deviation were computed for both models  
- A boxplot of fold performance visualized score variability  

This satisfies assignment requirements while remaining computationally safe.

---

## 7. Key Insights and Observations

### Model Performance
- **Ridge Regression** outperformed Linear Regression on both test-set performance and 5-fold CV.
- Regularization gave Ridge improved stability across folds.

### Feature Importance
Important predictors included:

- Length_of_Stay  
- Frequently occurring Medical Conditions  
- High-frequency Hospitals  

### Residual Behavior
- Residuals were centered around zero but exhibited mild heteroscedasticity.
- Suggests nonlinear models (Random Forest, Gradient Boosting) could improve predictive accuracy.

### Generalization
- Ridge Regression had lower variance across CV folds, indicating better generalization.
- Linear Regression was more sensitive to multicollinearity and categorical expansion.

---

## 8. Challenges Encountered & Resolutions

Several challenges were encountered throughout model development:

### 1. Lasso Regression Extremely Slow  
- Running Lasso caused 10+ minute fits, freezing the notebook.  
**Resolution:** Removed Lasso entirely.

### 2. GridSearchCV Causing System Freezes  
- Full hyperparameter tuning repeatedly froze execution.  
**Resolution:** Removed GridSearchCV; used fixed α for Ridge.

### 3. Undefined Variable Errors After Model Removal  
- Removing Lasso left behind references (`pipe_lasso`, `y_pred_lasso`).  
**Resolution:** Cleaned all affected tasks and visualizations.

### 4. Preprocessor Not Defined  
- Running Task 4 before Task 3 caused `preprocessor is not defined`.  
**Resolution:** Ensured correct execution order.

### 5. OneHotEncoder Deprecation  
- `sparse=False` raised warnings.  
**Resolution:** Updated to `sparse_output=False`.

### 6. Full Cross-Validation Too Heavy  
- 5-fold CV on full dataset overwhelmed system resources.  
**Resolution:** Used **5-fold CV on a smaller 2,000-row sample**.

---

## 9. Final Conclusion

Ridge Regression proved to be the best-performing model for predicting healthcare billing amounts in this dataset. While overall predictive power was moderate, the workflow provided robust feature engineering, rigorous evaluation, and reproducible modeling steps.

Future modeling improvements could explore:

- Random Forests or Gradient Boosting  
- Log-transforming Billing Amount  
- Incorporating domain-specific cost drivers  

This deliverable successfully demonstrates core regression modeling concepts and effective use of cross-validation under computational constraints.

---

## 10. Repository Contents

- `Deliverable_2.ipynb` — Full regression modeling notebook  
- `README.md` — Summary of approach, insights, and challenges  
- `model_evaluation_results.csv`  
- `ridge_coefficients.csv`  
- `best_model_pipeline.pkl`  

