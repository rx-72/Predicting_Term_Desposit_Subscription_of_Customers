The main goal of this study is to compare the performances of the following 4 classifiers: Logistic Regression, K Nearest Neighbors, Decision Trees, and Support Vector Machines. The data that we utilize in this scenario involves marketing campaigns through phone calls of a Portuguese banking institution where the goal is to predict whether the called customer will subscribe to a term deposit or not.

## Background

Opening the dataset, we're given a list of features involving the customer and more specific information about the bank in question. After cleaning the dataset of missing and/or null values, we decide to solely focus on the features of the customer for prediction which includes as follows:

1. Age
2. Job
3. Marital Status
4. Education
5. Credit Defaulted
6. Housing Loan
7. Personal Loan

The business objective here in question is if given these customer qualities, can we predict whether a customer would subscribe to our term deposit policy or not. The target variable would be for each customer whether they actual subscribed or not. Note the majority of customers in this dataset did not subscribe.

## Set up

We engineer the features that we've chosen above based on their data type. In particular the numeric variables (in this case, just age) are scaled using the StandardScaler() function while the categorical variables (all other variables) utilize the one hot encoder. We create a column transformer for this method that we plan to input into a pipeline for fitting the data based on multiple potential classifiers. Following this, the dataset is split between the training and testing where the training incorporates 80% of the dataset and the remaining 20% is for testing (A random state is also set to ensure repeated iterations are still the same). Finally, a baseline is created which simply guesses the majority class everytime (in this case is "no). This baseline maintains a training accuracy of 0.8743 and a testing accuracy of 0.8698.

## First Run and Results

We create pipeline that includes our column transformer and can fit any model classifier of our choosing. We then run 4 possible pipes on Logistic Regession, K Nearest Neighbors, Decision Trees, and Support Vector Machines on their default settings and see the results.
