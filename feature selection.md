>Chapter - [[]]

#Unlinked 
#incomplete 
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
1. helps in avoiding the curse of dimensionality 
2. helps in simplification of model so that it can be easily interpreted by the user
3. reduces the training time
4. reduce overfitting, hence enhance generalization
	- selecting such features so that the model is able to work on a variety of samples of data and is not fixated on a set of features

## techniques
two types of techniques
### 1. supervised 
- these can consider target variables and can be used for labelled dataset

### 2. unsupervised
