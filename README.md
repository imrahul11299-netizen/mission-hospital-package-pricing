# Mission Hospital Package Pricing Analysis Using R

**Academic project | Data Analytics Programme, IIM Sirmaur × Masai**

## Overview

This project explores hospital expenditure and its relationship with variables such as length of stay, ICU stay, implant costs, and selected patient characteristics. R and RStudio were used for data preparation, exploratory analysis, regression modelling, and cost prediction.

## Business Question

Which recorded factors are associated with hospital expenditure, and how can a regression model be assessed for estimating costs from the available data?

## Objectives

- Inspect and clean the hospital-cost dataset.
- Explore distributions and relationships between variables.
- Encode categorical variables for analysis.
- Examine correlations and potential multicollinearity.
- Fit and compare multiple linear regression specifications.
- Explore a log transformation of the cost target.
- Compare predicted and observed costs.

## Repository Files

- `Package Pricing at Mission Hospital.pdf` — project report and documented analysis.
- `Package Pricing at Mission Hospital - Data Supplement (2).xlsx` — accompanying data supplement.

Check the source, permission, and privacy status of all data before sharing or reusing it. Do not publish identifiable patient information.

## Tools and Techniques

- R and RStudio
- Tidyverse
- `fastDummies`
- `corrplot`
- `caTools`
- `psych`
- `car` for Variance Inflation Factor (VIF) assessment
- Exploratory Data Analysis (EDA)
- Correlation analysis
- Multiple linear regression

## Methodology

1. Load the data and review its structure and summary statistics.
2. Inspect missing values and prepare variables.
3. Encode selected categorical variables and create dummy variables.
4. Explore numeric relationships using correlation analysis and visualizations.
5. Split the data into training and test subsets (the documented workflow uses approximately 70:30 and a fixed random seed).
6. Explore a logarithmic transformation of the cost target.
7. Fit and compare multiple linear regression specifications.
8. Examine multicollinearity and compare predictions with observed costs.

## Business Relevance

Hospital cost analysis can help analysts investigate cost drivers and support questions about budgeting, resource planning, and package pricing. Any recommendation should be based on verified model results, an understanding of the dataset, and appropriate clinical and operational context.

## Results

Refer to the project report for the specific model outputs and findings. Before quoting a numeric performance measure, verify the selected model, target transformation, test-set evaluation, and units. Do not report an unverified accuracy or cost-saving percentage.

## Limitations

- Observational associations do not establish causation.
- Missing-value treatment and model selection can affect estimates.
- Regression assumptions and residual diagnostics should be checked.
- A model developed on one dataset may not generalize to other hospitals or time periods.
- Data privacy and permission to share healthcare-related data must be respected.

## Project Status

**Academic analysis / prototype.** No live hospital deployment, operational adoption, or realized cost savings are claimed.

## Learning Outcomes

Data cleaning, exploratory analysis, regression modelling, dummy-variable encoding, multicollinearity assessment, and communicating cost-analysis limitations.

## Author

Rahul | [GitHub Profile](https://github.com/imrahul11299-netizen)

