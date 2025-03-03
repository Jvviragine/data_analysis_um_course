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
However, high accuracy does not mean that such a model would be useful. This model will have 0/0 precision and 0/FN recall. Taking only the accuracy in consideration is problematic especially in heavily imbalanced datasets where simply predicting the majority class could produce a high accuracy.
That is why other metrics such as precision, recall and F1-score, should be considered and calculated for each individual class. In a lot of practical settings, it is critical to classify the minority class correctly and so people might choose to impose weights that reflect the cost of misclassification in order to illustrate the importance of the minority class.
In this case, if we were trying to identity the people who are not health and might need a medical treatment or special care, for example, we would have failed in every instance. In a lot of applications like medical domains, loans and predictive quality control, the cost of misclassifying the minority class can be much greater than simply being able to correctly identify the majority one. 
The confusion matrix shows this very clearly. We see how everyone who was in poor health was classified as being healthy. 

## Question 2 (3 pts)

- We see a 92% accuracy on the test. However, we see that the precision, recall and f1-scores are 0. In addition, the confusion matrix shows that the model is biased towards the majority class and thus never predicts 'poor health'. 
- The Confusion Matrix for both training and testing shows how the model is still essentially just predicting everyone to be in the majority class. For the Training Set, the confusion matrix shows us that out of the 74 people who were in poor health, only one was identified by the model. For the testing, it is even worst, since out of the 25 people who were in poor health, the model could not identify even one. 

## Question 3 (4 pts)

- We see that 588 records were dropped due to missing values in the 'income' column. This corresponds to ~37.9% of the dataset. Additionally, to evaluate how dropping observations affected the amount of poor health individuals, we counted those individuals before and after removing the NaN values. In the plot we can see that the proportion of poor health individuals in the dataset dropped from ~0.064 to ~0.017, which indicates more than a 3-fold reduction and demonstrates that removing incomplete observations disproportionately affects the number of poor health individuals.
- We have seen before how bad the Logistic Regression performed due to the highly Imbalanced Dataset we have. Now, after dropping the records that had missing values in the income value, we see how the minority class goes from representing 6.38% of the data to only 1.66%. This makes the situation that was already bad, even worst. We essentially destroy the distribution of our dataset.
- Besides, we can see how the Age distribution changes quite a bit with the deletion. The Median age decreased and the Upper Whisker, which was about 90 years old in the original data now goes down to around 82 years old. This shows how a great number of the people in bad health were older (which makes logical sense).

## Question 4 (4 pts)
We see an accuracy of 98%, however, as discussed earlier, accuracy alone is not very indicative of how good the performance of the model is. The first logistic regression model we built also had high accuracy, while being biased towards the majority class and never predicting the positive outcome. In addition, earlier we saw that there were only 2% 'poor health' individuals in our dataset after removing NaN values, therefore, it is possible to achieve 98% accuracy by just predicting the negative class.
Indeed, for this model, this is precisely the case, where we get a high accuracy by just predicting the majority class. In fact, we were not able to predict any of the minority class instances (we can see this by the 0% precision, 0% recall and 0% f1 we obtain for both training and testing)


## Question 5 (4 pts)
Here we notice some interesting facts. The first one is that by looking at the AUC, we see that the model is doing better than a random classifier (which has AUC of 0.5).
- I created the respective ROC curves for the logistic regression model where the income column is dropped and the logistic regression model where rows containing NaN values are removed. Both models perform the train test split with random state = 42 for reproducibility. In both models we can see that due to the majority class bias we need to use thresholds that are very close to 0 in order to improve the true positive rate, which makes sense. In addition, for the model where the income column is dropped we have AUC = 0.73, which is better than random but but suggests that there is room for improvement. On the other hand, the model that has rows with NaN values removed has AUC = 0.58, which is only slightly better than random and suggests poor predictive power. The difference in performance suggests that simply dropping rows with NaN values is not a good strategy as it leads to loss of valuable information. Those finding suggest that we should consider imputation techniques rather than attempting to remove columns or rows containing NaNs. 
- Another observation is that our model always says very close to the random model line (y = x), which shows in a visual manner what we had already seem numerically, namely that our model has almost zero discrimination power between the classes.
- Moreover, we see that the numbers inside the little rectangles corresponds to the different thresholds used by the model. We see how it can only classify a few instances in the minority classes by using extremely low thresholds, which is not a good sign at all, since, if we take a probabilistic interpretation of the scores output by Logistic Regression, we would be essentially saying that if the model gives like a 2% probability of being in the minority class, we should classify it as minority class, which is a very low confidence to base decisions upon.


## Question 6 (6 pts)
- Interesting to see that the Income Distribution after Imputation now has a huge bump in the value that was the older mean, since many samples were imputed with those.

- The calculated mean is ~15633. Since we were able to identify 588 missing values, those were replaced with the calculated mean. This change is clearly reflected in the income distribution visible on the histogram as the bin corresponding to income of ~15,000 jumps from ~100 to ~700 entries.

## Question 7 (4 pts)
- First observation that we see is that our AUC improved from around 0.6 to 0.71, which shows that our model improved in being able to distinguish between the 2 classes. However, there is still more left to be desired as this performance is comparable with the model where the income column was dropped (AUC = 0.73). While mean value imputation helps us preserve the original sample size, we see that in this case it does not offer us much in terms of performance, likely due to the fact that the relationship of income with the other columns is not taken into account. Also, the mean imputation might not be ideal in our case as we have a right-skewed distribution and taking the mean can introduce further bias, thus not capturing the true information of the missing values. While, mean imputation is simple to apply, we should consider more sophisticated techniques in this case like MICE (Multivariate Imputation by Chained Equations).
- Visually this can also be clearly seem by the fact that the ROC curve of our model is further away from the random classifier, which is also a good sign (numerically this translates to a bigger AUC).
- Moreover, another interesting fact is that now our model is already able to classify some minority classes with a much bigger threshold (starting at 0.26, while before the biggest was 0.02).
- The increase in performance is very likely due to the fact that now we did not delete the biggest part of the minority samples, but rather imputed with the mean (which I am not sure if it helped, but at least allowed us to not exclude the majority of the minority class, meaning that the model can actually learn something from it.)


## Question 8 (8 pts)
- Now, by using the Linear Imputation, the performance has actually decreased compared with the simple Mean Imputation (from AUC of 0.71 to 0.66). However, it's still performing better than just dropping the records with NaN (AUC of 0.6)
- This method was much more work to make it work, since we essentially have to train a model to predict the missing values which is then used to impute the missing values and then, another model is trained on top of that
- We are still not able to classify the minority class well, however, we do better than just dropping the missing values.
- One reason why the mean worked better could be because, perhaps, the Income is not linearly dependent with the other features, so a linear regression without any transformations in these features could be inappropriate (just a guess)

## Question 9 (4 pts)
The AUC score I achieved in this part is AUC = 0.71. This was surprising to me as I expected that a linear regression imputation would improve our classification performance. What that indicates is that linear regression might not be able to capture the relationships between income and other variables (specially if there are non-linear ones). Additionally, the models might be hitting a ceiling due to the class imbalance problem that we have not addressed.
The one that performed the worst was the one where we simply delete the records where there were Nan values. This makes sense since we went from having a representation of around 6% of the minority class to a bit over 1%. If the problem was already extremely imbalanced, we made it even worst by essentially destroying the few samples we had in the minority class. I believe there s no good reason to use this approach.
Mean Imputation and Linear Regression Imputation had similar performances. However, it is important to notice now the Mean Imputation is a much simpler approach to implement, while the Linear Regression Imputation essentially requires us to train a separate model for this just so we can latter train another model. Moreover, Linear Regression Imputation assumes the relationships between the variables are linear, which might not be the case.
With the Mean Imputation a disadvantage is that it destroys the original shape of the distribution in which that transformation is applied (we could visually see with the Histogram the big bump). This becomes even more significant when we realize that for this specific dataset, around 37% of the records had missing values for the Income feature, so we essentially made 37% of the records have the same value for a feature (the mean). This means that we decrease the variance of the original Income distribution, which in turn, means that when the models are being trained, for the Income feature, 37% of the records will have the same exact value, which is not very helpful to add useful information to the model.

# Part 3
- regularize with cross-validation


## Question 10 - improve the model (15 pts)

To address the challenges of class imbalance and improve model performance, I implemented several approaches:

 - 1. Regularized Logistic Regression with Cross-Validation

I applied regularization to the logistic regression model using GridSearchCV to find the optimal values for the regularization parameter C and class weights. Cross-validation with 5 folds was used to prevent overfitting. The best model achieved an AUC of 0.71, with optimal parameters  {'C': 0.01, 'class_weight': None}.

 - 2. Decision Tree Classifier

Decision trees offer a different modeling approach that can sometimes perform well on imbalanced datasets. I tuned hyperparameters including max_depth, min_samples_split, and min_samples_leaf to find the optimal tree structure. The best decision tree model achieved an AUC of 0.77.

The decision tree showed better performance compared to logistic regression, likely due to its ability to create non-linear decision boundaries.

 - 3. Random Forest Classifier

Random forests, as ensemble models, often perform better than single decision trees by reducing variance. I optimized the hyperparameters including n_estimators, max_depth, and class_weight. The best random forest model achieved an AUC of ~0.78.

The random forest showed slightly improved performance compared to the previous models.

 - 4. Handling Class Imbalance with SMOTE

To directly address the class imbalance issue, I applied the Synthetic Minority Over-sampling Technique (SMOTE) to generate synthetic examples of the minority class. To put it simply, what SMOTE does is tat instead of simply duplicating points from the minority class, it picks points in the minority class, finds neighbours, and essentially creates blends from these points, so as to have more "naturally looking points". It does this until the classes are balanced. Therefore, instead of simply doing oversampling by duplicating minority class points, it creates synthetic points that are close to the original ones. When combined with the best performing random forest model, this approach achieved an AUC of 0.80.

The SMOTE + Random Forest combination did improve performance over the standard Random Forest, suggesting that the synthetic examples helped the model better learn the minority class patterns.

- Conclusion

Among all models tested, SMOTE + Random Forest performed best with an AUC of 0.80. 

From the feature importance analysis, we can see that income and education are the most predictive features for identifying individuals with poor health. 


While the model's performance improved compared to our initial models, there is still room for improvement, potentially through:

1. Collecting more data, especially for the minority class
2. Exploring more sophisticated ensemble methods
3. Applying more advanced resampling techniques
4. Use different class weights within the model, so as to try to compensate for the imbalance in the dataset.
5. Understand better how to impute a value that makes sense for the missing values in Income. Perhaps, something more aligned with domain experts or try to predict the missing values with a model that can handle better non-linear relationships between the features.
6. Understand better what is the relative cost of misclassify a sample from the minority class. With this, we could apply weights to the sample in a more realistic sense, so as to make the model learn better from the minority class.
 
