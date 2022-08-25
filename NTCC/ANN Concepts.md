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

