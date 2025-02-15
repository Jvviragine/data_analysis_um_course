### 1.1 
The row causing the error was row 33:
15,646.9,22,21862.732919254657,Petrol,97,1,0,1400,3,1100,GBP
Due to the extra comma the csv file could not be read correctly. Fixed by adding "".

### 1.2
Problem with following row:
8423.0;68;58860.0;Petrol;110;1;0;1600;3;1055;CHF
-wrong delimiter is used

### 1.3
Probelm the dtype of "Price" is Object
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

### 2.1 C
Normally we would add a validation set for hyperparameter tuning. If we are building a simple linear regression model that might not be necessary. However, if we decide to use regularization, we might want to tune the parameter alpha.

### 2.1 D
Note - the mean of 1 and std. of 0 come from the constant column that we added

### 2.1 E
If we first standardize the data and then split, we might risk data leakage. That is because we are using information from the test set to scale the data. Instead we should first split the data and then standardize it using the train set statistics.

### 2.2.2
We observe RMSE ~1451.95. To calcualte it, first we compute the errors for all predictions -> (actual price - model prediction). Next we square all the erors, which is helpful because it allows us to treat positive and negative values equally and is sometimes used to also punish bigger errors more. To compute the MSE, we simply compute the average of the squared errors. Lastly, taking the root of the MSE essentially brings our metric back to the original units. *In this case, we can say that for a given car, the predictions from our linear regression model on average will be about 1451 euros away from the actual price.*

### 2.2.3
R-squared on the test dataset is ~0.82. This values means that our model explain ~82% of the variance in car prices observed on the test set. (Note the value is slightly lower than the adjusted r-squared observed on the training data - 0.853). Generally we want r-squared values closer to 1 as this indicates good generalization on the test set.

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
I think we could add the brand of the car although this is a categorical variable and it might increase the dimensionality considerably if we choose to use one-hot encoding. 
Additionally, a boolean flag indicating whether the full service history is included or not could be beneficial
to explaining the remaing variance. Also, we can add boolean features to indicate the presence of safety features such as ABS.

### 2.4
A confounding variable that may be correlated with the car's weight and price is the 'body type'. For example, we have Hatchback which is usually smaller in size and weight and more affordable than other types.
Then we have Sedans, which tend to be a bit bigger, offering sperate trunk space from the cabin, and thus they have mid-range prcies. Then there are SUVs which are bigger and boxier as well as more expensive than both Sedans and Hatchbacks. Lastly, there could also have the Minivan which is by far the heaviest and probably most expensive out of the 4 types mentioned.

### 2.5
With the inverse mileage term the r-squared has increased slightly by 0.001,
which means that we explain a bit more of the variance in car prices now. Additionally, we see that the inverser_mileage (x13) has p-value  of 0.006 which means that it is statistically significant at the 5% level.