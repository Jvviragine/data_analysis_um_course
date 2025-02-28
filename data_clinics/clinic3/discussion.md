## Question 1 (3 pts)

- a)
Percentage of positive class (poor health):  6.38
Percentage of negative class (not poor health):  93.62

- b) 
the majority class is "not poor health" with 93.62%, while hte minority class is "poor health" with 6.38%

- c) 
the accuracy measures the percentage of correct predictions that we make. Given a classifier that always predicts "not in poor health", we would achieve an accuracy of 93.62% as all the negative class instances would be classified correctly. 

- d)
Howerver, high accuracy does not mean that such a model would be useful. This model will have 0/0 precision and 0/FN recall. Taking only the accuracy in consideration is problematic especially in heavily imbalanced datasets where simply predicting the majority class could produce a high accuracy.
That is why other metrics such as precision, recall and F1-score, should be considered and calculated for each individual class. In a lot of practical settings, it is critical to classify the minority class correctly and so people might choose to impose weights that reflect the cost of misclassification in order to illustrate the importance of the minority class.

## Question 2 (3 pts)

- We see a 92% accuracy on the test. However, we see that the precision, recall and f1-scores are 0. In addition, the confusion matrix shows that the model is biased towards the majority class and thus never predicts 'poor health'. 


## Question 3 (4 pts)

- We see that 588 records were dropped due to missing values in the 'income' column. This correspond to ~37.9% of the dataset. Additionally, to evaluate how dropping observations affected the amount of poor health individuals, we counted those individuals before and after removing the NaN values. In the plot we can see that the proportion of poor health individuals in the dataset dropped from ~0.064 to ~0.017, which indicates more than a 3-fold reduction and demonstrates that removing incomplete observations disproprtionally affects the number of poor health individuals.

## Question 4 (4 pts)
We see an accuracy of 98%, howerver, as discussed earlier, accuracy alone is not very indicative of how good the performance of the model is. The first logistic regression model we built also had high accuracy, while being biased towards the majority class and never predicting the positive outcome. In addition, earlier we saw that there were only 2% 'poor hearlth' individuals in our dataset after removing NaN values, therefore, it is possible to achieve 98% accuracy by just predicting the negative class.

## Question 5 (4 pts)
I created 

## Question 6 (6 pts)
## Question 7 (4 pts)
## Question 8 (8 pts)
## Question 9 (4 pts)

# Part 3
- regularize with cross-validation
## Question 10 - improve the model (15 pts)

