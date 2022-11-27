>Chapter - [[_AIML]]

#incomplete 
Sep 29, 2022
Topics - 

# Simple Linear Regression
- most elementary type of regression model is simple linear regression
- we can train the relationship between dependent variable and independent variable
- it is a straight line plotted on the scatter plot of 2 vectors
- the best fit line formed by minimizing the Residual Sum of Squares (RSS)
- it is equal to sum of square of residuals for each data point in the dataset
- Residual for any data point is found by subtracting predicted value of dependent variable from actual value of dependent variable
- Strength of linear regression model can be assessed using two matrices $R^2$ or coefficient of determination
- ***Residual Standard Error ($R^2$)*** 
	- number which explains what portion of the given data variation is explained by the model
	- it always takes value between 0 and 1
	- higher the $R^2$ value, better the model predicts your data 
	- It is represented as $$R^2 = 1-\frac{RSS}{TSS}$$
		- RSS - Residual Sum of Squares
		- TSS - Sum of Errors of the data from the mean of response variable
			- it is the deviation from the mean line
			- TSS is represented as $$TSS = \sum_{i=1}^{n}(y_i-\bar y)$$
---
# Multiple Linear Regression
- statistical technique to understand the relationship between one dependent variable and $m$ independent variables
- objective is to find the linear equation that can best determine the value of dependent variable $Y$ for different values of independent variables $X$.

## very imp
- P value is used for hypo testing
- in regression model building the null hypo corresponding to each P value is that corresponding independent variable that doesn't affect the dependent variable
- the alt hypo is that the corresponding independent variable ...
- example: 
	- low P value where $P<0.05$ indicates that you can reject the null hypo - var not significant

---
# Handling Categorical Variables
- Categorical var need to be converted to num form to be used in regression model
- 
