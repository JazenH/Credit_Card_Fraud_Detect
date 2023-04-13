# Credit Card Fraud Detecttion: Project Overview

This is a project from Kaggle. The dataset contains transactions made by credit cards in September 2013 by European cardholders.
The dataset is highly unbalanced.There are 492 frauds and 284,315 clean transactions. The positive rate (frauds) is only 0.172%.

The dataset contains time-instance, transaction amount, class(fraud or not) and numerical input variables which are the result of a PCA transformation. The original features and background information are not provided. Feature 'Time' contains the seconds elapsed between each transaction and the first transaction in the dataset. The feature 'Amount' is the transaction Amount, this feature can be used for example-dependant cost-sensitive learning. Feature 'Class' is the response variable and it takes value 1 in case of fraud and 0 otherwise.

With a high unbalanced ratio, a direct applying of classification could lead to high variance. We apply downsampling method to the non-fraud class by randomly sample data from class 0 and build model on the resampled dataset.


## Main Manipulations

- Analysis the data, exstracting the frequency and transaction amount patterns of frauds
- Building Random Forest and XGboost models for predicting fraudulant transactions
- Building neural network work with Tensorflow to detect fraudulant transactions

## Code and Resources Used

**Python Version:** 3.10 \
**Packages:** pandas, numpy, sklearn, matplotlib, seaborn, tensorflow \
**Data Source:** https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud




