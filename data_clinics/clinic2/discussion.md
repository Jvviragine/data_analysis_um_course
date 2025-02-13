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