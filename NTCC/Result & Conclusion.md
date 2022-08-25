# rough notes
* get plots for 
	* training set size = 100, 500, 1000, 5000
	* at time t = 20, 180
	* epochs = 500, 1000

* best result (least loss value) at 
	* 500 epochs
	* 5000 training set size

# Result
The effectuation of the model is primarily assessed by plotting the curve of actual solution and the predicted solution for a series of time variable, training set sizes and epochs. The plots are for solution at time t=0.10 and 0.90, for 100, 500, 1000 and 5000 samples of training set and for 500 and 1000 epochs. The plots are created using Matplotlib Python Library. The inference gathered from the variety of plots is that there is virtually no effect of increasing the training set size and the number of epochs on the result. The plots for 500 epochs and 1000 epochs, the plots for 100 samples and 5000 samples, all are virtually the same. The difference is very minute and can be noticed when the loss values of the models for various training sets and number of epochs are tabulated and compared. The least loss is observed for training set with 5000 samples. 

| training set size | epoch=500 | epoch=1000 |
| ----------------- | --------- | ---------- |
| 100               | 1.79e-02  | 7.51e-03   |
| 500               | 2e-03     | 2.66e-03   |
| 1000              | 2.17e-03  | 1.82e-03   |
| 5000              | 1.36e-03  | 1.57e-03   |

Along with the loss values, the time taken by each model to complete training is also noted 

| training set size | epoch=500 | epoch=1000 |
| ----------------- | --------- | ---------- |
| 100               | 3.136     | 6.500      |
| 500               | 9.821     | 18.659     |
| 1000              | 17.696    | 30.323     |
| 5000              | 73.918    | 135.287    |

# Conclusion
The proposed model can predict solution for the given wave equation with fair accuracy, considering the limited number of iterations. The constructed Neural Network model is able to predict the solution with a least relative L2 error of 1.36e-03 at 1000 epochs over 5000 samples. Using this, we can say that although with usage of complex approaches proposed by Raissi and Moseley can improve the physical learning of the model, relatively simple and computationally cheaper techniques like the one proposed here are able to predict the solution with appreciable accuracy as well.

# Future Work
There are several areas where there is scope of improvement. This includes application of PINN method for a variety wave equation problems. PINN is one of the latest advancements in the field of Neural Networks used for solving complex PDEs. Further improvement can be achieved with application of Monte-Carlo approximation coupled with Neural Networks approach. For representation of result, the predicted solution can be compared with solution obtained from numerical methods like Finite Difference Method, Finite Element Method or other known spectral methods. After said improvements, the model can then be applied for solving 2D, 3D wave equations with minimal set of training points, minimal architecture and other complex equations like Fokker-Planck equation, Schrodinger's equation, Navier-Stokes equation, etc.
