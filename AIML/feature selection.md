>Chapter - [[_AIML]]

Sep 15, 2022
Topics - 

# Feature Selection
way of selecting the subsets of the most relevant features from the original feature set by removing the redundant, irrelevant or noisy features

>[!features vs labels]
>- features are input attributes
>- labels are class to which class particular sample belongs to

- while developing the ML model only a few variables in the dataset are useful for building the model and the rest features are either redundant or irrelevant

- if we input the dataset with all these redundant and irrelevant features, it negatively impact and reduce the overall performance and the accuracy of the model

## need for feature selection
1. helps in avoiding the ***curse*** of dimensionality 
2. helps in simplification of model so that it can be easily interpreted by the user
3. reduces the training time
4. reduce overfitting, hence enhance generalization
	- selecting such features so that the model is able to work on a variety of samples of data and is not fixated on a set of features

## techniques
two types of techniques
### 1. supervised feature selection
- these can consider target variables and can be used for labelled dataset
- there are mainly 3 techniques
	1. ***Wrapper Method***
		- selection of features done by considering it as a search problem 
		- in this different combinations are made, evaluated and compared with other combinations
		- trains the algo by using a subset of features iteratively
		- some techniques of Wrapper method are
			- **forward selection**
				- iterative method
				- which begins with an empty set of features
				- after each iteration it keeps adding on a feature and evaluates the performance to check whether it is improving the performance or not
				- the process continues until addition of new variable/feature doesn't improve the performance of the model
			- **Backward elimination**
				- opposite of forward selection
				- begins the process by considering all the features and remove the least significant features
				- process continues until removing the features doesn't improve the performance of model
			- **Exhaustive Feature selection**
				- it evaluates each feature set as brute force
				- one of the best method
				- tries and makes each possible combination of features and returns the best feature set
			- **Recursive**
				- recursive greedy optimization approach
				- features selected by recursively taking smaller and smaller subset of features
	2. ***Embedded Method***
		- **Regularization**
			- adds a penalty term to different parameters of the machine learning model for avoiding overfitting in the model
			- penalty term is added to the coefficients
			- shrinks some coefficients to zero
			- features with zero coefficients can be removed from the dataset
			- types of regularization techniques are 
				- L1 Regularization (Lasso Regularization) or Elastic Nets (L1 and L2 regularization).
		- **Dimensionality Reduction**
	1. ***Filter Method***
		- features are selected on the basis of statistics measures
		- does not depend on the learning algorithm and chooses the features as a pre-processing step
		- filters out the irrelevant feature and redundant columns using different metrics through ranking
		- needs low computational time and does not overfit the data
		- **Information Gain**
			- determines the reduction in entropy while transforming the dataset
			- used as a feature selection technique by calculating the information gain of each variable with respect to the target variable.
		- **Chi-Square Test**
			- technique to determine the relationship between the categorical variables
			- value is calculated between each feature and the target variable
			- and the desired number of features with the best chi-square value is selected
		- **Fisher's Score**
			- one of the popular supervised technique
			- returns the rank of the variable on the fisher's criteria in descending order
			- select the variables with a large fisher's score
		- ***Missing Value Ratio***
			- 

### 2. unsupervised
- can be used for unlabelled data


- we have coloured image
- the three image can be treated as unit by expressing each group of three corresponding pixels as vectors
- for example: let $x_1$, $x_2$ and $x_3$ be the value of the pixel for the RGB components
- these three elements can be expressed in the form of a 3D column vector $X$ where $X = [x_1, x_2, x_3]$
- this vector represents one common pixel in all three images
- if the images are of size $M\times N$, there will be a total $k=MN$ 3D vectors 
- if we have M registered images the vector will be M dimensional
- so we can treat the vectors as random quantities


...something i missed...

- covariance of random vectors
	- mean vector of population is defined as $m_X = E(X)$
	- where E is expected value of the arguments
	- subscript denotes that $m$ is associated with the population of $X$ vectors
	- covariance of the vector population is defined as $C_X = E[(x-m_X)(x-m_X)^T]$
	- because X is M dimensional, $C_X= E[(x-m_X)(x-m_X)^T]$ = qncpq is order of MXN 
	- The matrix $C_X$ real and symmetric
	- the element x_i and x_j are uncorrelated, their covar is zero
	- for k vector samples, random population, the mean vector can be approximated from the sample by using the familiar average function $m_x = 1/k summ_1_to_k(x_k)
	- similarly by expanding the product (x-m_x)(x-m_x)^T we get m_x = 1/k summ_1_to_k(x_k*x_k^T - m_x*m_x)
	- let A be the matrix whose rows are formed from the eigenvector of C_X, so that first row of A is the eigenvector corresponding to the largest eigenvalue and last row is the eigenvector corresponding to the smallest eigenvector
	- y = A(x - m_X)
	- this expression is called Hoteller transform

# how to choose a feature selection model
variables are of two main types
1. numerical var
2. categorical var

based on whether we have num or cat var as imput or output, we can choose our feature selection model as follows
1. input and output both are num
	- pearson correlation model
	- spearman rank coeff
2. input is num output cat
	- ANOVA
	- Kendall something
3. input is cat output is numerical
	- Kendall rank coeff
4. input cat cat output
	- chi square
	- mutual info















>[!NOTE]
>PCA = Principal Component Analysis

