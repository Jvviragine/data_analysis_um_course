## Question 1 (3 pts)

- a)
Percentage of positive class (poor health):  6.38
Percentage of negative class (not poor health):  93.62

- b) 
the majority class is "not poor health" with 93.62%, while hte minority class is "poor health" with 6.38%

- c) 
the accuracy measures the percentage of correct predictions that we make. Given a classifier that always predicts "not in poor health", we would achieve an accuracy of 93.62% as all the negative class instances would be classified correctly. 
Cases of Extreme Imbalance show how careful we have to be by just looking at the accuracy of a classifier, as this can be extremely misleading.

- d)
Howerver, high accuracy does not mean that such a model would be useful. This model will have 0/0 precision and 0/FN recall. Taking only the accuracy in consideration is problematic especially in heavily imbalanced datasets where simply predicting the majority class could produce a high accuracy.
That is why other metrics such as precision, recall and F1-score, should be considered and calculated for each individual class. In a lot of practical settings, it is critical to classify the minority class correctly and so people might choose to impose weights that reflect the cost of misclassification in order to illustrate the importance of the minority class.
In this case, if we were trying to identity the people who are not health and might need a medical treatment or special care, for example, we would have failed in every instance. In a lot of applications like medical domains, loans and predictive quality control, the cost of misclassifying the minority class can be much greater than simply being able to correctly identify the majority one. 
The confusion matrix shows this very clearly. We see how everyone who was in poor health was classified as being healthy. 

## Question 2 (3 pts)

- We see a 92% accuracy on the test. However, we see that the precision, recall and f1-scores are 0. In addition, the confusion matrix shows that the model is biased towards the majority class and thus never predicts 'poor health'. 
- The Confusion Matrix for both training and testing shows how the model is still essentially just predicting everyone to be in the majority class. For the Training Set, the confusion matrix shows us that out of the 74 people who were in poor health, only one was identified by the model. For the testing, it is even worst, since out of the 25 people who were in poor health, the model could not identify even one. 

## Question 3 (4 pts)

- We see that 588 records were dropped due to missing values in the 'income' column. This corresponds to ~37.9% of the dataset. Additionally, to evaluate how dropping observations affected the amount of poor health individuals, we counted those individuals before and after removing the NaN values. In the plot we can see that the proportion of poor health individuals in the dataset dropped from ~0.064 to ~0.017, which indicates more than a 3-fold reduction and demonstrates that removing incomplete observations disproprtionally affects the number of poor health individuals.
- We have seen before how bad the Logistic Regression performed due to the highly Imbalanced Dataset we have. Now, after dropping the records that had missing values in the income value, we see how the minority class goes from representing 6.38% of the data to only 1.66%. This makes the situation that was already bad, even worst. We essentially destroy the distribution of our dataset.
- Besides, we can see how the Age distribution changes quite a bit with the deletion. The Median age decreased and the Upper Whisker, which was about 90 years old in the original data now goes down to around 82 years old. This shows how a great number of the people in bad health were older (which makes logical sense).

## Question 4 (4 pts)
We see an accuracy of 98%, howerver, as discussed earlier, accuracy alone is not very indicative of how good the performance of the model is. The first logistic regression model we built also had high accuracy, while being biased towards the majority class and never predicting the positive outcome. In addition, earlier we saw that there were only 2% 'poor hearlth' individuals in our dataset after removing NaN values, therefore, it is possible to achieve 98% accuracy by just predicting the negative class.
Indeed, for this model, this is precisely the case, where we get a high accuracy by just predicting the majority class. In fact, we were not able to predict any of the minority class instances (we can see this by the 0% precision, 0% recall and 0% f1 we obtain for both training and testing)


## Question 5 (4 pts)
Here we notice some interesting facts. The first one is that by looking at the AUC, we see that the model is doing better than a random classifier (which has AUC of 0.5). 
- An important observation is that I fixed the random seed across my entire notebook, otherwise we were always getting a different data split and a different logistic regression model.
- Another observation is that our model always says very close to the random model line (y = x), which shows in a visial manner what we had already seem numerically, namely that our model has almost zero discrimnation power between the classes.
- Moreover, we see that the numbers inside the little rectangles corresponds to the different thresholds used by the model. We see how it can only classify a few instances in the minority classes by using extremely low thresholds, which is not a good sign at all, since, if we take a probabilistic interpretation of the scores output by Logistic Regression, we would be essentially saying that if the model gives like a 2% probability of being in the minority class, we should classify it as minority class, which is a very low confidence to base decisions upon.
## Question 6 (6 pts)
- Interesting to see that the Income Distribution after Imputation now has a huge bump in the value that was the older mean, since many samples were imputed with those.
## Question 7 (4 pts)
- First observation that we see is that our AUC improved from around 0.6 to 0.71, which shows that our model improved in being able to distinguish between the 2 classes.
- Visually this can also be clearly seem by the fact that the ROC curve of our model is further away from the random classifier, which is also a good sign (numerically this translates to a bigger AUC).
- Moreover, another interesting fact is that now our model is already able to classify some minority classes with a much bigger threshold (starting at 0.26, while before the biggest was 0.02).
- The increase in performance is very likely due to the fact that now we did not delete the biggest part of the minority samples, but rather imputted with the mean (which I am not suure if it helped, but at least allowed us to not exclude the majority of the minority class, meaning that the model can actually learn something from it.)
## Question 8 (8 pts)
## Question 9 (4 pts)

# Part 3
- regularize with cross-validation
## Question 10 - improve the model (15 pts)

