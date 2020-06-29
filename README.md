<<<<<<< HEAD
# Project 2 - Ames Housing Data and Kaggle Challenge

## Overview
The project focuses of finding the best strategy to predict the sale price of individual residential properties in Ames, Iowa.

## Problem Statement
1. Which machine learning model is more effective in predicting sale price?

2. Which are the features of a residential property that have the largest impact on sales price?

## Data
Ames Housing Dataset

Original version: contained 2930 observations and 82 variables of individual residential properties sold in Ames, Iowa between 2006 and 2010. <br>
[Data Source](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt)

Version used in this project: contained 2051 observations and 81 variables. <br>
[Data Source](https://www.kaggle.com/c/dsi-us-11-project-2-regression-challenge/data)

## Missing Data
- Values that appeared typos were replaced by their reasonable counterpart (Garage Year Built 2207, with 2007)


## Feature Engineering

- used total SF instead of all SF variables - basement type 1-2, unfinished basement, 1st fl, 2nd fl

**Scaling**
- y variable: log-transformed
- X variables: StandardScaler
# Modeling
## Baseline - Linear Regression - Manually Selected Features

Features: variables that had at least a .5 correlation strength (absolute value of correlation) in relation to SalePrice <br>
All variables were unscaled. No polynomial features.

## Linear Regression - Automated Feature Selection
All features in the model - except: <br>
                      'Id', 'PID', <br>
                      'BsmtFin SF 1', <br>
                      'BsmtFin SF 2', <br>
                      'Bsmt Unf SF', <br>
                      'Total Bsmt SF', <br>
                      '2nd Flr SF', <br>
                      'Low Qual Fin SF', <br>
                      'Gr Liv Area', <br>
                      'Wood Deck SF', <br>
                      'Open Porch SF', <br>
                      'Enclosed Porch',<br>
                      '3Ssn Porch', <br>
                      'Screen Porch', <br>
                      'Pool Area' <br>
All polynomial features added - except bias variables <br>
All featured scaled with StandardScaler.<br>
SelectKBest - 45 best features.
Y variable - logtransformed Sale Price

## Regularized Regression Models
## Ridge Regression
Sklearn.linear_models RidgeCV <br>
Features - all variables that went into the SelectKBest transformer. <br>
Alphas - np.logspace(0, 4, 50) <br>

## LASSO Regression
Sklearn.linear_models LassoCV <br>
Features - all variables that went into the SelectKBest transformer. <br>
Alphas - np.logspace(0, 4, 50) <br>

## Evaluating the Models 
The models were evaluated based on their accuracy (training dataset: R-squared score), generalizability (comparison of training and testing R-squared scores), and cross-validation R-squared scores.

||**Training R^2**|**Testing R^2**|**Cross-Val R^2**|
|---|---|---|---|
|**Linear Regression** <br> **baseline** |.80|.86|.78|
|**Linear Regression** <br> **automated** |.87 |.85|.78|
|**Ridge Regression**||.98|.79|
|**Lasso Regression**||.97|.87|

All three models performed better when I log scaled the y variable and increased the test size. <br>

Baseline model seems to be the best: it has a relatively low bias level, it explains 80% of the variance in the sale price. The cross-validation score supports this interpretation (being only 2 percentage points lower than the training score). The relatively higher R^2 score on the test data set indicates that the testing subsample of the data was not fully representative of the total dataset.

The linear regression model with automated feature selection performed better than the two regularized models, but not as well as baseline model. Although the model explains 87% of the variance in the sale price, and seems sufficiently generalizable (the testing R^2 is close to the training R^2), the almost 10 percentage points lower cross-validation score indicates that the model is unstable.

Comparing the training and test R^2 scores of each regularized regression model suggest that both of these models are overfit, and quite likely they will not generalize well to previously unseen data. 

## Conclusion and Recommendations

1. Based on this preliminary analysis of the data I would suggest the use a simpler linear regression model when predicting housing prices in Ames, Iowa. Although more complex machine learning models often perform better when it comes to prediction, given the features of this particular dataset, the unregularized regression models performed much more reliably.

2. When we have a dataset with a large number of features, using the SelectKBest function of the sklearn.feature_selection library has its undoubtable advantages. However, given that the model with intuitively selected features had better bias/variance indicators than the model with automated feature selection, I recommend the use of a methodological hybryd: machine aided - intuitive feature selection. 

3. Outliers identified during EDA seem to make the more complex models unstable. Further analysis may reveal underlying trends in the data that may require special attention. Revealing those trends would help fine-tune the models to increase the reliability of our predictions. 
=======

>>>>>>> c723199f78ab8daf52acf04e86451d50ff9e4ea8
