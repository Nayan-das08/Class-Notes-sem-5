# Progress Diary

>Nayan Ranjan Das
>A2305220148
>5CSE2

for NTCC In-House Training Project

***Project Title*: Solving Partial Differential Equations using Deep Learning Techniques**

## Week 1
* Explored and found 10 papers on the topic
* Studied deep learning coding aspect
* installed tensorflow, keras and jupyter notebook
* made a model using keras for digit recognition
	* learnt basics of keras
		* functions
		* data structures
		* arguments

## Week 2
* made another model for insurance data *(binary classification)* 
	* first using keras
	* then again using simple python and numpy
	* created essential functions
		* ```sigmoid()``` for sigmoid of a number to get probability at a point
		* ```los_loss()``` to calculate **binary crossentropy**
		* ```grad_descent()``` to calculate new values of weights and biases; keep updating them for some finite number of iterations
		* ```predict()``` to get values of probabilities on testing dataset
	* we also plotted the graph of cost vs weights

## Week 3
* Read original paper *(Lagaris et. al.)* and understood the basic objective
	* minimize (*LHS of the PDE* and the error from *initial and boundary condition functions to their actual given values*)
	* this can be replicated for first order, 2nd order and further complex PDEs
	* the method applies a feedforward NN approach along with gradient descent algorithm
* Grad descent optimizers
* backprop derivation

## Week 4
- created a model (a python Class) including the NN architecture
	- we initialized the weight and bias matrices for each hidden layer
	- weighted sum and non-linear aspects were introduced to the model using class constructor function
- explored optimizing algorithms
	- Gradient descent approaches - SGD, Mini-Batch, etc.
	- others - Adam, RMSProp, etc.

## Week 5
- developed a NN model for damped oscillating wave
	- this involves solving partial differential equation for damped oscillation
	- the equation is : $$m\frac{d^2u}{dx^2}+\mu\frac{du}{dx}+ku=0$$
	- we tried implementing a modified loss function 
		- we integrated the differential loss of each sample

## Week 6
- implemented 2-dimensional wave equation dependent of one  and temporal attributes.
- 2 dimensional PDE is : $$\frac{\partial^2u(x,t)}{\partial t^2}=c^2\frac{\partial^2u(x,t)}{\partial x^2}$$
- evaluated the result and streamlined the project pipeline
- plotted the Neural Network model results on testing data
- made arrays for loss values and time taken for different instances of epochs and sample size of training set.

---
# ANN Concepts
We will jot down brief notes about various concepts of ANN here
Note: Any mathematical thing will be written in physical diary

## Basics
* Feedforward NN
	* when a NN has only forward pass among the neurons

### Weights
* numeric values emphasising the importance of each node
* multiplied with activation function output 
* the values of weights are changed/updated as per gradient descent algorithm or via backpropagation

### Activation Function
* used to find the output of a node on the basis of input/incoming value and the weight.
* some commonly used activation functions are
	* sigmoid function
		* from 0 to 1
		* $f(x) = 1/(1+e^{-x})$
	* hyperbolic tangent function 
		* from -1 to 1
		* $f(x) = tanh(x) = (e^{2x}-1)/(e^{2x}+1)$
	* Rectified Linear Unit **(ReLU)** 
		* ```f(x) = max(0,x)```

### Bias Neuron
used to shift the activation function left or right to create an explicit bias in the output

### Backpropagation NN
* when a NN has both forward and backward passes among the neurons
* we calculate errors for output layer and propagate these errors backwards through the NN
* the values calculated for each node (except for input and bias neurons) is called **node delta**
	* $\delta_{output} = -Ef'_{i}$
	* $\delta_{input} = f'_{i}\Sigma_kw_k\delta_k$ 
		* $E$ is the error
		* $f'_{i}$ is the derivative of activation function at $sum$
		* $\Sigma_kw_k\delta_k$ is the sum of product of weight of inner neuron to outer neuron and the node delta of outer neuron
* gradient for weight from hidden node H1 to output node O1
	* output(H1) * node_delta(O1)

### Gradient Descent
* we update the value of weights using this algorithm
* $w_t := w_t - \alpha\frac{\partial J}{\partial w_t}$
	* $w_t$ is the weight 
	* $\frac{\partial J}{\partial w_t}$ is the change in cost function with respect to weight $w_t$
	* $\alpha$ is the learning rate
	* the algorithm guides the NN towards local minima of cost function via the direction of steepest descent
	* this is an iterative algorithm and is executed till the cost function gives value within acceptable thresholds

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
