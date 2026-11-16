# Energy Consumption Prediction Using Linear Regression

## Project Overview

This project uses a **Linear Regression** model to predict building energy consumption. The notebook explores the dataset, prepares the input features, trains a regression model, and evaluates its predictions using numerical metrics and a visualization.

The target variable is **Energy Consumption**.

## Dataset

The notebook downloads the dataset from Kaggle using KaggleHub:

- **Dataset:** [Energy Consumption Dataset – Linear Regression](https://www.kaggle.com/datasets/govindaramsriram/energy-consumption-dataset-linear-regression)
- **Training file:** `train_energy_data.csv`
- **Testing file:** `test_energy_data.csv`

The dataset contains information about building type, square footage, number of occupants, appliances used, average temperature, day of the week, and energy consumption.

## Notebook Workflow

The notebook follows the steps below.

### 1. Importing Libraries

The notebook imports the Python libraries required for the project:

- **Pandas** for reading and handling tabular data.
- **NumPy** for numerical operations.
- **Matplotlib** and **Seaborn** for creating visualizations.
- **Warnings** to suppress warning messages during execution.

### 2. Loading the Dataset

The energy-consumption dataset is downloaded from Kaggle with KaggleHub. The training and testing CSV files are then loaded into separate Pandas DataFrames.

The first few rows of the training dataset are displayed to get an initial look at the data and its columns.

### 3. Understanding the Data

The notebook performs initial data inspection to understand the dataset:

- Checks the number of rows and columns in the training data.
- Displays column names, data types, and non-null counts.
- Checks both training and testing datasets for missing values.
- Checks the training dataset for duplicate rows.

These checks help determine whether the data has basic quality issues that need attention before modelling. The notebook's displayed results show no missing values and no duplicate rows in the training dataset.

### 4. Outlier Detection

Box plots are created for the numerical columns in the training dataset. These plots are used to visually inspect the distributions and identify possible outliers.

The notebook records the conclusion that no outliers were observed.

### 5. Encoding Categorical Columns

The dataset contains two categorical columns:

- `Building Type`
- `Day of Week`

Their unique values are inspected, and both columns are converted into numerical indicator columns using one-hot encoding. The original categorical columns are then removed from the training and testing DataFrames.

This step makes the categorical information suitable for use by the Linear Regression model.

### 6. Exploratory Data Analysis (EDA)

Exploratory Data Analysis is performed to understand the relationships between the input features and energy consumption.

Two types of visualizations are created:

- **Correlation heatmap:** Displays the correlations between the numerical features and helps identify relationships among variables.
- **Scatter plots:** Show the relationship between each numerical feature and the target variable, Energy Consumption.

Based on the heatmap and scatter plots, the notebook identifies **Square Footage** as highly correlated with Energy Consumption.

### 7. Preparing Features and Target

The `Energy Consumption` column is separated as the target variable. The remaining columns are used as input features.

The notebook uses the training and testing datasets supplied with the Kaggle dataset:

- The training features and target are used to train the model.
- The testing features and target are kept for evaluating model performance.

The notebook does not create a new random train-test split; it uses the two provided CSV files.

### 8. Feature Scaling

The numerical input features are standardized using `StandardScaler`.

The scaler is fitted on the training features, and the learned scaling is then applied to both the training and testing features. This puts the features on a comparable scale while ensuring that the test data does not determine the scaling parameters.

### 9. Model Training

A **Linear Regression** model from Scikit-learn is initialized and trained using the scaled training features and their corresponding energy-consumption values.

During training, the model learns the linear relationship between the input features and the target variable.

### 10. Model Evaluation

After training, the model predicts energy consumption for the test dataset. The predictions are compared with the actual test values using four evaluation metrics:

- **Mean Squared Error (MSE):** Measures the average squared difference between actual and predicted values. Lower values indicate smaller errors.
- **Mean Absolute Error (MAE):** Measures the average absolute difference between actual and predicted values. Lower values indicate better predictions.
- **Root Mean Squared Error (RMSE):** Measures prediction error in the same scale as the target variable. Lower values are better.
- **R² Score:** Indicates how much of the variation in energy consumption is explained by the model. A value closer to 1 indicates a stronger fit.

The saved notebook output reports the following results:

| Evaluation Metric | Result |
|---|---:|
| MSE | 0.0002015424 |
| MAE | 0.0121619012 |
| RMSE | 0.0141965634 |
| R² Score | 0.9999999997 |

The notebook describes the model's performance as excellent based on its R² score.

### 11. Graphical Evaluation

The final visualization compares actual energy-consumption values with the values predicted by the model.

- The horizontal axis represents actual energy consumption.
- The vertical axis represents predicted energy consumption.
- Each point represents a test observation.
- A diagonal reference line represents the ideal case where predicted values equal actual values.

Points closer to the diagonal line indicate predictions that are closer to the actual values. This plot provides a visual check of the model's performance on the testing data.

## Conclusion

The notebook completes an end-to-end energy-consumption prediction workflow using Linear Regression. It loads and inspects the dataset, checks for missing values and duplicates, examines potential outliers, encodes categorical features, explores feature relationships, scales the inputs, trains the model, and evaluates its predictions.

In the saved run, the model achieves an R² score of approximately **0.9999999997** on the supplied testing dataset. This indicates an extremely close fit on that test set. Further validation on an independent dataset would be useful before relying on the model for real-world predictions.

## Project Structure

    Unit 1  
    ├── RCA_Act_1.ipynb
    └── README.md

The dataset files are downloaded from Kaggle when the notebook is run, rather than being stored in the repository.

## Requirements

The notebook uses the following Python libraries:

- pandas
- numpy
- matplotlib
- seaborn
- kagglehub
- scikit-learn

Jupyter Notebook or JupyterLab is required to run the notebook.

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
