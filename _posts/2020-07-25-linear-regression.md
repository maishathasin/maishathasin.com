---
layout: post
title:  "Linear Regression with Gradient Descent!"
date:   2020-07-25 13:42:19 -0400
categories: machine learning
---

# Linear Regression 

    Linear regression is finding the linear relationship between two variables (x,y). Where x is the input variable and y is the result output and follows the equation y = mx + b where m is the gradient and b is the intercept. To summarise, we have a training data which shows the relationship between the X and Y values, and from the training set we will draw the relationship and then use this to predict Y values for unknown X values.
    I will use gradient descent algorithm instead of the regression formula as it has a better optimization.
                
### GRADIENT DESCENT
    The gradient descent algorithm is finding the minimum of a diffrentiable function. We apply the gradient descent algorithm by calculaing the partial derivative of the slope and the intercept and then update the slope and intercept in the gradient descent formula after each iteration.

    From highschool we have learned that to find the minima we need to calculate its derivative. And that is exactly what we are doing here
    We are finding the minima of the intercept and slope so the loss function that we are using here which is mean squared error function is (ideally) 0. 

    The loss equation looks like this:

![equation](/assets/images/equation.png)
    

    while the derivative in respect to m and c is 
![derivative](/assets/images/derivative.png)


    Ideally we would split 80% of the data to train the function i.e use the algorithim on this data and use the rest 20% of the data to test it, however, for this program i am using all the data to train the function.

    NOTE : We square the equation because we are trying to find the distance between the actual,correct point and the line that we have drawn to fit the points.


```python
import numpy as np 
import pandas as pd #a library that allows us to read CSV files and other table-like data structures
import matplotlib.pyplot as plt
```
```python
plt.rcParams['figure.figsize'] = (12.0, 9.0)

# Preprocessing Input data
data = pd.read_csv('gre.csv')
data
```
![data](/assets/images/data.png)

```python
X = data.iloc[:, 1]#gets all the values in the 2nd column
Y = data.iloc[:, 8]#gets all the values in the 8th column
plt.scatter(X, Y)
plt.xlabel('GRE score')
plt.ylabel('Chance of getting into university %')
plt.show()
```
![scatter](/assets/images/scatter.png)
```python
m = 0
c = 0

L = 0.0000001  #small learning rate
i = 100  

n = float(len(X)) 

# Performing Gradient Descent 
for i in range(i): 
    Y_pred = m*X + c  # The current predicted value of Y
    D_m = (-2/n) * sum(X * (Y - Y_pred))  # Derivative wrt m
    D_c = (-2/n) * sum(Y - Y_pred)  # Derivative wrt c
    m = m - L * D_m  # Update m
    c = c - L * D_c  # Update c


```
For this program we have just guessed  the learning rate and havent normalized it so the line will not accurately predict and have best fit line 

```python
Y_pred = m * X + c
y_new = m * 338 + c
y_test1 = m * 292 + c
#here we are testing with two values and plotting the output as a red dot  

plt.plot(338,y_new,'ro') #red dot
plt.plot(292,y_test1,'ro') 


plt.scatter(X, Y) 
plt.plot([min(X), max(X)], [min(Y_pred), max(Y_pred)], color='red')  # regression line
plt.show()
```
 ![regression](/assets/images/final-regression.png)



