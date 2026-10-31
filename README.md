# 🏥 Mission Hospital Package Pricing Analysis Using R

## 1. Project Overview

This project analyzes hospital expenditure using **R and RStudio**. It explores the relationship between total hospital costs and factors such as length of hospital stay, intensive care unit (ICU) stay, implant costs, patient characteristics, and medical history.

The analysis applies data preprocessing, exploratory data analysis, correlation analysis, multiple linear regression, multicollinearity assessment, and cost prediction.

The primary objective is to understand the factors associated with hospital costs and develop a regression model to predict total hospital expenditure.

## 2. Project Objectives

* Clean and preprocess hospital data.
* Handle missing values in numeric variables.
* Encode categorical variables and create dummy variables.
* Explore relationships between numeric variables.
* Divide the dataset into training and testing subsets.
* Develop and compare multiple linear regression models.
* Assess multicollinearity using Variance Inflation Factor (VIF).
* Apply a logarithmic transformation to hospital costs.
* Generate predictions using the selected regression model.
* Compare predicted and observed costs visually.

## 3. Tools and Technologies

* **R:** Statistical computing and data analysis.
* **RStudio:** Environment for writing and executing R scripts.
* **Tidyverse:** Data manipulation and preprocessing.
* **fastDummies:** Dummy-variable creation.
* **corrplot:** Correlation matrix visualization.
* **caTools:** Training and testing data splitting.
* **psych:** Exploratory data analysis and correlation plots.
* **car:** Multicollinearity assessment using VIF.

## 4. Dataset and Variables

The dataset contains hospital cost information and patient-related variables.

Important variables include:

| Variable               | Description                                   |
| ---------------------- | --------------------------------------------- |
| Total Cost to Hospital | Target variable for cost prediction           |
| Total Length of Stay   | Total duration of hospital stay               |
| ICU Length of Stay     | Duration of stay in the intensive care unit   |
| Ward Length of Stay    | Duration of stay in the hospital ward         |
| Cost of Implant        | Cost associated with implants                 |
| Age                    | Patient age                                   |
| Creatinine             | Creatinine measurement                        |
| High Blood Pressure    | Blood pressure-related variable               |
| Heart Rate/Pulse       | Patient pulse measurement                     |
| Body Weight            | Patient body weight                           |
| BMI                    | Body Mass Index                               |
| Admission Type         | Type of hospital admission                    |
| Implant Used           | Indicates whether an implant was used         |
| Key Complaints         | Code representing the patient's key complaint |
| Past Medical History   | Code representing medical history             |
| Mode of Arrival        | Mode of arrival at the hospital               |

*Variable definitions should be confirmed using the original dataset documentation.*

## 5. Methodology

### Step 1: Data Loading and Exploration

The dataset is imported using `read.csv()`. The `summary()` function provides an initial overview of the variables and their distributions.

### Step 2: Missing-Value Treatment

Missing values in numeric columns are replaced with the corresponding column means.

### Step 3: Categorical Variable Encoding

Selected variables, including admission type and implant usage, are converted into binary numeric values.

### Step 4: Dummy-Variable Creation

Dummy variables are generated for key complaints, past medical history, and mode of arrival to represent categorical information numerically.

### Step 5: Correlation Analysis

A correlation matrix is calculated for numeric variables and visualized using `corrplot`. This helps explore relationships among variables.

### Step 6: Training and Testing Split

The dataset is divided into approximately 70% training data and 30% testing data using `caTools`. A random seed of 11 is used to make the split reproducible.

### Step 7: Logarithmic Transformation

The target variable, total hospital cost, is transformed using the natural logarithm. This approach can help address skewness and investigate non-constant variance.

### Step 8: Exploratory Data Analysis

The `pairs.panels()` function is used to examine relationships among selected variables before regression modeling.

### Step 9: Multiple Linear Regression

Twenty-three numbered model specifications are explored in the supplied script, although one model name is reused. Different combinations of predictors are evaluated using `lm()` and `summary()`.

### Step 10: Multicollinearity Assessment

Variance Inflation Factor (VIF) is calculated using the `car` package to assess relationships among regression predictors.

### Step 11: Prediction and Visualization

The selected Model 23 specification is used to generate predictions on the testing dataset. The code also produces plots to compare model residuals and predicted versus observed values.

## 6. Regression Results

The PDF report contains the results of multiple regression models.

### Model 1: Initial Regression Model

**Predictors:** ICU length of stay and total length of stay.

* R-squared: 62.77%
* Adjusted R-squared: 62.34%
* Residual standard error: 0.3196
* Overall model p-value: Less than 2.2 × 10⁻¹⁶

The initial model explains approximately 62.77% of the variation in the logarithm of hospital cost in the training data.

### Model 4: Adding Implant Cost and Age

* R-squared: 77.02%
* Adjusted R-squared: 76.48%
* Residual standard error: 0.2526

Adding implant cost and age increases the explanatory power compared with Model 1.

### Model 13: Adding Key Complaints

* R-squared: 83.47%
* Adjusted R-squared: 81.66%
* Residual standard error: 0.223
* Overall model p-value: Less than 2.2 × 10⁻¹⁶

Model 13 shows a stronger in-sample fit among the reported models highlighted here. However, it contains multiple categorical complaint levels, making it more complex than the initial model.

### Model 23: Selected Prediction Model

The final prediction section of the PDF uses Model 23.

**Predictors:**

* Age
* Ward length of stay
* Total length of stay
* Implant cost
* Heart rate/pulse
* Body weight
* Past medical history

Reported training results:

| Metric                  |        Result |
| ----------------------- | ------------: |
| R-squared               |        80.38% |
| Adjusted R-squared      |        78.77% |
| Residual standard error |        0.2399 |
| F-statistic             |          50.1 |
| Overall model p-value   | < 2.2 × 10⁻¹⁶ |

The model explains approximately 80.38% of the variation in log hospital costs in the training data. The adjusted R-squared is 78.77% after accounting for the number of estimated parameters.

The statistically significant overall F-test indicates that the model, considered as a whole, provides evidence of a relationship between the predictors and the transformed target variable.

**Important:** R-squared is an in-sample explanatory measure. It does not mean the model predicts hospital costs with 80.38% accuracy.

## 7. Interpretation of Model 23

The coefficient estimates help explain how individual predictors relate to log hospital costs while holding the other included variables constant.

| Predictor            | Coefficient |      P-value | Interpretation                                             |
| -------------------- | ----------: | -----------: | ---------------------------------------------------------- |
| Age                  |    0.000602 |     0.690625 | Not statistically significant at the 5% level              |
| Ward length of stay  |    -0.03718 |  4.81 × 10⁻⁷ | Statistically significant negative conditional association |
| Total length of stay |     0.07422 |  < 2 × 10⁻¹⁶ | Statistically significant positive association             |
| Implant cost         | 0.000009262 | 2.69 × 10⁻¹³ | Statistically significant positive association             |
| Heart rate/pulse     |    0.001096 |     0.364595 | Not statistically significant at the 5% level              |
| Body weight          |    0.002893 |     0.107035 | Not statistically significant at the 5% level              |

The past medical history variable is categorical, so its coefficients compare specific categories against a reference category.

For example, the `Diabetes2` category has a coefficient of approximately 0.3871 and a p-value of 0.000297. The `other` category has a coefficient of approximately -0.2445 and a p-value of 0.031245.

These results indicate conditional associations in the fitted model; they do not establish that a variable causes hospital costs to increase or decrease.

Because the target variable is log-transformed, coefficients should be interpreted on the log scale. Converting a coefficient into a percentage association requires exponentiation, and interpretation depends on the variable's units and the model assumptions.

## 8. Multicollinearity Results

For Model 23, the reported adjusted VIF values for the numerical predictors include:

| Predictor            |  VIF |
| -------------------- | ---: |
| Age                  | 4.79 |
| Ward length of stay  | 2.13 |
| Total length of stay | 2.43 |
| Implant cost         | 1.22 |
| Heart rate/pulse     | 1.79 |
| Body weight          | 5.22 |

For the categorical past medical history variable, the reported generalized VIF is 2.32 across seven degrees of freedom. Its adjusted value, `GVIF^(1/(2*Df))`, is approximately 1.06.

The results suggest that age and body weight deserve closer inspection for potential multicollinearity. The VIF values alone do not establish whether the regression assumptions are satisfied.

## 9. Testing Data Predictions

The PDF reports the following first six predictions from Model 23:

| Observation | Predicted log cost | Observed log cost |
| ----------- | -----------------: | ----------------: |
| 6           |           12.96734 |          12.82761 |
| 9           |           13.20720 |          12.98890 |
| 13          |           14.33053 |          13.47529 |
| 14          |           12.63198 |          12.94811 |
| 15          |           12.63808 |          13.11427 |
| 22          |           12.50184 |          12.57404 |

These values are on the logarithmic scale, not the original hospital-cost scale.

The PDF also includes a plot comparing predicted and observed values. However, it does not report a formal testing-set R-squared, Root Mean Squared Error (RMSE), or Mean Absolute Error (MAE).

Consequently, the model's out-of-sample predictive accuracy cannot be fully assessed from the reported values alone.

## 10. Key Findings

* Hospital stay duration and implant cost are important predictors in several reported models.
* Model 13 has a higher reported training R-squared than Model 23, but it also includes more categorical complaint levels.
* Model 23 provides a reported training R-squared of 80.38% and adjusted R-squared of 78.77%.
* In Model 23, total length of stay and implant cost have statistically significant positive coefficients.
* Ward length of stay has a statistically significant negative coefficient after controlling for the other included predictors.
* Age, heart rate/pulse, and body weight are not statistically significant at the 5% level in Model 23.
* The model produces testing-set predictions, but formal testing metrics are needed to assess predictive performance.

## 11. Limitations and Improvements

* Mean imputation may distort variable distributions and relationships.
* The supplied code does not formally evaluate every regression assumption.
* The numbered model definitions include a reused `model18` name, which overwrites an earlier model.
* The code creates dummy variables but generally uses the original categorical columns in the regression formulas.
* The testing-set prediction results are not summarized using RMSE or MAE.
* Predictions are on the logarithmic scale and must be transformed appropriately for interpretation in original cost units.
* Model selection should consider testing performance, model complexity, and statistical assumptions rather than R-squared alone.
* Healthcare data must be checked for confidentiality before publication.

## 12. Project Files

* **`Package Pricing at Mission Hospital.pdf`** — PDF report containing the R code, analysis, and reported results.
* **`Package Pricing at Mission Hospital - Data Supplement (2).xlsx`** — Supplementary data file.

The original `missionML.csv` dataset is required to run the supplied code unless the script is adapted to use another verified data source.

## 13. Conclusion

This project demonstrates the use of R for hospital cost analysis through data preprocessing, exploratory analysis, correlation analysis, multiple linear regression, multicollinearity assessment, and prediction.

The reported regression results indicate that length of stay and implant cost are associated with transformed hospital costs. Model 23 explains approximately 80.38% of the variation in log costs in the training data.

Further validation using formal testing metrics and regression diagnostics is necessary before using the model for real-world hospital pricing or financial decisions.

**Note:** The accompanying PDF contains the complete R code, analysis, and reported results.




