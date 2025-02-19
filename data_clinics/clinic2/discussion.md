### 1.1 
The row causing the error was row 33:
15,646.9,22,21862.732919254657,Petrol,97,1,0,1400,3,1100,GBP
Due to the extra comma the csv file could not be read correctly. Fixed by adding "".

### 1.2
Problem with following row:
8423.0;68;58860.0;Petrol;110;1;0;1600;3;1055;CHF
-wrong delimiter is used

### 1.3
Problem the dtype of "Price" is Object
Reason:
28 cases with "":
most are in this format:  
"14,851.099999999999"

Need to adjust special cases:
1 in this format:
"15,398,499999999998"
3 in this format:
"9,864£"

Finally, remove '"' and ',' and convert to floats

### 1.4
Problem converting mileage to numeric
- need to remove special symbol from a row: ß7787.0

### 1.5
Fuel type with highest avg. price:  Diesel
Num doors with highest avg. price:  5

### 1.7 B
The Spearman correlation is stronger (-0.604) compared to the Pearson correlation (-0.564). This aligns with our visual inspection of the scatter plot that shows a non-linear relationship as Spearman correlation is better at capturing non-linear monotonic relationships. On the other hand, when we compare the correlation for Age-Price, we see that the Pearson correlation is stronger (-0.871 v. -0.832), which is what we expect as Pearson tries to capture the linear r-ship between the 2 variables and the scatter plot indicates a linear r-ship between Age and Price.

### 2.1 A
To avoid the problem of multicollinearity coming from the fact that our one-hot encoded colums are linearly dependent (you can always infer the n_th if you know the other n-1), we decided to use the drop_fist option in pd.get_dummins. We go from 10 to 13 columns after the one-hot encoding.
The idea is that we could predict of the options but knowing the others, which could cause problems, since there would be esentially a perfect correlation.
### 2.1 C
Normally we would add a validation set for hyperparameter tuning. If we are building a simple linear regression model that might not be necessary. However, if we decide to use regularization, we might want to tune the parameter alpha.
For a normal linear regression without regularization, there are no hyperparameters and we can even find the solution in a purely analytical way (Ordinary Least Squares)
### 2.1 D
With Standardization, we get a Mean of 0 and Standard Deviation of 1. In the table, the values are not exactly 0 and 1 due to arithmetic precision.
### 2.1 E
If we first standardize the data and then split, we might risk data leakage. That is because we are using information from the test set to scale the data. Instead we should first split the data and then standardize it using the train set statistics.
We can also think from a practical point of view. A model in production, cannot use the "test set" to help it in the standardization, since it does not even have access to the test set. Therefore, we should always first split the data and then train the standardization on thr training and simply apply it to the test.
### 2.2.2
We observe RMSE ~1451.95. To calcualte it, first we compute the errors for all predictions -> (actual price - model prediction). Next we square all the erors, which is helpful because it allows us to treat positive and negative values equally and is sometimes used to also punish bigger errors more. To compute the MSE, we simply compute the average of the squared errors. Lastly, taking the root of the MSE essentially brings our metric back to the original units, which makes the interpretation easier. *In this case, we can say that for a given car, the predictions from our linear regression model on average will be about 1451 euros away from the actual price (could be underestimating or overestimating).*
### 2.2.3
R-squared on the test dataset is ~0.82. This values means that our model explain ~82% of the variance in car prices observed on the test set. (Note the value is slightly lower than the adjusted r-squared observed on the training data - 0.853). Generally we want r-squared values closer to 1 as this indicates good generalization on the test set.
The fact that the r-squared between the Training and Testing was similar is a good sign, which generally means that the model is not overfitting the training data and is generalizing well.

### 2.2.4
From the table we can observe that the statistically significant features at 5% are: Age, Mileage, HP, CC, Weight, FuelType_Diesel, FuelType_Petrol (the ones not statistically significant are: MetColor, Automatic & Doors)
                            coef          std err    t           P
Age             x1         -2090.5956     53.300    -39.223      0.000   
Mileage         x2          -507.3151     53.426     -9.496      0.000   
HP              x3           498.7567     96.956      5.144      0.000   
MetColor        x4            19.5791     38.321      0.511      0.610   
Automatic       x5           -29.9615     40.279     -0.744      0.457  
CC              x6          -493.9176    113.633     -4.347      0.000   
Weight          x7          1199.5142     77.912     15.396      0.000   
FuelType_Diesel x8           468.4691    174.046      2.692      0.007   
FuelType_Petrol x9           407.1422    108.328      3.758      0.000   
Doors_3         x10           43.6853    639.728      0.068      0.946   
Doors_4         x11          113.7366    386.811      0.294      0.769   
Doors_5         x12          -10.0184    642.788     -0.016      0.988   

### 2.2.5
The 2 features with highest coefficients are Age and Weight. Age has a coef of ~-2090.6 which implies that for each additional year of a car's age, it's value depreciates by roughly 2090 euros. On the other hand, the coef for Weight is ~1199.5, which means that for each kilogram added, the value of a car rises by ~1199.5 euros.

### 2.3

A feature that could be interesting and is usually very much cosidered when buying a car is the general state of the car, for example, if there are scratches or dents or if the car has been in an accident before. This could be a boolean feature as well.
Additionally, a boolean flag indicating whether the full service history is included or not could be beneficial
to explaining the remaing variance. Also, we can add boolean features to indicate the presence of safety features such as ABS.


### 2.4
A confounding variable that may be correlated with the car's weight and price is the 'body type'. For example, we have Hatchback which is usually smaller in size and weight and more affordable than other types.
Then we have Sedans, which tend to be a bit bigger, offering sperate trunk space from the cabin, and thus they have mid-range prcies. Then there are SUVs which are bigger and boxier as well as more expensive than both Sedans and Hatchbacks.

Links that show different Toyota Corollas (Hatchback, Sedan, SUV, Wagon):

- https://sunshinetoyota.com.au/blogdetails/which-toyota-corolla-is-right-for-you--a-look-at-the-hatch-vs--sedan/1658#:~:text=Corolla%20Hatchback%3A%20The%20hatch%20has,for%20a%20little%20extra%20flair.

- https://newsroom.toyota.eu/toyota-announces-the-new-2023-corolla/

- https://www.toyota.nl/modellen/corolla-touring-sports

### 2.5
With the inverse mileage term the r-squared has increased slightly by 0.001,
which means that we explain a bit more of the variance in car prices now. Additionally, we see that the inverser_mileage (x13) has p-value  of 0.006 which means that it is statistically significant at the 5% level.

### 3.1
880 sold within 3 months and 556 not.

### 3.2.7
1 = positive = sold <= 3 months
0 = negative = sold > 3 months

We are predicting whether a car will be sold within the first 3 months or not. How can we ensure that we capture all the cars that will not be sold within 3 months such that we minimize the false positives (falsely think we will sell first 3 months but not the case in practice). Conversely, this is also a question of how do we maximize the probability of predicting sold within 3 months correctly such that we have higher confidence when assigning the positive class.

By increasing the threshold we would classify more samples as class 0 meaning decrease the false positives, meaning we would have better precision. This in turn will increase the false negatives (worse recall) but if we aim to maximize the cash flow and sell the cars as quickly as possible increasing the threshold that dictates whether the model thinks the car will be sold within the first 3 months or not could be beneficial because picking a higher threshold gives us higher probability of being correct when assigning class 1 which means we can know which cars to focus on selling quickly.

If we increase the threshold this increases the precision because we have more confidence when predicting the positive class. In turn, the recall is decreased because the model is less likely to predict positive outcomes.
Vice versa, if we decrease the threshold the precision decreases and recall increases.

 ### 3.2.8
 Used link for testing multiple thresholds: https://stackoverflow.com/questions/28716241/controlling-the-threshold-in-logistic-regression-in-scikit-learn

Note that the binary search implementation only gives us a heuristic and is not guaranteed to find the optimal f1 score - that is because binary search works well with monotonic functions. In our case it found a thrshold that is very close to the optimum.

An interesting observation came from the fact that the optimal threshold for the training data was about 0.56, so prioritizing higher precision at the cost of recall. While the optimal threshold for the testing set was about 0.45. I thought that this might because of the class distribution but in the training set we have ~61% class 1 instances and in the test set we have ~60% class 1 instances, so the difference does not seem substantial.

### 3.3.2 
For the random forest classifier I chose the following parameters somewhat arbitrarily:
n_estimators=200, max_depth=5, min_samples_split=10, min_samples_leaf=3, max_features=5, bootstrap=False, random_state=42

### 3.3.3
I added the confusion matrix matrix on the test set of the the random forst classifier.
If we were to compare with the logistic regression model, using the best threshold that was obtained on the training set:
 ******** For threshold = 0.56 ******
Accuracy: 0.9340277777777778
Precision: 0.9378531073446328
Recall: 0.9540229885057471
F1 score: 0.9458689458689458
Confusion matrix:
 [[103  11]
 [  8 166]]

We can see that the models are quite close in terms of performance:
accuracy: 0.9305555555555556
precision: 0.9325842696629213
recall: 0.9540229885057471
f1: 0.9431818181818182
[[102  12]
 [  8 166]]

The difference comes from 1 misclassified instance.

Additionally, a feature importance plot is created which illustrates that price, age, km & weight are our most important features.

Lastly, I added ROC curve comparison between the 2 models, and we can see that they have very similar performance.

### 3.3.4

Two grid searches were attempted - one was more broad and the other more focused. The broader search aimer to identify promising regions in the hyperparameter space and thus was more computationally expensive. Once promising ranges were identified, a nire ficysed grid search was performed to fine-tune the most promising parameter combinations. The process used 5-fold cross validation