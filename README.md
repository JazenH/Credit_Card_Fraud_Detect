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
**Packages:** pandas, numpy, sklearn, matplotlib, seaborn, tensorflow, xgboost \
**Data Source:** https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud

## EDA
- Aggregate the transactions in unit hour. The data provide instances in seconds, by gathering the events in hours, we found a main difference between fraud and non-frand transaction
- Re-scale the data with RobustScaler. We found that fraud transaction are more tend to be small in amount. There are sporadic large fraud transaction as outlier. We resclae the data to reduce the risk to sabotage the behavior of the models

<p >
<img src="https://github.com/JazenH/Credit_Card_Fraud_Detect/blob/main/amount_frequency.png" width="1100" height="450" />
</p>


The data contains records in unit seconds, which elapsed between each transaction and the first transaction in the dataset. There are more than 280,000 in the dataset, the enormous records bury the pattern of the collective behavior. We construct a column "hour" by aggregating the transation amount in each hour. We should the relation between the amount and time. From the graph we can see that for non-fraud transaction, there is an obvious period which is about 24 hours. This can be easily explain that true transactions occored within normal working hours and the peaks mark at day time. There are certain transaction happen at night. For fraudulant transaction, there is no pattern. The fraudster keep attack the system in short intervals. A possible reason is that with large attack rate and small transaction amount, the fraudster and hide the tracks an acumulate considerable quota.

<p >
<img src="https://github.com/JazenH/Credit_Card_Fraud_Detect/blob/main/fraud_amount.png" width="850" height="450" />
</p>

In this graph we plot the transaction amount versus time instance. There is no obvious correlation between the two variables. A key feature is that the fraudulant transaction amount are mainly small (around 500), which confirms the assumption from previous observation. There are some large transactions look like outliers. The reason could be that the fraudster sometime take a bold move to steal a large amount or that the transactions are from different fraudster with different strategy.

## Modeling
### Down-sampling
The data is highly imbalanced. we randomly sample from non-fraud section with the same amount of record as that in fraud section, constructing the training set by combining two parts.

### Random Forest
<p >
<img src="https://github.com/JazenH/Credit_Card_Fraud_Detect/blob/main/RandomForest_n.png" width="600" height="450" />
</p>

We check how different n_estimator's affect the model by checking the accurary. It is visible that a high value for n_estimators will give a good acuracy score, but it is fluctuating randomly in the curve even for nearby values of n_estimators, and higher n(>75) will not give noticablly better score. In the actual modeling, we use n_estimator=100.

<p >
<img src="https://github.com/JazenH/Credit_Card_Fraud_Detect/blob/main/RandomForest_ROC.png" width="600" height="450" />
</p>
The confusion matrix 

[130   4] \
[20  142]

## Xgboost
The confusion matrix

[[134,   0] \
[ 13, 149]]

f_1 = 0.9581993569131833

Xgboost obtained a slightly better result than random forest, as expected. The Xgboost focuses on the errors and boost the decision tree to better classify the classes.

## Neural Network with Tensorflow

We build a neural network with tensorflow. We use Relu as activation function in the hidden layers. We used sigmoid function as the output layer as there are only two class. The loss function we used BinaryCrossentropy

Here are some results:

**f1_score**: 0.9556962025316457 \
**accuracy_score**: 0.9527027027027027 \
**confusion_matrix**: \
[[131,   3] \
[ 11, 151]]

## Summary

We analysis the pattern of transaction frequency of fraud and non-fraud events, found that there are different modes between two groups. We noticed that the fraudster tend to make small amount transactions to hide the tracks, but there are some large amount of transaction, which may come from bold move or different fraudster.

We down sample the non-fraud class to make balanced datasets for modeling. We used Random Forest, Xgboot, ANN model to predic the fraud transactions. Xgboot gave a slightly better result than random forest model. The ANN model gave a similar result as the Xgboost.

