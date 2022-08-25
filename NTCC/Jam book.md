# Jam book
*type here, paste there

## backprop in brief
* so backprop is calculating the gradients of cost function wrt. the weights starting from output layer towards the input layer, *one layer at a time*
* these gradients are used to update the values of respective weights as per the gradient descent formula
* used when number of hidden layers is large as gradient calculation can be difficult
* it is also known as **an example of automatic differentiation (AD) algorithm**
	* it is a special case of reverse mode accumulation AD technique 


## optimizers
* these are optimization algorithms
	* optimizes the cost function
	* utilizes the gradient obtained from **backprop**
* popular examples are
	* Gradient Descent optimizers
		* batch, stochastic, mini-batch, momentum
	* Adaptive optimizers
		* RMSprop
		* Nesterov accelerated gradient
		* adagrad
		* adadelta
		* adam - adaptive moment estimation
* different optimizers have different applications as per the field of work
* how to choose optimizers
	* start with Adam
		* will most probably give good (excellent) results
	* then shift to SGD
	* then try SGD with momentum
	* **tinker and explore**

### hence, optimizers along with backprop are used to train the Neural Network by updating the weights as per the various optimization algorithms using the gradients obtained from backpropagation

>[!NOTE]
>need to explore autodifferentiation and backprop relation
