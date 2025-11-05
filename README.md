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

We engineer the features that we've chosen above based on their data type. In particular the numeric variables (in this case, just age) are scaled using the StandardScaler() function while the categorical variables (all other variables) utilize the one hot encoder. We create a column transformer for this method that we plan to input into a pipeline for fitting the data based on multiple potential classifiers. Following this, the dataset is split between the training and testing where the training incorporates 80% of the dataset and the remaining 20% is for testing (A random state is also set to ensure repeated iterations are still the same). Finally, a baseline is created which simply guesses the majority class everytime (in this case is "no). This baseline maintains a training accuracy of 0.8743 and a testing accuracy of 0.8698. Note accuracy was chosen for the metric as the business objective in this case does lean towards one specific prediction preference (more "yes" or more "no") so we utilize our default metric here.

## First Run and Results

We create pipeline that includes our column transformer and can fit any model classifier of our choosing. We then run 4 possible pipes on Logistic Regession, K Nearest Neighbors, Decision Trees, and Support Vector Machines on their default settings and see the results. After fitting and testing, we record for each model the train accuracy, the test accuracy, and the time spent training.

In terms of accuracy, the Logistic Regression and the Support Vector Machine performed the best of the 4 models, each with equaling testing accuracy. However their default test accuracy ended up being the same as the baseline at 0.8698. Meanwhile the K nearest neighbors and the decision tree both showcased signs of overfitting as their train accuracy was much higher, particularly for the decision tree. As for training time, k nearest neighbors had the quickest time at 0.03 seconds with Logistic and Decision Trees not far behind at 0.18 and 0.19 seconds respective. However, the support vector machine took 8.8 seconds for training, more than 10x the next largest training time. As such the best model here would the logistic regression due to its low train time and highest accuracy. For further detail in these findings, please check our jupyter notebook in this directory on this section. Next, we hypertune each model based on chosen parameters to see if we can improve them.

## Hypertuning and Results

Following these base models, we now want to hypertune each of them against potential parameters to further improve upon them. We hypertune upon the following parameters for each model:

Logistic Regression:
- norm of penalty
- regularization strength
- optimization algorithm
- weights associated with classes

K Nearest Neighbors:
- number of neighbors
- method of weights
- power parameter

Decision Tree:
- criterion
- max depth of tree
- min number of samples required for split
- min number of samples required to be a leaf node
- weights associated with classes

Support Vector Machines:
- Regularization Parameter
- Kernel Type
- Gamma Value
- weights associated with classes

For each of these models we run a pipeline that contains the transformer into a grid search testing on accuracy which utilizes 5 cross validation splits. Each model goes through the grid search before finding the best parameters and running a final pipeline with them fitted on the train data against the test data. For further details on these parameters chosen, please refer to the jupyter notebook.

The first main notice of the results found was that none of the models were able to outperform the baseline. As with default parameters, Logistic and Support Vector Machine had the same training and testing accuracy despite the hyper tuning. A further look at the parameters chosen on these 2 models showcases that most of the default parameters were chosen as best during the hypertuning. Decision Tree was a model that was improven from default settings but the training and testing accuracy were still the same as the baseline. The only model not identical to the baseline was k nearest neighbors, where hyper tuning assisted it with lower levels of overfitting but its testing accuracy was still worse. As for training time, logistic took an increase letting Decision Tree be the new best model of the 4 with the highest accuracy and shortest time at 0.198 seconds.


## Conclusions and Next Steps

Overall in this scenario, in terms of a default model the Logistic Regression performed the best whereas if we had the resources to implement a hypertuning on each model, then the decision tree would perform the best. However, it can't be ignored that none of the 4 models ever surpassed the baseline. Looking at the decision tree more, it seems the only real feature of value for prediction here was age, the rest of the features were not as useful for our metric. The next steps in this study would be to either explore deeper into the data and feature engineer new and stronger features that we can train and improve our models upon or alternatively based on the business objective (aiming to predict more for yes subscriptions correctly for example) change our metric which would in turn change how our models think. Alternatively, we can further improve on our current models but since performance across most of these models seems to be best near default settings and the fact that their results are the exact same as the baseline, I would not recommend this step.
