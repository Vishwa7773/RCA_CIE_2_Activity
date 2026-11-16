# Loan Approval Prediction

## Project Overview

This project builds a **binary classification model** to predict whether a loan application will be approved or rejected. The target variable is `loan_status`, and the notebook uses applicant information such as age, income, employment experience, loan details, credit history, and credit score to make predictions.

The workflow covers data loading, data inspection, outlier investigation and filtering, categorical encoding, exploratory data analysis, feature scaling, Logistic Regression model training, and model evaluation.

## Dataset

The notebook downloads the dataset from Kaggle using KaggleHub:

- **Dataset:** [Loan Approval Classification Data](https://www.kaggle.com/datasets/taweilo/loan-approval-classification-data)
- **File used:** `loan_data.csv`
- **Initial size:** 45,000 rows and 14 columns

### Features in the dataset

The dataset contains the following applicant and loan attributes:

- `person_age`
- `person_gender`
- `person_education`
- `person_income`
- `person_emp_exp`
- `person_home_ownership`
- `loan_amnt`
- `loan_intent`
- `loan_int_rate`
- `loan_percent_income`
- `cb_person_cred_hist_length`
- `credit_score`
- `previous_loan_defaults_on_file`

The target column is `loan_status`, which represents the loan decision.

## Notebook Workflow

### 1. Importing libraries

The notebook imports the libraries required for data manipulation, numerical operations, visualization, and analysis:

- **Pandas** and **NumPy** for working with tabular and numerical data.
- **Matplotlib** and **Seaborn** for charts and visual analysis.
- **Warnings** to suppress warning messages during execution.

### 2. Loading the dataset

The dataset is downloaded from Kaggle using `kagglehub`. The `loan_data.csv` file is then loaded into a Pandas DataFrame. A copy of the original data is created for further processing.

### 3. Understanding the data

The notebook performs initial checks to understand the dataset:

- Checks the number of rows and columns.
- Checks each column's data type and non-null count.
- Counts missing values in every column.
- Checks for duplicate records.

**Findings from the notebook:**

- The dataset initially contains 45,000 rows and 14 columns.
- No missing values are reported.
- No duplicate records are reported.
- The columns include numerical and categorical features.

### 4. Detecting and treating outliers

Boxplots are created for the numerical columns to visually inspect their distributions and identify potential extreme values.

The notebook then applies domain-based filters to three columns:

- **`person_age`:** Records with an age above 70 are removed.
- **`person_emp_exp`:** Records with employment experience above 40 years are removed.
- **`cb_person_cred_hist_length`:** Records with a credit history length above 20 years are removed.

The dataset sizes shown after each filter are:

| Stage | Rows remaining |
|---|---:|
| Initial dataset | 45,000 |
| After age filter | 44,985 |
| After employment experience filter | 44,935 |
| After credit history filter | 44,739 |

A distribution plot is also created for each numerical feature, using `loan_status` to distinguish the two target classes. This helps inspect how feature values are distributed across loan outcomes.

### 5. Encoding categorical columns

Machine learning models require numerical inputs, so the notebook identifies the columns with the `object` data type and converts them into numerical indicator columns using **One-Hot Encoding**.

The encoding uses `drop_first=True`, which drops one category from each encoded feature to avoid retaining a redundant reference category.

The original categorical columns are removed after the encoded columns are added to the DataFrame.

### 6. Exploratory Data Analysis (EDA)

The notebook explores relationships between the processed features using:

- **Correlation heatmap:** Displays the pairwise correlations between numerical and encoded features.
- **Correlation distribution plot:** Visualizes the distribution of correlation values.

The notebook's observation is that the correlations are concentrated near zero.

### 7. Separating features and target

The dataset is divided into:

- **Features (`X`):** All columns except `loan_status`.
- **Target (`y`):** The `loan_status` column, which the model is trained to predict.

### 8. Train-test split

The data is split into training and testing sets using `train_test_split`:

- **Training set:** 75% of the data.
- **Testing set:** 25% of the data.
- **Random state:** 42, to make the split reproducible.

The training set is used to fit the model, while the testing set is used to evaluate its performance on unseen records.

### 9. Feature scaling

The notebook applies **StandardScaler** to standardize the input features.

- The scaler is fitted on the training features.
- The fitted scaler transforms the training features.
- The same fitted scaler transforms the test features.

This ensures that the test data is scaled using the training data's mean and standard deviation, rather than calculating separate scaling parameters for the test set.

### 10. Model training

A **Logistic Regression** classifier from Scikit-learn is created and trained using the scaled training features and their corresponding `loan_status` labels.

Logistic Regression is used because the task is a binary classification problem: predicting one of two loan outcomes.

### 11. Model evaluation

The trained model predicts loan outcomes for the test set. The notebook evaluates these predictions using three classification metrics:

| Metric | Result | Meaning |
|---|---:|---|
| Accuracy | 0.8986 (89.86%) | Proportion of all test predictions that are correct. |
| Precision | 0.7918 (79.18%) | Of the applications predicted as class 1, the proportion that actually belong to class 1. |
| Recall | 0.7486 (74.86%) | Of the actual class 1 applications, the proportion correctly identified by the model. |

These values are the results recorded in the notebook. Accuracy gives an overall measure of correctness, while precision and recall provide additional information about performance on the positive class.

### 12. Confusion matrix

A confusion matrix is calculated from the actual and predicted test labels and displayed as a Seaborn heatmap.

It summarizes predictions in four groups:

- **True Negative (TN):** Class 0 correctly predicted as class 0.
- **True Positive (TP):** Class 1 correctly predicted as class 1.
- **False Positive (FP):** Class 0 incorrectly predicted as class 1.
- **False Negative (FN):** Class 1 incorrectly predicted as class 0.

The notebook's written observation highlights the number of true negatives and true positives as evidence of model performance.

## Results and Conclusion

The Logistic Regression model achieves approximately **89.86% accuracy** on the test set, with **79.18% precision** and **74.86% recall** for the positive class.

The notebook concludes that the model performs well based on these evaluation results. However, accuracy alone does not fully describe a loan approval classifier. Precision and recall should also be considered, particularly because false approvals and missed approvals can have different practical consequences.

For a more complete assessment, the model could also be evaluated using an F1-score, ROC-AUC, and class-wise metrics. The decision about which metric matters most should depend on the cost of false positives and false negatives in the loan approval process.

## Tools and Libraries

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- KaggleHub
- Scikit-learn
- Jupyter Notebook

## How to Run the Notebook

1. Clone or download this repository.
2. Open the project in Jupyter Notebook or JupyterLab.
3. Install the libraries listed above if they are not already installed.
4. Run the notebook cells in order.
5. The notebook downloads the dataset through KaggleHub, so ensure that your environment can access Kaggle and that any required Kaggle authentication is configured.

## Project Structure

```text
Unit2
├── RCA_Act_2.ipynb
└── README.md
```

## Notes

- The outlier filters are based on the thresholds chosen in the notebook; they are not a general rule that all extreme values should be removed.
- The notebook uses a random train-test split and fits the scaler on the training data only.
- The reported evaluation metrics are based on the test split created in the notebook.

## Acknowledgement   
This project was created as a part of CIE 2 Activity of Unit 1 for the subject "Regression and Classfication Algorithms".   
**Course Faculty :** Mr. Deepanshu Sagar  
**Faculty Git hub:** [Mr. Deepanshu's git hub](https://github.com/complexiota)  

## Author 
**Name :** Vishwajeet Baing  
**Class :** TY AI-DS A  
**Roll Number :** AD3110  
**Course :** Regression and Classification Algorithms  
**Activity :** CIE 2, Unit 1: Linear Regression Algorithm

