# Rough idea
* implement the idea of PINN on examples of *one dimensional wave equation* (and damped wave equation, if time persists)
*  try different methods of data selection
	* the one already done
		* giving pretty good results
	* Raissi method
		* trying, ==if takes too much time, leave it==
		* not working
* compare results with Finite Difference Method
* **Future work** :-
	* compare with other spectral methods
	* try Monte-Carlo approximation
	* try 2D, 3D wave equations with minimal set of training points, minimal architecture
	* try other complex equations like Schrodinger's equation, 

# Methodology
I have created a model for predicting the solution of one dimensional wave equation with given initial and boundary conditions. I started with obtaining a labelled dataset for the training of the Neural Network model. The model is then implemented on the dataset (or a subset of it) to get series of predicted values of the solution for the PDE for the dataset. 

The PDE problem in question is 
	==insert PDE problem here* 
	*insert analytically obtained solution here*==

The dataset is prepared using Numpy, a Python Library for mathematical functions. The ```numpy.linspace()``` function is used to create a vector of 200 evenly spaced points between the boundaries of the concerned equation, which are from 0 to 1. This vector is used for both the independent variables the function - x and t. These vectors of independent variables are used to get the actual value of the solution for the points (x,t) using the analytically solved solution for the equation. The obtained solution is a 200x200 matrix containing values of the solution for each combination of values of x and t. 

For the training dataset I have randomly chosen 'n' number of samples from the main dataset. The number of samples chosen for training the Neural Network model is kept a variable so that the affect of number of samples on the accuracy of the prediction can be studied for some given number of epochs the model will iterate over the values for optimization. 

I have used Tensorflow and Keras Python packages for developing the model. The Multilayer Perceptron or the Neural Network model consists of 2 hidden Dense layers, each having 20 neurons. These layers help in computing the predicted value of solution with the help of Hyperbolic Tangent function as the activation function. 

==*insert tanh equation*==

The neurons multiply and add the incoming values with the associated weights providing the linear aspect of Neural Networks which is then used as the input for the activation function to provide the non-linearity required for generating the solution. The final layer of the model contains only one neuron which gives the output of the model as the predicted solution. This output is then compared with the actual solution to give an error value which needs to be minimized.

Other hyperparameters set for the model are the loss function, the optimizer and the learning rate for the optimizing algorithm. For the loss function the Mean Squared Error was chosen.

==*insert MSE equation*==

With rigorous trial and error method I have selected RMSprop optimizing algorithm as it was able to minimize the loss function with least number of epochs. Stochastic Gradient Descent and Adam and were among the algorithms that were tested for the model. The learning rate for RMSprop was selected in a similar manner and was finalized at 0.01.

For testing the accuracy, the plots for actual solution and predicted solution are presented over the same axis for various values of the time variable, so that the results can be compared visually. 

