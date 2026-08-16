Parkinson's Disease Progression Analysis

Overview

This project analyzes Parkinson's disease progression using clinical and biomedical voice measurements. The analysis focuses on identifying relationships between voice-related features, demographic variables, and UPDRS scores, followed by regression modeling and evaluation.

The notebook performs exploratory data analysis, preprocessing, multicollinearity assessment, regression analysis, residual diagnostics, outlier detection, regularization, and Random Forest modeling.

Dataset

The analysis uses the parkinsons_updrs.csv dataset.

According to the notebook:

Data contains observations from 42 individuals monitored over a six-month period.

There are approximately 200 observations per individual.

The dataset contains 18 predictor variables, including age, sex, and biomedical voice measurements.

UPDRS stands for Unified Parkinson's Disease Rating Scale.

The analysis primarily uses total_UPDRS as the response variable.

Main Features

The dataset includes several groups of biomedical voice measurements:

Jitter features: Jitter(%), Jitter(Abs), Jitter:RAP, Jitter:PPQ5, Jitter:DDP

Shimmer features: Shimmer, Shimmer(dB), Shimmer:APQ3, Shimmer:APQ5, Shimmer:APQ11, Shimmer:DDA

NHR: Noise-to-Harmonics Ratio

HNR: Harmonics-to-Noise Ratio

RPDE: Recurrence Period Density Entropy

DFA: Detrended Fluctuation Analysis

PPE: Pitch Period Entropy

Age and sex

Objectives

The main objectives of the analysis are to:

Explore the structure and distribution of the Parkinson's disease dataset.

Identify missing values, duplicate records, and potential data-quality issues.

Examine relationships between predictors and UPDRS scores.

Detect and assess multicollinearity among predictor variables.

Evaluate linear regression and Ordinary Least Squares models.

Analyze residual assumptions and model diagnostics.

Identify influential observations and potential outliers.

Refit models after removing influential observations and transforming the response.

Apply Ridge and Lasso regularization.

Build and evaluate a Random Forest Regressor.

Compare model performance using cross-validation.

Analysis Workflow

1. Exploratory Data Analysis

The notebook examines:

Missing values

Duplicate observations

Summary statistics

Feature distributions

Response-variable distribution

Box plots

Pair plots

The dataset was found to have no missing values and no duplicate observations according to the notebook analysis.

2. Data Preprocessing

The analysis extracts predictor variables and applies feature scaling using StandardScaler.

3. Multicollinearity Analysis

Several approaches are used to investigate multicollinearity:

Covariance matrix

Correlation matrix

Variance Inflation Factor (VIF)

Condition number

Condition indices

Variance decomposition

The notebook identifies substantial multicollinearity, particularly among several Jitter and Shimmer variables.

4. PCA

Principal Component Analysis is explored as a dimensionality-reduction approach for handling multicollinearity.

5. Base Regression Models

Two linear regression approaches are evaluated:

Scikit-learn LinearRegression

Statsmodels OLS

The OLS model reports an R-squared of approximately 0.170, indicating that the linear model explains a relatively small proportion of the variability in total_UPDRS.

The model is statistically significant overall, but diagnostic statistics indicate issues including residual autocorrelation and non-normality.

6. Residual Analysis

The OLS model is assessed using:

Residuals vs fitted values

Histogram of residuals

Q-Q plot

Autocorrelation function (ACF)

The notebook identifies evidence of non-linearity, residual patterns, and strong positive autocorrelation.

7. Outlier and Influence Detection

Potential influential observations are investigated using:

Cook's Distance

DFFITS

DFBETAs

COVRATIO

Several observations, particularly around indices 1900, 4100, and 5300, are identified as influential by multiple methods.

8. Outlier Removal and Model Refitting

Potentially influential observations are removed and the response variable is square-root transformed.

The refitted OLS model produces:

R-squared: 0.356

Adjusted R-squared: 0.353

F-statistic: 129.5

Although explanatory power improves, the notebook concludes that the model still has limitations, including multicollinearity and residual autocorrelation.

9. Regularization

Ridge Regression

Ridge regression is applied to reduce the effect of multicollinearity while retaining all predictors.

The analysis indicates that:

age has a strong positive influence.

PPE and several Jitter/Shimmer features contribute meaningfully.

HNR has a strong negative coefficient.

Ridge shrinks coefficients without eliminating predictors completely.

Lasso Regression

Lasso regression is used for both regularization and feature selection.

The notebook reports:

R-squared: 0.1510

Best alpha: 0.0142

Several features are reduced to zero by Lasso, producing a simpler model.

10. Random Forest Regression

A Random Forest Regressor is used to capture nonlinear relationships that may not be adequately represented by linear regression.

The notebook evaluates the model using:

Mean Squared Error (MSE)

R-squared

Feature importance

5-fold cross-validation

The final cross-validation results reported in the notebook are:

Metric

Result

Cross-Validated MSE

9.7592

Cross-Validated R²

0.9148

These results indicate substantially stronger predictive performance from the Random Forest model compared with the linear regression approaches explored earlier.

Key Findings

The dataset contains strong multicollinearity among several voice-related predictors.

Standard linear regression provides relatively limited explanatory power.

OLS diagnostics reveal problems with residual independence and other model assumptions.

Several observations have substantial influence on regression estimates.

Removing influential observations and transforming the response improves the OLS R-squared, but does not fully resolve the diagnostic issues.

Ridge regression reduces coefficient magnitude while retaining all predictors.

Lasso regression performs feature selection by shrinking some coefficients to zero.

Voice-related features such as Jitter, Shimmer, RPDE, and PPE show important relationships with UPDRS measures.

age consistently appears as an influential predictor.

The Random Forest model performs considerably better in the reported cross-validation results, suggesting that nonlinear or interaction effects may be important in predicting UPDRS scores.

Technologies and Libraries

The notebook uses Python and the following major libraries:

NumPy

Pandas

Matplotlib

Seaborn

Scikit-learn

Statsmodels

SciPy

Project Structure

.
├── Parkinson's Disease Progression Analysis.ipynb
├── parkinsons_updrs.csv
└── README.md

How to Run

Place parkinsons_updrs.csv in the same directory as the notebook.

Open Parkinson's Disease Progression Analysis.ipynb using Jupyter Notebook, JupyterLab, or a compatible notebook environment.

Install the required Python libraries if they are not already available.

Run the notebook cells sequentially.

Conclusion

The analysis compares traditional linear regression, diagnostic and influence analysis, regularization methods, and Random Forest regression for Parkinson's disease progression modeling.

The results suggest that linear models are affected by multicollinearity, residual dependence, and other diagnostic limitations. Regularization provides some control over correlated predictors, while the Random Forest model achieves much stronger predictive performance in the reported 5-fold cross-validation results.
